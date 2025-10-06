# Control Tower

- *Control Tower* is a service to set up and govern a secure and compliant multi-account AWS environment based on best practices

## Features

- Automate set up of environments in a few clicks
- Detect and remediate policy violations
- Monitor compliance through an interactive dashboard
- Runs on top of AWS organizations

## Guard Rails

- Automate policy management using guardrails
    - Preventative guard rails use SCPs
    - Detective guard rails use config
- Guard Rails have several levels:
    - *Mandatory*: automatically enabled and enforced
    - *Strongly Recommended*: in line with best practices
    - *Elective*: Optional

## Account Factory

- Automates the provisioning and deployments for new accounts
- Uses AWS Service Catalogue to provision new accounts
- *Account Factory Customization (AFC)* is used to customize resources in new and existing accounts
    - Uses a special CloudFormation template called a *Custom Blueprint* to define resources an configurations
    - Blueprints are defined as Service Catalogue Products in CloudFormation
    - It's recommended to store blueprints in a special hub account rather than a management account
    - Predefined blueprints created by AWS partners
    - Only one blueprint can be deployed per account
- *Account Factory for Terraform (AFT)* helps provision and customize AWS accounts using Terraform
- There are optional features for AFT which can be enabled:
    - CloudTrail Data Events
    - Enterprise Support Plan
    - Delete the Default VPC in all regions

## Landing Zones

- *Landing Zones* are automatically provisioned, secure, and compliant multi-account environments based on best practices
- Landing Zones consist of:
    - AWS organization
    - Account Factory
    - Organizational Units
    - Service Control Policies
    - IAM Identity Center
    - Guardrails
    - AWS Config

## Customizations for AWS Control Tower

- *Customizations for AWS Control Tower (CfCT)* is a GitOps-style customization framework created by AWS
- Helps add customizations to Landing zone using custom CloudFormation Templates and SCPs
- Automatically deploy new resources using Account Factory

