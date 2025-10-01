# Lambda

---

- Lambda functions are serverless functions which run on demand
- Lambda charges per invocation of functions
- CPU power is scaled by RAM
- At 1792MB of RAM, multi-core CPUs are enabled
- Function timeouts range between 3 seconds and 15 minutes

## Supported languages/runtimes and architectures

- Lambda supports several runtimes:
    - NodeJS
    - Python
    - Java
    - C#
    - Ruby
    - OS-only
- For natively compiled languages such as Go, Rust, and C++, use the OS-only runtime
- Lambda supports both X86 and arm CPU instruction sets

## Layers

- *Lambda Layers* are zipped libraries containing dependencies for functions
- Layers can be uploaded to lambda directly or imported from S3

## Versions

- Lambda supports creating function versions
- Versions are immutable, so the code, environment variables, and config can't be changed
- Each new version gets its own ARN

## Environment Variables

- Lambda supports environment variables in the form of key value pairs
- Environment variables are always strings
- Variables can be encrypted using KMS

## Invocation

- Lambda receives events (input) in JSON format
- Lambda functions can be triggered using EventBridge or CRON jobs
- Functions can be invoked either synchronously or asynchronously

### Aliases

- Lambda functions can be aliased where the alias acts like a pointer to a function
- Aliases are mutable
- Aliasing is useful for directing traffic to different versions of a function
    - This enables canary deployments
- Aliases **can not** point to other aliases

## Authorization

- Lambda functions get permissions from *Execution Roles* which have IAM policies attached
- An IAM principle can access lambda if:
    - The IAM policy attached to the principle authorizes it (user access)
    - The resource based policy authorizes it (service access)

## Storage

- Lambda includes up to 10GB of temporary storage in the /tmp directory
- *Lambda Execution Context* is a temporary runtime environment used to resolve dependencies and initialize connections
- Execution Context includes the /tmp directory
- Lambda can mount EFS (NFS) volumes if they are stored in a VPC
    - The file system is accessed using EFS access points
In order to have cross account EFS mounting, VPC peering is required

### Storage Options

| - | Ephemeral Storage | Lambda Layers | S3 | EFS |
| --- | --- | --- | --- | --- |
| **Max Size** | 10,240 MB | 5 layers per function (250 MB max) | Elastic | Elastic |
| **Persistent** | No | Yes | Yes | Yes |
| **Content** | Dynamic | Static | Static | Dynamic |
| **Type** | File System | Archive | Object | File System |
| **Operations supported** | any | immutable | Atomic with versioning | any |
| **Cost** | Included in lambda | Included in lambda | Storage, Requests, Data Transfers | Storage, Data Transfers, Throughput |
| **Sharing/Permissions** | Function Only | IAM | IAM | IAM, NFS |

## Concurrency

- Lambda can have up to 1000 concurrent invocations per account
- The maximum number of concurrent calls can be limited by setting a *reserved concurrency*
- Concurrency limits apply account wide
- If a concurrency limit is triggered:
    - Synchronous invocations will return an `HTTP 429` status
    - Asynchronous invocations and retry automatically and the go to the Dead Letter Queue (DLQ)
- Retry intervals start at 1 second and increase exponentially to a maximum or 5 minutes
- *Cold Starts* are when code is loaded and code outside of the handler is run (init)
    - If the init is large, cold starts can take a long time
    - The first request served by new instances has a higher latency than the rest
- *Provisioned Concurrency* can be used to avoid cold starts by allocating concurrency before invocation
    - Application Auto Scaling can be used to manage concurrency

## Monitoring

- Lambda Metrics include:
    - Invocations
    - Duration
    - Error Count
    - Concurrent Executions
    - Iterator Age (Kinesis and DynamoDB streams)
    - Async Event Age
    - Async delivery errors
- CloudWatch Logs Insights allows querying of CloudWatch Logs
- Lambda Insights can collect, aggregate and summarize system level metrics and diagnostic information
- Lambda Insights must be included as a layer to be used

# X-Ray Integration

- In addition to CloudWatch logs and and metrics, Lambda can also be integrated with X-Ray for tracing
- To enable the X-Ray Daemon, configure Lambda functions with Active Tracing
- X-Ray requires 3 environment variables for use in lambda:
    - `_X_AMZN_T RACE_ID`: Contains the trading header
    - `AWS_XRAY_CONTEXT_MISSING`: By default, `LOG_ERROR`
    - `AWS_XRAY_DAEMON_ADDRESS`: The X-Ray Daemon `IP_ADDRESS:PORT`
