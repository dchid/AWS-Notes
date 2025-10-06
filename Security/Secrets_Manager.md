# Secrets Manager

---

- *Secrets Manager* is a serverless secrets store
- Supports forced rotations every n days
- Automate generation of secrets in rotation with Lambda
- Secrets can be encrypted using KMS
- Supports multi region secrets with read replicas in sync with primary secret
- Can be accessed using CLI or SDK
- CloudTrail captures non-API service events including:
    - `RotationStarted`
    - `RotationSucceeded`
    - `RotationFailed`
    - `RotationAbandoned`
    - `StartSecretVertionDelete`
    - `CancelSecretVertionDelete`
    - `EndecretVertionDelete`

# Compared to SSM Parameter Store

- Automatic rotation
- Secrets Manager is more expensive
- KMS encryption is mandatory
