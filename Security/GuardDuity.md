# GuardDuty

---

- *Amazon GuardDuty* uses intelligent threat discovery and ML to protect AWS accounts

## Features

- It can be enabled in one click and starts with 30 day trial
- Looks at:
    - CloudTrail Event Logs for unusual API calls
    - VPC flow logs for unusual traffic and IP addresses
    - DNS logs for compromised EC2 instances
    - **Optionally** S3, Lambda, RDS, EBS, EKS
- Can protect against crypto currency attack
- Multi-Account Strategy can be enabled using Organizations
- A member account in a Organization can be designated as the GuardDuty Admin
- Has trusted and threat IP lists of public IP addresses that are know to be either safe or malicious
- If GuardDuty is already enabled in a target account, a CloudFormation template that tries to set up GuardDuty will fail
    - This can be mitigated using CloudFormation custom resources

## Findings

- *Findings* are potential security issues detected by GuardDuty
- Findings are sent to Eventbridge, which can trigger actions to remediate
- Findings are assigned a severity value between 0.1 and 8+
- The naming convention is `ThreatPurpose:ResourceTypeAffected/ThreatFamilyName.DetectionMechanism!Artifact`
    - `ThreatPurpose`: primary purpose of threat
    - `ResourceTypeAffected`: impacted resources
    - `ThreatFamilyName`: describes potential malicious activity
    - `DetectionMechanism`: how GuardDuty detected the finding
    - `Artifact`: resource used in malicious activity

