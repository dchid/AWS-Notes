# CloudWatch

- CloudWatch is a monitoring service for AWS
- *Metric* are the variables which are monitored
- Metrics belong to *Namespaces*
- A *Dimension* is an attribute of a metric
- Metrics have time stamps
- CloudWatch supports custom metrics using the `PutMetricData` Api call
- Custom metrics can have custom resolution
- Metrics can be pushed with past and future timestamps, often in error

## Dashboards
- CloudWatch can turn metrics into *Dashboards*
- Dashboards can span across accounts and regions
- Can be shared publicly
- 3 Dashboards with up to 50 metric for free and $3 per month per dashboard after

## CloudWatch Logs
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
- Ecrypted by default and support KMS
- CloudWatch logs can collect logs from a CloudWatch Agent
- *CloudWatch Logs Insights* enables querying of logs using a purpose built query language
- Queries can be saved
- Logs can be batch exported to S3
- For real time log forwarding, use *CloudWatch Log Subscriptions*
    - Subscriptions are sent using destinations

## CloudWatch Alarms
- Alarms can be used to alert users once metrics pass a certain threshold
- Aalrms have three states: `OK`, `INSUFFICIENT_DATA`, `ALARM`
- Can send to SNS, EC2, or Auto Scaling
- `Composite Alarms` monitor multiple metrics by combining multiple alarms using AND/OR logic
- Biling data is a metric stored only in us-east-1
- Billing data can be used to make a billing alarm

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
