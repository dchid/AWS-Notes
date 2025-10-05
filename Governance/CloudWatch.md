# CloudWatch

---

- CloudWatch is a monitoring service for AWS

## Metrics

- *CloudWatch Metrics* are variables to monitor in the cloud
- Metrics are organized into *Namespaces* with one namespace per service
- A *Dimension* is an attribute of a metric
    - Up to 30 dimensions per metric
- Metrics have time stamps
- Metrics can be pushed with past and future timestamps, often in error
- Metrics can be sent in real time to 3rd party services such as Splunk and Datadog via Kinesis Firehose
- CloudWatch can continually monitor metrics and use ML to detect anomalies
- Specific time periods can be excluded from training data and analytics

### Metric Filters

- *Metric Filters* are filter expressions on logs that can be used to create metrics
- Metrics created from filters can be used to trigger alarms
- Filters do **not** retroactively filter data from pre-existing logs
- Up to 3 dimensions can be specified for the metric filter

### Custom Metrics

- CloudWatch supports custom metrics using the `PutMetricData` API call
- Custom metrics can have custom resolution with the `StorageResolution` API
    - The default resolution is 60s with higher resolution available at a higher cost

### Dashboards

- CloudWatch can turn metrics into *Dashboards*
- Dashboards can span across accounts and regions
- Can be shared publicly
- 3 Dashboards with up to 50 metric for free and $3 per month per dashboard after

## Logs

- CloudWatch Logs are used to aggregate logs
- Logs are stored in *Log Groups* representing applications
- Log files within an application are stored in *Log Streams*
- Expiration can be managed with an expiration policy to expire between 1 day to 10 years or never
- Logs can be sent to:
    - S3
    - Kinesis Data Stream
    - Kniesis Firehose
    - AWS Lambda
    - OpenSearch
- Encrypted by default and support KMS

- *CloudWatch Logs Insights* enables querying of logs using a purpose built query language
    - Queries can be saved
- Logs can be batch exported to S3 using the `CreateExportTask` API
- For real time log forwarding, use *CloudWatch Log Subscriptions*
    - *Subscription Filters* define which log events are sent to the destination
- Log streams can be forwarded to *Live Tail* for debugging

### Agents

- There are three ways to send logs to CloudWatch
    - SDK
    - CloudWatch Unified Agent
    - CloudWatch Logs Agent (deprecated but still supported)
- CloudWatch agents support on premise servers
- In addition to logs, the unified agent can collect metrics such as:
    - CPU
    - Disk metrics
    - RAM
    - Netstat (number of TCP/UDP connections, net packets)
    - Processed (total, dead, running, sleeping)
    - Swap Space

### Log Types

- *Application Logs* are produced by application code
    - Written to local file system
    - Use CloudWatch Unified agent to stream to EC2
    - Direct integration with Lambda, ECS, Fargate
- *Operating System Logs* inform of system behavior
    - Use CloudWatch Unified agent to stream to EC2
- *Access Logs* list requests for individual files made from websites
    - Used for load balancers, web servers
- Logs from CloudTrail, CloudFront, Route 53, and ELB and S3 access logs are AWS managed

## Alarms

- Alarms can be used to alert users once metrics pass a certain threshold
- Alarms have three states:
    - `OK`
    - `INSUFFICIENT_DATA`
    - `ALARM`
- The period is the length of time in seconds to evaluate the metric
- Can send to SNS, EC2, or Auto Scaling
- `Composite Alarms` monitor multiple metrics by combining multiple alarms using AND/OR logic
- Billing data is a metric stored only in us-east-1
- Billing data can be used to make a billing alarm
- Alarms can be tested using the CLI with the below command

```bash
    aws cloudwatch set-alarm-state --alarm-name "name" --state-value ALARM --state-reason "testing"
```

## CloudWatch Synthetics Canary

- *CloudWatch Synthetics Canary* is a configurable script to monitor APIs, URLs or websites
- This allows reproduction of customer actions programmatically
- Scripts are written in NodeJS or Python
- Scripts can be run once, or on schedule
- Blueprints can be used as templates
    - *Heartbeat Monitor*: load URL, store screenshot and archive HTTP files
    - *API Canary*: test read/write functions of REST APIs
    - *Broken Link Checker*: check all links inside URL
    - *Visual Monitoring*: compare screenshot during canary run with baseline screenshot
    - *Canary Recorder*: record actions on a website automatically generate a script
    - *GUI Workflow Builder*: verify actions taken on web GUI
