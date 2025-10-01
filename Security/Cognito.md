# Cognito

- *AWS Cognito* is a service to provide external access to AWS services, usually for logins
- Integrates with DynamoDB for login databases

# User Pools vs Identity Pools

- Use *User Pools* to create IAM users for logins
- Use *Identity pools* for temporary access with tokens

|             | User Pools  | Identity Pools   |
|-------------|-------------|------------------|
| Use         | User Logins | Federated Logins |
| Access Time | Long Term   | Temporary        |
| IAM User    | Yes         | No               |
| IAM Role    | Yes         | Yes (Temporary)  |
| SAML        | Yes         | Yes              |
| ODIC        | Yes         | Yes              |
| MFA         | Yes         | No               |
