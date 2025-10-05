# Serverless Application Model

- AWS Serverless Application Model (SAM) is a framework for developing and deploying serverlss apps
- SAM generstes complext CloudFormation scripts from simple YAML files
- SAM can run Lambda, API Gateway, and DynamoDB locally
- *SAM Templates* are an extension of CloudFormation which provides simplified syntax
- The `Transform` header SAM to transform a SAM template into a CloudFormation template

## Templates

- Templates use YAML format
- `AWS::Serverless::Function` lambda functions
- `AWS::Serverless::Api` API Gateway
- `AWS::Serverless::SimpleTable` DynamoDB

## SAM CLI

- `sam init` command creates a directory for a SAM project
- `sam deploy` deploys the code (optionally preceded by `sam package`)
- `sam sync` sync local changes using SAM accelerate
    - use `--code` flag to sync code changes without infrastructure updates
    - use `--resource-id` flag to sync a specific resource
    - use `--watch` flag to monitor file changes and automatically sync when detected

## Deployment

1. Prepare code and template
2. Build the app locally with SAM build
3. Transform to CloudFormation
4. zip and upload to S3
5. Create and changeset on CloudFormation

## SAM Accelerate

- SAM accelerate is a set of features to reduce latency with deployments
- SAM accelerate uses service APIs rather than CloudFormation

## CodeDeploy integration

- SAM Can use CodeDeploy to deploy lambda functions
    - CodeDeploy creates an alias for lambda versions and shifts traffic to the current alias
    - Pre-traffic and post-traffic hooks can optionally be run
    - Can rollback using CloudWatch alarms
    - The `AutoPublishAlias` option in templates is used for automatic aliasing and deployment for lambda
