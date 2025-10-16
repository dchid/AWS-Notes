# CodePipeline

- *CodePipeline* is a visual CI/CD workflow orchestration tool
- Pipelines have six distinct action types
    1. Source *(using CodeCommit, ECR, 3rd party version control)*
    2. Build *(using CodeBuild or 3rd party tools like Jenkins)*
    3. Test *(using CodeBuild, AWS Device farm, 3rd party testing tools)*
    4. Approval *(if manual approval is required)*
    5. Deploy (using CodeDeploy, Elastic Beanstalk, CloudFormation, ECS, S3)
    6. Invoke *(using AWS Lambda or Step Functions)*
- Pipelines are separated into stages and stages are separated into action groups
- Pipeline stages create *artifacts* which are stored in an S3 bucket to be passed on to the subsequent stages
    - input bucket must have versioning activated to work with CodePipeline
    - A customer managed KMS key is required for cross account deployments
- Stages can execute actions sequentially or in parallel
- Manual approval can be defined at any stage
- EventBridge can be used to trigger notifications upon a stage or build failing or being canceled
- CloudTrail can be used to audit AWS API Calls
- Pipelines require appropriate IAM permissions
- CodePipeline can trigger using events, webhooks or polling, but events are preferred
- Manual approvals are owned by AWS
- Manual approvals can trigger an SNS topic which can send emails to an IAM user
- IAM users need to have GetPipeline and PutApprovalResult permissions to manually approve pipelines

## CloudFormation Integration

- CloudFormation can be used as a deploy action to deploye resources in CodePipeline
- Works with CloudFormation StackSets to deploy across multiple accounts/regions
- Use CREATE_UPDATE action mode to create or update an exiting stack
- Use DELETE_ONLY action mode to delete test infrastructure
- Template parameters can be overridden in the JSON document

## Best Practices

- You can use one pipeline to deploy to multiple Deployment Groups in parallel
- Actions actions can be run in parallel by assigning actions the same *RunOrder*
- It is recommended to deploy to nonprod environments before deploying to production
- EventBridge can be leveraged to trigger appropriate actions on failed or canceled pipelines
- Pipeline functionality can be extended using Invoke actions
- Pipeline actions can be in different regions
- S3 artifact stores must be defined in each region where artifacts are being stored
