# EFS

- Elastic File System EFS is a managed file system for mounting NFS drives on Linux servers
- EFS drives require security groups
- EFS has several features:
    - Multi AZ support (multi region requires VPC peering)
    - Scales capacity automatically
    - Supports encryption with KMS
    - Supports moving files between storage tiers through lifecycle policy
- Performance mode can be set to general purpose of max I/O on creation
- Throughput mode has several settings:
    - Bursting: 1 TB = 50 MiB/s and burst up to 10MiB/s
    - Provisioned: Set throughput regardless of size
    - Elastic: Scales throughput automatically based on workload
- Access Points (NFS Shares) can be restricted using IAM policies
- Some operations such as encryption and enabling performance mode require AWS DataSync
- EFS has several CloudWatch metrics:
    - PercentIOLimit
    - BurstCreditBalance
    - StorageBytes
