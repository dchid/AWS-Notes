# DMS

---

- *Database Migration Service (DMS)* helps migrate on premise databases to AWS

## Features

- Resilient and self healing
- The source DB remains available
- The data source remains available during the migration
- Supports both homogeneous (from same DB engine) and heterogeneous integrations (from one DB engine to another)
- Continuous data replication using Change Data Capture (CDC)
- Can use either EC2 to perform replication or serverless migration
- Supports multi-AZ deployment which maintains a synchronous stand in replica
    - Provides data redundancy
    - Elminates I/O freezes
    - Minimizes latency spikes
    - Ideal for production workloads

## Sources and Targets

- *Schema Conversion Tool (SCT)* is used to convert one database schema to another
- Sources
    - On-premise databases (MySQL, MariaDB, etc.)
    - EC2 Instances
    - Azure SQL DB
    - RDS
    - S3
    - DocumentDB
- Targets
    - On-premise databases (MySQL, MariaDB, etc.)
    - EC2 Instances
    - RDS
    - Redshift
    - DynamoDB
    - S3
    - OpenSearch Service
    - Kinesis Data Streams
    - Apache Kafka
    - DocumentDB & Amazon Neptune
    - Redis & Babelfish

## Monitoring

- *Task Status* indicates the condition of the task (created, running, stopped, etc.)
- *Table State* includes the current state of the table (before load, table completed, etc.)
- Host metrics for utilization statistics
    - `CPUUtilization`
    - `FreeableMemory`
    - `FreeStorageSpace`
    - `WriteOPS`
- Replication task metrics for changes between source and target
    - `FullLoadThroughputRowsSource`
    - `FullLoadThroughputRowsTarget`
    - `CDCThroughputRowsSource`
    - `CDCThroughputRowsTarget`

