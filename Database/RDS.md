# RDS

- RDS is a managed service for relational SQL databases
- Engines supported are:
    - PostgreSQL
    - MySQL
    - MariaDB
    - Oracle
    - Microsoft SQL Server
    - Aurora
- Provisioning of Databases are fully automated
- Uses EBS backed storage
- `Parameters` Groups can be used to configure the engine
- Dynamic parameters are applied immediately while static parameters need a reboot
    - For PostgreSQL and MS SQL server, SSL connections can be forced using `rds.force_ssl=1` parameter
    - For MySQL and MariaDB, SSL connections can be forced using `require_secure_transport=1` parameter

## Aurora

- Aurora is the proprietary RDS optimised db engine for AWS
- Starts at 10GB and scales to 128 TB
- Faster read replication and failover
- Stores 6 copies of all data across 3 AZ
    - Only requires 4 copies for write and 3 copies for read
- Self healing
- Storage striped across 100s of volumes
- Has automatic backups 1-35 days (can't be disabled)
- Backups restore to new cluster
- Aurora Backtracking can rewind cluster back and forth in time up to 72 hours
- Cloning creates a new db cluster using the same volume as the original cluster
    - Cloning uses *copy-on-write* protocol
    - Useful for creating test environments
- Can assign priority 0-15 for read replicas for failover
    - If replicas have the same priority, aurora will favor larger
    - If replicas are same priority and same size, aurora will pick randomly for failover
- Sends lag metrics to CloudWatch
    - AuroraReplicaLag
    - AuroraReplicaLagMinimum
    - AuroraReplicaLagMaximum
    - DatabaseConnections
    - InsertLatency

## Read Replicas

- Up to 15 Read replicas can be created for increased read performance
- Read replicas can work in single AZ, multi AZ, or cross region
- Read replicas use eventually consistent asynchronous read replication
- Can be promoted to their own DB
- RDS Read Replicas are good for analytics
- Use only for SQL `SELECT` statements
- Read Replicas network traffic is free within region but paid cross region

## Availability

- RDS Multi AZ can be used for disaster recovery
- Uses Synchronous copying
- Multi AZ can be used for automatic failover under several conditions:
    - Failed
    - OS patch
    - Unreachable due to loss of network connection
    - Modified
    - Busy and unresponsive
    - Storage failure
- Manual failover is also available
- Can not be used for scaling
- Read Replicas can be setup as multi AZ
- Moving to single AZ to multi AZ is a zero downtime operation
    - Snapshot is taken
    - New DB is restored from snapshots
    - New DB and old DB are synced

## Backups and Snapshots
- Backups
    - Continious
    - Allow point in time recovery
    - Occur during maintenance windows
    - When deleting a db instance, automated backups can be retained
    - Retention period between 0-35 days
- Snapshots
    - Require I/O operations and can stop database from seconds to minutes
    - Snapshots taken on Multi AZ db don't impact master, only standby
    - Incremental after first snapshot
    - Can copy and share
    - Final Snapshots available on deletion
    - Manual Snapshots can be shared cross accounts
    - Automated Snapshots require copying before sharing
    - Encryption keys must be shared for encrypted snapshots

## Scaling

- RDS autoscales storage
- Set *Maximum Storage Threshold* to limit scaling
- Storage is automatically modified if:
    - Free storage is < 10%
    - Low storage for >= 5 minutes
    - 6 hours have passed since last modification

## Networking

- RDS can use proxies for connections outside of VPC
    - This can be used to avoid a `TooManyConnections` exception in Lambda

## Monitoring
- RDS keeps a record of events such as an instance state going from pending to running
- Can integrate with SNS and EventBridge
- Database logs can be sent to CloudWatch
- Cloudwatch stores several metrics for RDS
    - DatabaseConnections
    - SwapUsage
    - ReadOPS
    - WriteOPS
    - ReadLatency
    - WriteLatency
    - ReadThroughput
    - WriteThroughput
    - DiskQueueDepth
    - FreeStorageSpace
- Enhanced monitoring can gather information from agent installed on DB instance
- Performance can be visualized on *Performace Insights Dashboard*
- Performance can filter by four metrics
    - Waits: bottlenecks from CPU or I/O
    - SQL Statements
    - Hosts
    - Users
- DBLoad is the number of Queries putting load on the db

## Security
- Supports at rest encryption using KMS
- Read replicas can't be encrypted if master is not encrypted
- User snapshot and restore to encrypt an unencrypted db
- In flight encryption via TLS
- Supports IAM authentication
- Use security groups to control subnets that RDS instances are in
- SSH available only through *RDS Custom*
- Audit logs can be retained by sending to CloudWatch Logs
