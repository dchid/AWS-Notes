# CloudFormation

- CloudFormation is a JSON/YAML based IaC platform for AWS
- The log for user data is stored in `/var/log/cloud-init-output.log`
- The cfn-init script makes complex EC2 configs more readable
- Logs for cfn-init script go to `/var/log/cfn-init.log`
- cfn-signal scripts conditionally tell CloudFormation to wait for a signal in the event that cfn-init fails
- CloudFormation supports nested stacks
- ChangeSets are lists of changes made when stacks are updated
- CloudFormation Drift can be used to detect unwanted changes made to resources
- There are also CreationPolicy and UpdatePolicy attributes in addition to DeletionPolicies
- There are three types of update policies for ASG:
  - Replacing update
  - Rolling Update
  - Autoscaling schedule actions
- DependsOn is an attribute which prevents resources from being created before their dependencies
- Stack Policies define which resources can and can't be updates
- CloudFormation can automate the creation of architecture diagrams

## Templates

- CloudFormation Templates must be stored in S3 buckets
- CloudFormation Templates have several components
  - Resources: (The AWS resources declared in the template) Mandatory!
  - Parameters: Dynamic inputs
  - Mappings: Static Variables
  - Outputs: References to what was created
  - Conditionals: If statements to preform resource creation
  - Metadata
- Resources follow the format `AWS::aws-product-name::data-type-name`

### Resources

- Resource type identifiers are declared using the syntax `service-provider::service-name::data-type-name`
- The resource documentation is found at [here](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-template-resource-type-ref.html)

### Parameters

- Parameters have several types:
    - String
    - Number
    - CommaDelimitedList
    - AWS-Specific Parameter
    - SSM Parameter
- Parameters can be constrained by:
    - Description (String)
    - ConstraintDescription
    - Min/MaxLength
    - Min/MaxValue
    - Default
    - AllowedValues (array)
    - AllowedPattern (regex)
    - NoEcho (boolean) to prevent secrets from being logged
- Use the `!Ref` function to access parameters (shorthand for `Fn::Ref`)
- Pseudo Parameters such as `AWS::AccountId` and `AWS::Region` can be accessed at any time

### Mappings

- Mappings are for fixed values such as environments (dev vs prod), regions, AMI types, etc.
- The `Fn::FindInMap` function is used to find a named value from a specific key

### Outputs

- Outputs are useful for importing values to other stacks
- Use an `Export` block to export values
- Exported values need to be unique for a specific region
- Use the `ImportValue` function to import an output from another stack
- Importing values helps to prevent accidental deletion

### Conditionals

- Conditions are useful for basing resource creation on environment, region, or parameters
- CloudFormation supports several logical conditions:
  - `Fn::And`
  - `Fn::Equals`
  - `Fn::If`
  - `Fn::Not`
  - `Fn::Or`

### Intrinsic Functions
- Some important CloudFormation functions include:
  - `Fn::Ref`: Returns Physical ID of a resource or the value of a parameter
  - `Fn::GetAtt` Get an attribute of a resource
  - `Fn::FindInMap`: Access a named value from a specific key
  - `Fn::ImportValue`: Used to link outputs together
  - `Fn::Join`: Works the way as the str.join() function in python
  - `Fn::Sub`: Substitute values in strings
  - `Fn::ForEach` Iterates over array
  - `Fn::ToJsonString`
  - `Fn::Base64`: Primarily used to pass shell scripts in base 64
  - `Fn::Cidr`: Gets CIDR block
  - `Fn::GetAZs`: Gets availability zone
  - `Fn::Select`
  - `Fn::Split`
  - `Fn::Transform`
  - `Fn::Length`

## Deletion

- If a CloudFormation stack is deleted, then all of the resources that it provisioned will also be deleted
- *DeletionPolicies* define what should occur when a resource is deleted
- There are several DeletionPolicies:
    - **Delete**: Default, deletes the stack
    - **Retain**: Lets users choose which resources should be preserved
    - **Snapshot**: Takes snapshot of the resource before deletion
- The default deletion policy is delete
- DeletionPolicies will fail if a resource can not be deleted, such as a non-empty S3 bucket
- Termination Protection prevents accidental deletion of CloudFormation stacks
- `DELETE_FAILED` statuses are common when a resource like an S3 bucket needs to be emptied
- Security Groups can't be deleted until all of the instances within them are removed or deleted

## Rollbacks

- By default, failed stack creations will result in a rollback (they get deleted)
- There is an option to disable rollback to troubleshoot
- If stack updates failed, they will automatically roll back to previous stable states
- When roll backs fail, a stack will go into the `UPDATE_ROLLBACK_FAILED` state
- The `continue-update-rollback` API call can help to manually fix resources
- The `UPDATE_ROLLBACK_FAILED` status occurs when a rollback of a failed update fails as well
- Rollbacks can fail when resources are changed outside of CF, or due to insufficient permissions, or when an ASG doesn't receive enough signals

## Stack Sets

- StackSets allow the creation and deletion of stacks across multiple accounts and regions with a single operation
  - Admin accounts can create stack sets
  - Trusted accounts can create, update and delete stack instances from StackSets
  - StackSets have the ability to set max concurrent actions as number or percentage
  - Failure tolerance can also be set as a number or percentage
  - All stacks belonging to a StackSet are updated with the StackSet

## Stack Policies

- *StackPolicies* define which actions are permitted on different resources during updates
- There is no default StackPolicy, so resources can be updated
- StackPolicies protect all resources by default when set, so users need to specifically **allow** updates on resources

## Service Roles

- CloudFormation can use special IAM Roles called *Service Roles* to create and delete resources with CloudFormation
- Service Roles help with abiding by the principle of least privilege
- Users require the iam:PassRole permission to give a role to a specific service such as CloudFormation

## CloudFormation Capabilities

- `CAPABILITY_NAMED_IAM` and `CAPABILITY_IAM` are necessary when CloudFormation needs to create, update or delete IAM resources (Specify named when resources are named)
- `CAPABILITY_AUTO_EXPAND` is included in templates with macros or nested stacks
- CloudFormation will throw an `InsufficientCapabilitiesException` if a deployment lacks the necessary capabilities

## Custom Resources

- *Custom Resources* are used for several things
    - Manage resources that are not yet supported by CloudFormation
    - Manage on premise resources
    - Manage 3rd party resources
    - Take custom action on resources using a lambda function (such as emptying an S3 bucket before deletion)
- Custom resources are defined in the template using the syntax `Custom::<MyCustomResourceTypeName>`
- Can be backed by either a lambda function or an SNS topic
- The ARN of the SNS topic or lambda function must be provided in the template and they must be in the same region as the resource in question

## Dynamic References

- *Dynamic References* are used to reference external values in System Manager, Parameter Store, and Secrets Manager
- Dynamic References support:
    - **ssm**: for paintext values
    - **ssm-secure**: for secure strings in ssm
    - **secretsmanager**: for secret values in Secrets Manager
- The syntax to access Dynamic References is `'{{resolve:service-name:reference-key}}'`
- Dynamic References can be used to rotate passwords at regular intervals
- When the option *ManageMasterUserPassword* is set to true, a service such as RDS will automatically provision a master password
    - Use `!GetAtt ClusterName.MasterPassword.SecretArn` to access the password

## CloudFormation Helper Scripts

- CloudFormation supports *Helper Scripts* written in python that helps evolve the state of an EC2 instance without terminating it and creating a new one
- The scripts come with AMIs but can also be installed using package managers like yum or dnf
- There are four very important scripts:
    - **cfn-init** - used to install packages and files to an instance
    - **cfn-signal** - used to check that a cfn-init ran properly
    - **cfn-get-metadata**
    - **cfn-hup** Used to tell an EC2 instance to check for metadata changes every n minutes and apply

### cfn-init

- The init block of a CF script is in a resource and is used to define:
    - packages
    - groups
    - users
    - sources (to download files to an instance)
    - files
    - commands

### cfn-signal
- The cfn signal is usually run right after the init script to check if the init succeeded
- *WaitConditions* are used by cfn-signal to make a stack wait while checking if cfn-init worked
- cfn-signal uses an attached CreationPolicy
- The signal count defines the number of resources that require signals

### cfn-hup

- The cfn-hup script relies on a cfn-hup configuration file in `/etc/cfn/cfn-hup.conf` and `/etc/cfn/hooks.d/cfn-auto-reloader.conf` 

## Nested Stacks

- CF supports nested stacks which are useful for isolating repeated patterns and common components, so they can be called from other stacks
- Common examples for nesting are load balancers and security groups that are reused
- When updating a nested stack, always update the parent (root)
- *Cross Stacks* are helpful for stacks with different lifecycles that require imported and exported values, while nested stacks are good for reusable components
- Nested stacks should be used when the resources in the child stack are used **only** by the parent stack

## DependsOn

- The *DependsOn* key allows for the specification of order in creation of resources
- DependsOn is applied automatically when using `!Ref` and `!GetAtt` functions

## StackSets

- *StackSets* allow for deployments across multiple AWS accounts and regions
- Only an administrator account has permission to create stack sets, while the stacks are created, deleted, and updated in the target accounts
- When StackSets are are updated in the administrator account, all of the target stacks across all accounts and regions get updated
- To delete a StackSet, you need to delete all stacks within the StackSet, or remove the stacks from the StackSet
- StackSets sometimes fail when a template is trying to create global resources that must be unique but aren't such as S3
- StackSets can also fail when EC2 instances reach a limited quota

### Permissions
- There are two types of permission models for StackSets, Self-managed and Service-managed
- For self-managed permissions, IAM roles need to be assigned in both the administrator and target accounts
    - Admin accounts need `AWSCloudFormationStackSetAdministrationRole`
    - Target accounts need `AWSCloudFormationStackSetExecutionRole`
- For service managed permissions AWS organizations are used and StackSets create IAM roles on behalf of the users
    - This requires trusted access to be enabled with AWS Organizations
    - This also requires enabling all features in AWS Organizations
    - StackSets can be set to automatically deploy to new accounts when they are created

## ChangeSets

- *ChangeSets* are lists of changes that will be made when updating a CF stack
- ChangeSets will not say if an update will succeed or fail
- For nested stacks, change sets will list changes across all stacks

## Drift

- CloudFormation has drift detection as a feature
- Drift detection can be used for an entire stack, or individual resources
- StackSets can check for drift on each stack in the StackSet
- If stacks within a StackSet are updated individually, this is not considered drift (Although this is not best practice)
- When stacks drift either the stack can be updated to reflect the drift, or the resource can be updated back to what the stack defines
- CloudFormation does **not** support drift detection for custom resources.
