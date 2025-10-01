# API Gateway

---

- API Gateway is a serverless application for building APIs
- API Gateway is most commonly used to invoke Lambda Functions
- Can be used to expose HTTP endpoints in the backend
- Supports WebSocket and HTTPS protocols
- The default timeout for an API call is 29 seconds

## Deployment

### Deployment Stages

- Changes made to an API need to be deployed before they go live
- Deployments are done in *stages*
- There is no limit to the number of deployment stages
    - You can have stages such as [dev, test, prod] or [V1, V2, V3..]
- Each deployment stage has its own configuration parameters

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

## Security

- There are three ways to provide authentication on API gateway
    - IAM Roles
    - Cognito (for external users)
    - Custom Auth
- API Gateway supports HTTPS with custom domains using ACM and Route 53
