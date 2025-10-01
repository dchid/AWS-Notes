# AWS Systems Manager

- AWS Systems manager (SSM) is a suite of tools used to manage your EC2 and on premise servers
- Systems manager can:
    - Automate patching
    - Get insights about the state of global infrastructure
    - Detect issues
- SSM only charges for resources it creates
- SSM agent is installed on Amazon Linux 2 AMI and some Ubuntu AMIs

- SSM Inventory is used to connect server metadata viewable in console or stored in S3 and queried via Athena
- Metadata collection can be collected at specified intervals
- State Manager is used to keep servers in a specific state as defined by a State Manager Association
- Fleet manager is used to manage fleets of EC2 instances

## Resource Groups

- *Resource Groups* are collections of resources deployed in AWS
- can be created using either tags or CloudFormation
- Useful for organizing resources by
    - applications
    - application components
    - environments
    - region/AZ

## Documents

- *SSM Documents* are JSON or YAML docs which define actions and parameters
- Can be used to run shell scripts
- Parameter Store allows for dynamic values in documents
- AWS provides many preconfigured SSM docs

## Session Manager

- *SSM Session Manager* allow access to SSH using an SSM Agent instead of an SSH key or instance connect
- Allows connection using:
    - AWS Console
    - AWS CLI
    - Session Manager SDK
- Session log data can be sent to S3 or CloudWatch Logs
- CloudTrail can intercept `StartSession` events
- An EC2 instance doesn't need to allow inbound SSH traffic over port 22 for connection as Session Manager gains access using the agent and the IAM policy
- Tags can be used to restrict access to only specific instances
- Allowed commands that run during an SSH session can be restricted

## Automation

- SSM can automate tasks such as:
    - Restart instances
    - Create an AMI
    - Take an EBS or RDS snapshot
- SSM automations can be triggered with
    - AWS Console
    - AWS CLI
    - AWS SDK
    - EventBridge
- An *Automation Runbook* is the document used to run automatons
    - Runbooks can be user defined or provided by AWS
- Use cases include:
    - Reducing costs by automatically starting and stopping EC2 instances
    - Build a golden AMI (similar to image builder)
    - Integrate with AWS config to automate bringing resources into compliance

## Run Command

- Run Command allows a single shell script to be run across an entire fleet EC2 instances in a resource group
- Include `runCommand` in an SSM doc to define a shell script
- Run Command output can be viewed in CloudWatch Logs by adding the `CloudWatchAgentServerPolicy` to the EC2 instance role

## Parameter Store

- SSM Parameter Store is a secure, serverless, KMS compatible storage for configurations and secrets
- SSM Parameter Store has version traking
- Parameter Store uses a file tree like hierarchy
- Parameter Store can be used to access AWS Secrets Manager using the following reference: "/aws/reference/secretsmanager/secret\_ID"
- Public parameters are issued by AWS
- Parameter Policies can give a parameter an expiration date (TTL)
- Multiple Parameter policies can be assigned at once
- There are two different tiers for parameter store:

| Tier | Standard | Advanced |
| --- | --- | --- |
| Parameters per account per region | 10,000 | 100,000 |
| Max size of parameter value | 4KB | 8KB |
| Parameter policies availability | No | Yes |
| Cross-account parameter sharing | No | Yes |
| Pricing | Free | $0.05 per parameter per month |

### CLI

- Parameters can be retrieved using CLI with the command `aws ssm get-parameters`
    - Use the `--names` flag to specify a parameter name
- Use`aws ssm get-parameters-by-path` to get all of the parameters within a path
    - use the `--path` flag to specify the path and the `--recursion` to search a path recursively
- Use the flag `--with-decryption` to decrypt encrypted values in the CLI output

## Patch Manager

- SSM Patch Manager automates OS, application, and security updates for servers
- Supports EC2 and on-prem
- Patch Manager scans instances and generates a *patch compliance report* to identify missing patches, which are uploaded to S3
- *Patch Policies* are used to define maintenance windows and patch baselines, and can be applied to resource groups

### Maintenance Windows

- Patches can be applied manually or scheduled with *maintenance windows*
- Supports CRON scheduling
- Maintenance windows contain:
    - Schedules
    - Duration
    - Set of registered instances
    - Set of registered tasks

### Patch Baselines

- *Patch Baselines* define which patches should be applied
- Patch Baseline defaults to critical and security updates only
- Predefined baselines are AWS managed and cant be modified
- The SSM Document `AWS-RunPatchBaseline` is used to apply patches
- Custom Patch Baselines can be created

### Patch Groups

- *Patch Groups* are a set of instances with a specific patch baseline
- Defined by the tag key `Patch Group`
- Instances can only be a part of one Patch Group
- Patch Groups can only be associated with on Patch Baseline

