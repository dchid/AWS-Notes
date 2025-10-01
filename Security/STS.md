# Securtity Token Service


- *Securtity Token Service (STS)* is a service which allows temperoary assumption of IAM roles
- Uses `AssumeRole` and `GetSessionToken` API calls
- SAML and WebIdentity compatible
- Compatible with IAM and Cognito user pools
    - Cognito user pool integrate with API Gateway and ALB
- STS tokens can be used to grant temporary cross account access
- Uses *JSON Web Tokens (JWT) for federated access*
