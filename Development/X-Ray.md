# X-Ray

---

- *X-Ray* is a service used to to trace code and get visual analysis for debugging

## Features

- Integrates with the following services:
    - EC2
    - ECS
    - Lambda
    - Elastic Beanstalk
    - API Gateway
- Can assume cross account IAM roles to aggregate debug data across multiple accounts
- X-Ray traces each request and separates them into *segments*
- Annotations can be added to traces
- Helps analyze performance bottlenecks
- Helps understand dependencies within a micro-service architecture

## Enabling X-Ray

- X-Ray supports the following languages using the AWS-SDK
    - Java
    - Python
    - Go
    - JavaScript
    - C#
- The SDK captures:
    - Calls to AWS services
    - HTTP requests
    - Database calls
    - Queue calls (SQS)
- To work on servers, the *X-Ray daemon* works at the transport layer and intercepts UDP packets
- X-Ray integration needs to be enabled for serverless services which support it
    - Lambda requires `AWSX-RayWriteOnlyAccess` permission and active tracing enabled to write to X-Ray
- Applications require IAM permissions to write data to X-Ray
