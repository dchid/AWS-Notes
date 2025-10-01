# Snow

- The AWS Snow family is a series of highly secure, portable devices used for data migration and edge computing
- There are three storage devices:
    - Snowcone
    - Snowball Edge
    - Snowmobile
- OpsHub is a desktop app for managing snow devices

## Snowball Edge

- The Snowball Edge is used to transfer terrabytes or petabytes of data
- Pay per data transfer job
- Has block storage and S3 compatible object storage
- Two variants of the device:
    - *Snowball Edge Storage Optimized* has 80 TB of HDD storage
    - *Snowball Edge Compute Optimized* has 42 TB of HDD storage or 28 TB of NVMe SSD storage
- Can run EC2 Instances and Lambda functions using AWS IoT Greengrass

## Snowcone
- Very small 2.1 kg device
- 8 TB of HDD storage or 14 TB of SSD storage
- Customer must provide batteries and cables
- Compatible with datasync

## Snowmobile
- An entire massive trucking truck!
- Used for exabytes of data transfer
- Offline only with 24/7 surveillance
