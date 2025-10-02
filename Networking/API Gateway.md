# API Gateway

---

- API Gateway is a serverless application for building APIs
- API Gateway is most commonly used to invoke Lambda Functions
- Can be used to expose HTTP endpoints in the backend
- Supports WebSocket and HTTPS protocols


## Deployment

### Deployment Stages

- Changes made to an API need to be deployed before they go live
- Deployments are done in *stages*
- There is no limit to the number of deployment stages
    - You can have stages such as [dev, test, prod] or [V1, V2, V3..]
- Each deployment stage has its own configuration parameters
- Canary stages can be used to route a variable amount of traffic to two lambda aliases or other resource

### Stage Variables

- *Stage Variables* are like environment variables of API Gateway
- Stage variables are passed to the `context` object when a Lambda Function is invoked
- The syntax to access stage variables is `${stageVariables.variableName}`
- Stage variables are useful to define environments, Lambda aliases, and ARNs

### Endpoint Types

- There are ways to deploy API Gateway called EndpointTypes
    - *Edge-Optimised* (default) is accessible globally from every CloudFront Edge locations
    - *Regional* exposes endpoints within a single region
    - *Private* is accessible only within a VPC

## Cashing

- Caching can be overridden at the method level
- The Cache can be encrypted
- API Gateway sets a default TTL of 300s with a min of 0 and max of 3600
- Cache capacity is between 0.5 GB to 237 GB
- Caching is expensive, so it should be used in production
- There are two ways to invalidate the cache:
    - Flush it entirely from the console
    - Clients can invalidate cache with the header `Cache-Control:max-age=0`
- IAM permissions are required to invalidate the cache

## Open API

- API Gateway supports the OpenAPI specification
- OpenAPI compliant APIs can be imported to and exported from API Gateway
- The OpenAPI spec can be used for request validation (checking schema) within API Gateway

## Logging and Monitoring

- There are multiple ways to log and monitor different components of API Gateway

### CloudWatch Logs

- CloudWatch logs can be used to record information about API requests/responses
- Logging is enabled at a stage level
- Log levels can be set to `ERROR`, `DEBUG`, and `INFO`
- Log settings can be overridden on a per-API basis

### X-Ray

- X-Ray can be enabled to get extra information about requests
- Using X-Ray with API Gateway and Lambda gives a complete trace of an API call

### CloudWatch Metrics

- CloudWatch Metrics monitor by stage
- `CacheHitCount` and `CacheMissCount` metrics give information about caching efficiency
- `Count` metric is the total number of API requests in a given period
- `IntegrationLatency` metric measures the time between when API Gateway relays a request to the backend and when the backend responds
- `Latancy` metric measures the overall amount of time it takes to respond to a client request
- The default timeout for an API call is 29 seconds
- `4XXError` and `5XXError` metrics measure the number of client-side and server-side http error code being returned

### Throttling

- By default API Gateway throttles requests at 10,000 requests per second across all APIs
    - This is a soft limit which can be increased upon request
- In the case of throttling, API gateway will send an `HTTP 429` status for "Too Many Requests"
- *Stage Limits* and *Method Limits* can be set to make sure a single stage or method doesn't exhaust the account's quota
- *Usage Plans* can be used to throttle on a per-customer basis

## Security

- There are three ways to provide authentication on API gateway
    - IAM Roles
    - Cognito (for external users)
    - Custom Auth
- API Gateway supports HTTPS with custom domains using ACM and Route 53
