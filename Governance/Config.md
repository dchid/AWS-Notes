# Config

- Config is a service which helps with auditing and recording compliance with resources
- Compliance can be reviewed over time and cross referenced with CloudTrail logs
- Can receive SNS notifications for changes
- Config is a per region service, but can be aggregated across regions and accounts
- Possibility of storing configuration data in S3
- Supports AWS managed rules of custom Config rules defined by Lambda functions
- Config rules are for compliance, not enforcement
- No free tier
- Automate remediation of non-compliant resources using SSM Documents
    - Can use AWS managed documents or create custom documents
    - Can set up to 5 remediation retries
- EventBridge can can be used to trigger actions on non-compliant resources
- Notifications can also be triggered using SNS
- *Aggregators* are used to aggregate data on non-compliant resources in a specific aggregator account
