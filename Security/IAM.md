# IAM

---

## Features

- *Identity and Access Management (IAM)* is used to manage authentication and authorization in AWS
- *IAM Users* can inherit permissions from *IAM Groups* when assigned to them
- *IAM Policies* are JSON documents which define permissions
- *IAM Roles* are sets of permissions defined by the IAM Policies attached them which can then be assumed by users
- *IAM Credentials Report* is a report generated at an account level which summarized users and their credentials
- *IAM Access Advisor* shows what permissions a user has and when they were last used
- *IAM Access Analyzer* is used to find out which resources are shared internally and externally
    - Used to enforce least privilege
    - Creates analyzers to get findings
    - Works by defining a zone of trust (such as an AWS account)

## IAM Identity Center

- *IAM Identity Center* provides SSO on for all AWS accounts as well as 3rd party apps
- Supports Identity Federation using SAML 2.0
    - Supports Okta, Azure AD, OneLogin
    - SAML does not provide a way to query users and groups so identical users and groups must be created for the external ID provider
    - The *System for Cross Identity Management (SCIM)* protocol can be used to synchronise users and groups
- Allows login to EC2 Windows instances
- The Identity provider can be either the build in identity store or a 3rd party such as Active Directory
- *Permission Sets* are collections of one or more IAM policies which define which users have access to what
- Can grant multi account permissions
- Provides required certificates, metadata and URLs
- *Attribute-Based Access Control (ABAC)* provides fine grained permissions based on user attributes
    - ABAC can be controlled by tagging resources and IAM users
- MFA is supported in two modes:
    - Always-on
    - Context-aware (only when sign in context changes)
