# Config

---

- Config is a service which helps with auditing and recording compliance with resources

## Features

- Compliance can be reviewed over time and cross referenced with CloudTrail logs
- Can receive SNS notifications for changes
- Config is a per region service, but can be aggregated across regions and accounts
- Possibility of storing configuration data in S3 and queries in Athena
- *Aggregators* are used to aggregate data on non-compliant resources in a specific aggregator account

## Pricing

- $0.003 per config item recorded per region
- $0.001 per config rule evaluation per region
- No free tier

## Rules

- There are over 75 AWS managed config rules
- Users can define their own config rules using Lambda
- Config rules are for compliance, not enforcement
- Rules can be evaluated during changes, or at regular time intervals
- *Organizational Rules* are defined at an organization level

## Remediation

- Automate remediation of non-compliant resources using SSM Documents
    - Can use AWS managed documents or create custom documents
    - Can set up to 5 remediation retries
- EventBridge can and SNS be used to trigger actions on non-compliant resources

## Configuration Recorder

- A *Configuration Item* is a point in time view of a various attributes of a resource that's created whenever resources are changed
- *Configuration Recorder* is used to record Configuration Items
- Configuration Recorders are automatically created when using Config in the console or CLI
- An *Service Control Policy (SCP)* is placed at the root of an AWS organization to prevent config from getting disabled

## Conformance Packs

- *Conformance Packs* are sets of rules and remediation actions (essentially IaC for config rules)
- Packs use YAML format
- Can be deployed to an AWS account and regions, or across and AWS Organization
- AWS managed packs are available and users can create their on
- Can pass inputs via a parameter section
- Deployment can be automated using CodePipeline, CodeCommit, and CodeBuild
