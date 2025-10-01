# KMS

- *Key Management Service (KMS)* is a service which provides AWS managed encryption keys
- Fully integrates with IAM
    - Keys can be assigned to IAM users or IAM groups
- Able to audit key use from CloudTrail
- KMS supports symmetric encryption with AES-256 and Asymmetric encryption with RSA and ECC
- Private asymetric keys can't be downloaded and have to be accessed by API call
- There are three types of keys:
    - AWS owned keys: Can't be controled by users
    - AWS managed keys: Can only be used within assigned service
    - Customer Managed Keys
- *Key Policies* are JSON documents used to define which users and groups have access to a KMS key
- The key used to encrypt an EBS volume can't be changed
- Cross account key sharing needs to be configured in a key policy
- A key can be scheduled for deletion with a waiting period of 7 to 30 days
    - During a waiting period, a key can't be used for cryptographic operations
    - Keys scheduled for deletion will not be rotated

## Key Rotation
- Automatic key rotation can be set for customer managed
- Non-customer managed keys are automatically rotated annually
- Manual key rotation will assign a new key ID while automatic key rotation will not
- Using aliases are used to hide the occurrence of a key rotation
