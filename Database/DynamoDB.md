# DynamoDB

---

- DynamoDB is a proprietary AWS managed highly scalable NoSQL Database

## Features

- Can scale to millions of requests per second, trillions of rows, 100s of TB of storage
- Single digit millisecond performance
- Standard and Infrequent Access (IA) table classes
- DynamoDB can rapidly evolve schemas

## Tables

- DynamoDB is divided into tables
- Each table must have a primary key defined at creation time
- Has an optional sort key
- No limit on number of rows
- Each item has attributes that can be added over time (can be null)
- Maximum item size is 400KB

## Data Types

- Scalar Types
    - String
    - Number
    - Binary
    - Boolean
    - Null
- Document Types
    - List
    - Map
- Set Types
    - String Set
    - Number Set
    - Binary Set

## Capacity modes

- There are multiple capacity modes

### Provisioned Mode

- User specified number of read/writes per second
- is default mode
- Ideal for predictable workloads and cost savings
- Pay per provisioned *Read Capacity Units (RCU)* and *Write Capacity Units (WCU)*
- Possibility to add autoscaling for RCU and WCU

### On-Demand Mode

- Read/writes scale automatically with workloads
- Ideal for unpredictable workloads
- No capacity planning needed or concept of RCU/WCU
- Pay per read/write (more expensive)

## DynamoDB Accelerator (DAX)

- DAX is a fully managed, highly available, seamless, in-memory cache for DynamoDB
- Can solve read congestion through caching
- Microseconds latency for cached data
- Doesn't require change in application logic
- Default 5 minute TTL

## Stream Processing

- Ordered stream of item level modifications (create/update/delete) in a table
- Use cases:
    - React to changes in real time (welcome email to new users)
    - Real time usage analytics
    - Insert into derivative tables
    - Implement cross region replication
    - Invoke Lambda function for data transformation
- Two types of stream processing *DynamoDB Streams* and *Kinesis Data Streams*:

| - | DynamoDB Streams | Kinesis Data Streams |
| --- | --- | --- |
| **Retention** | 24 hours | 1 year |
| **Consumer Number** | Limited | High |
| **Services for Processing** | Lambda Triggers or DynamoDB Kinesis Stream Adapter | Lambda, Kinesis Data Analytics, Data Firehose, Glue Streaming ETL |

## Global Tables

- *Global Tables* are tables replicated across multiple regions
- Two way replication
- Used to give DynamoDB tables low latency in multiple regions
- Applications can read and write to the table in any specific region
- DynamoDB Streams are required as a pre=requisite

## TTL

- DynamoDB allows automatic deletion of after expiry of a timestamp
- Use cases:
    - Remove out of date or unnecessary items
    - Adhere to regulatory regulations such as data privacy laws
    - Web session handling

## Backups

- Recovery process creates a new table

### S3 integration

- Export to S3
    - For data analysis and ETL 
    - No effect on read capacity
    - JSON or ION formats
    - Requires PITR
- Import from S3
    - Doesn't consume write capacity
    Creates new table
    - CSV, JSON, ION formats
    - Creates new tables
    - Import errors captured in CloudWatch Logs

### Backup Types

- Continuous backups using point in-time recovery (PITR)
    - Optionally enabled for the last 35 days
    - PITR to any time in the backup window
- On Demand Backups
    - Full backups for long term retention until explicitly deleted
    - No effect of performance or latency
    - Can be configured and managed in AWS Backup (enables cross-region copy)
