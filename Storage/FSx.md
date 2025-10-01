# FSx
- FSx allows launching of 3rd party high-performance file systems on AWS including:
    - Luster
    - Windows File Server 
    - NetApp ONTAP
    - OpenZFS

## Lustre

- Distributed HPC computing for Linux
- Millions of IoPs
- Seamless S3 integration 
- Connect with VPN or Direct Connect

## Windows File Server

- SMB protocol
- Daily S3 Backup
- Multi AZ config available
    - Use multi AZ for replication with failover
- Connect with VPN or Direct Connect

## NetApp ONTAP

- Compatible with NFS, SMB, or iSCSI protocols
- Works with: 
    - Linux
    - Mac
    - Windows
    - EC2
    - ECS
    - EKS
    - Appstream
    - VMware 
    - Amazon Workspaces
- Autoscales storage
- Supports Snapshots replication, data compression data de-duplication

## OpenZFS
- Uses NFS protocol only
- Works with: 
    - Linux
    - Mac
    - Windows
    - EC2
    - ECS
    - EKS
    - Appstream
    - VMware
    - Amazon Workspaces
- Up to 1,000,000 IOPS with < 0.5 ms latency

## File Systems

- Scratch File System
    - Data is not replicated
    - High Burst
    - Used for short-term processing and cost optimization
- Persistent File System:
    - Single AZ Replication
    - Long term storage
