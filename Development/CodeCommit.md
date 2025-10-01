# CodeCommit

- *CodeCommit* is a version control service in AWS
- Supports private git repos
- Hosts repos in a VPC
- Has no size limitations
- Is a fully managed cloud service
- Integrations with other AWS services
- Events such as pull requests can be monitored in AWS EventBridge
- Supports cross-region replication
- CodeCommit was abruptly discontinued on July 25th 2024

## Security

- Authentication with either SSH of HTTPS
- Authorization uses IAM policies, users, and roles
- Encrypted at rest using AWS KMS
- Cross account access using AWS STS (AssumeRole API)

## branch protections
- IAM policies can be used to implement branch security
- Pull request approval rules can be set up to require a certain number of authorized users approve a PR before merging branches
- Specify an IAM Principle ARN (of IAM users, roles, groups or federated users) to define who can approve a PR
- *Approval Rule Templates* can be used to define branch protections
