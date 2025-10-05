# Other Services

---

- *Service Quotas* allow alarms to be set when quotas have reached or are nearing their threshold
- *AWS Health Dashboard* shows health of regions and services for each day and has RSS feed and notifications
- *AWS Control Tower* can automate setting up organizations
- *Cost Explorer* is a tool to visualize and analyze costs over time
    - Can monitor costs by service, hourly resource levels, and forecast costs
- *AWS Budgets*  can be used to create a budget for an account and setup alarms
- *AWS Compute Optimizer* uses machine learning to optimize costs of compute resources
- *Datasync* is used for data migration between AWS and on premise resources or other clouds
    - Synchronizes on a schedule
    - POSIX compliant and maintains file permissions
    - Requires *AWS DataSync Agent* to sync on premise data
- *AWS Backup* is a fully managed service to automate backups across services
    - Supports cross region and cross account backups
    - Can create policies known as *Backup Plans*
    - *Backup Vault Locks* allow enforcing of Write Once Read Many (WORM) policy
- *Trusted Advisor* provides an account assessment and high level recommendations
    - Checks for cost: optimization, performance, security, fault tolerance, and service limits
    - Trusted advisor has 7 checks on basic and developer support plan: S3 Bucket Permissions, Security Groups, IAM use, MFA on Root Account, EBS Public Snapshots, RDS Public Snapshots, and Service Limits
    - Full Checks are available on business and enterprise support plans which allow for programmatic access using the AWS Support API
- *OpenSearch* is a service for Elasticsearch, an open source RESTful analytics engine
    - Managed by *Access Policy*
    - Recommended to have 3 access nodes

## AppConfig

- AppConfig is used to configurem validate and dyplay dynamic configurations outside of an app
- Integrates with EC2, ECS, EKS
- AppConfig can be thought of a dynamic settings menu for a cloud application
- AppConfig can have several sources such as SSM Documents, Parameter Store, or an S3 Bucket
- Configuration can be validated using either a JSON schema for a syntactic check or a Lambda Function for a semantic check

## Apmplify

- *Amplify* is a web and mobile app dev tool which can integrate many AWS services into a single stack
- Works with AWS services such as S3, Lambda, DynamoDB, Cognito, API Gateway, etc using CLI
- Connects to a front end such as View, React, Futter, etc.
- Supports CodeCommit, Guthub, BitBucket, and GitLab
- Is like elastic Beanstalk for web and mobile apps
- Can connect to CodeCommit and make one deployment per branch

## Security

- *AWS Shield* protects against DDoS attacks
    - Has free standard tier and paid advanced tier
- *Web Application Firewall (WAF)* protects web apps from common exploits using web ACLs and other tools
    - Protects against XSS, DDoS, and SQL injection
- *Amazon Inspector* automates security assessments on compute resources and sends findings to AWS *Security Hub*
    - Works on EC2, ECS, and Lambda
    - Gives risk score
- *Amazon GuardDuty* is a machine learning powered threat detection tool which monitors logs
    - Analyzes Cloudwatch Logs, VPC Logs, DNS Logs
    - Can protect against CryptoCurrency attacks
- *Amazon Macie* is a fully managed data security and privacy service which uses ML and pattern matching to find personally identifiable information
- *CloudHSM* is a physical hardware security module used to store encryption keys so that they are fulling stored and managed by the customer
    - Supports integration with Redshift
    - Uses CloudHSM software to manage keys instead of IAM
- *AWS Artifact* is a portal which provides customers with compliance documentation and AWS agreements
- *AWS Cognito* is used to create federated identity pools to allow external users assume IAM roles

