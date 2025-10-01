# EBS

- EBS volumes are attachable storage for EC2 instances
- Volumes are bound to a specific Availability Zone
- EBS is mounted by network, not physical physical hardware
- EC2 instance stores are VMs with physically attached non persistent storage
- EBS volumes have storage capacity and I/O operations per second or _IOPS_
- Volumes can be encrypted using KMS keys
- By default the delete on terminate attribute is set to true on root volumes, and false on non root volumes
- There are several types of EBS volumes
- _EBS Multi-Attach_ allows provisioned iops volumes to be attached to multiple instances simultaneously within a single AZ
  - Volumes can be attached to up to 16 instances at a time
  - Requires cluster aware file system (no xfs or ext4)

| Name | Type | Speed | Boot | Min Size | Max Size | Multi Attach |
| --- | --- | --- | --- | --- | --- | --- |
| **gp2/gp3** | SSD | Standard | Yes | 1 GiB | 16 Tib | No |
| **io1/io2** | SSD | Fast | Yes | 4 GiB | 16 Tib | Yes |
| **st1** | HDD | Slow | No | 125 GiB | 16 Tib | No |
| **sc1** | HDD | Slowest | No | 125 GiB | 16 Tib | No |

- Volumes can be increased in capacity or performance, but not decreased
  - Drives need to be re-partitioned after resizing
- _EBS Snapshots_ allow users to create backups of their volumes
  - It is recommended but not required to detach volumes during a snapshot
  - Snapshots can be copied across AZs or regions
  - The time it takes to complete a snapshot is dependent on the amount of data written to the drive since the last snapshot was taken
  - If a drive was encrypted, a snapshot will require the same key to decrypt
  - Snapshots are stored in S3 behind the scenes
- Amazon Data Lifecycle Manager automates creation, retention, and deletion of snapshots
  - Can schedule backups across accounts and delete old backups
  - Uses tags to identify resource type
  - Can't be used to manage snapshots outside of DML
  - Can't be used to manage instance store backed AMIs
- Fast Snapshot Restore (FSR) reduces latency for restoration at great cost
- EBS Snapshot archives allows slower restoration at lower cost
- A recycle bin can be enabled to mark snapshots for deletion after a set amount of time to protect against accidental deletion
- There is a setting to encrypt new EBS volumes by default with an AES 256 KMS key


