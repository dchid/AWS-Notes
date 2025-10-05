# Athena

---

- Athena is a serverless SQL based query service used to analyze data stored in S3

## Features

- Athena is built on the Presto engine which uses SQL
- Costs $5 per TB of data scanned
- Can be used to analyze logs and for data lakes
- *Federated Queries* allow queries to run on custom data sources
- Federated Queries connect to data sources using a special Lambda function called a *Data Source Connector*
- Athena is often used in conjunction with Amazon QuickSight to make reports and dashboards

## Supported Formats

- Supports several formats:
    - CSV
    - JSON
    - ORC
    - Avro
    - Parquet

## Performance Optimization

- Compress data for smaller retrievals
- Partitioning datasets helps improve querying in Athena
    - Partitions are separated by path-like strings
- Use columnar data type for cost savings:
    - Parquet or ORC are recommended formats
    - Glue can convert data to Parquet
- Using bigger files (> 128 MB recommended) improves scan performance

