# CloudTrail

---

- CloudTrail is a service to view history of all ALI calls made in an AWS account

## Event Sources

- API calls can come from:
    - SDK
    - CLI
    - Console
    - AWS services

## Event Types

- *Management Events* are operations performed on resources in an AWS account
- *Data Events* are read and write and execute events which are not logged by default due to volume
- *CloudTrail Insights* are used to detect unusual activity in an account

## Retention 

- Events are stored by 90 days by default
    - To keep events long term, they need to be logged in S3 and queried in Athena

## Features

- CloudTrail integrates with EventBridge to intercept API calls
- *Digest Files* contain all log files from previous hour with corresponding SHA-256 hash
    - This can be used to check if logs are tampered with
- *Organization Trails* are used to log all events for all accounts in an organization
