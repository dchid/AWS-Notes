# Amazon Data Firehose

- *Data Firehose* is a service to send data from producers into target destinations

## Features

- Fully managed service
- Serverless
- Scales automatically
- Pay per usage
- Near real-time service

## Supported formats
- Supports several data formats
    - CSV
    - JSON
    - Parquet
    - Avro
    - Raw Text
    - Binary Data
- Supports converting data to Parquet and ORC
- Supports compression to gzip and snappy
- Supports custom data transformations through lambda

## Flow of Data

- Data is sent from producers in records <= 1MB
- Data can optionally be transformed by a lambda function connected to Firehose
- Data is accumulated in a buffer and the buffer is flushed during batch writes
- Some destinations include:
    - S3
    - Redshift
    - OpenSearch
    - Datadog
    - Splunk
    - mongoDB
    - Custom HTTP endpoints
