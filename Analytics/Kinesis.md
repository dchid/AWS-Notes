# Kinesis

---

- *Amazon Kinesis* is a family of services used for processing and analyzing large data streams in real time

## Kinesis Data Streams

- *Kinesis Data Steams* is a service to collect and store streaming data in real time
- Streams can be used for IoT devices, Click Streams, and metrics/logs
- The Kinesis agent can forward data from a device to Kinesis Data Streams
- A *Producer* is a user written piece of software to forward stream data from a server or embedded system.
- *Consumers* are applications which consume stream data such as:
    - AWS Lambda
    - Server applications
    - Amazon Data Firehose
    - Apache Flink
- Data can be retained on the stream for up to 365 days
- Data can't be deleted from Kinesis until it expires
- Data up to 1 MB can be sent but it's designed for small real time data
- Data is ordered and have *Partition IDs* to show their relation in time
- Data is encrypted at rest using KMS and encrypted in-flight with HTTPS
- Use the *Kinesis Producer Library (KPL)* to write an optimized high throughput producer application
- Use the *Kinesis Client Library (KCL)* to write an optimized consumer application

### Capacity Modes

- There are two capacity modes

#### Provisioned 

- Shard number is user defined
- Each shard gets 1MB/s or 1000 records per second input
- Each shard gets 2MB/s out
- Scale manually to increase or decrease shard number
- Pay per shard provisioned per hour

#### On-demand mode

- No need to provision or manage the capacity
- Default capacity provisioned (4 MB/s or 4000 records per second)
- Scales automatically based on observed throughput peak during last 30 days


