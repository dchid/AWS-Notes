# Storage Gateway

- Storage Gateway is used for a *hybrid cloud* strategy to have storage on premises and in cloud
- Storage Gateway is Posix Compliant
- Storage Gateway can be activated using CLI or http request on port 80
- Uses include:
    - Backup and Restore
    - Disaster Recovery
    - Tiered Storage (for warmer or colder data)
    - On-premise cache
- Storage Gateway supports a hardware appliance

## Types of Storage Gateways
- S3 Storage Gateway
    - Use s3 bucket as on premise file share
    - Active Directory integration
    - Does not support Glacier
- FSx Storage Gateway
    - Works with FSx for Windows File server
    - Primarily used for caching
- Volume Storage Gateway
    - Block storage using iSCSI protocol
    - *Cached Volumes* are used for low latency access to most recent data
    - *Stored Volumes* are used for scheduled backups to S3 when the entire data set is on premise
    - CasheHitPercent metric measures cache efficiency in CloudWatch
- Tape Storage Gateway
    - Used for backup to Glacier
    - Supports iSCSI interface
    - Requires stopping, rebooting, then starting service during reboot
