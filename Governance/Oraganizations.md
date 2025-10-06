# Organizations

---

- Organizations is a global service used to manage multiple accounts

### Features

- The main account is the *Management Account* while others are *member accounts*
- Member accounts can only belong to one organization
- Used for consolidated billing and logging
- Pricing benefits from aggregated use
- To share reserved instances across accounts, turn on the share reserved instances setting
- The *Root Organizational Unit (OU)* controls several Management Accounts which then Control Members
- *Service Control Policies (SCP)* are IAM policies applied to OUs
- The `aws:PrincipalOrgID` condition is used in IAM policies to allow access from any IAM principal in all accounts within an organization
- *Tag Policies* can be used to enforce tagging requirements in your account
- A special IAM role called `OrganizationAccountAccessRole` is used to grant a management account full permissions to a member account
    - The role is stored in the member account and is automatically added when a new account is created within an organization
    - The role needs to be manually added for existing accounts
- Consolidated billing across all accounts can save money from aggregated usage
- In order to move accounts between organizations, an member account needs to be removed from the old organization and invited to the new organization

## Service Control Policies

- *Service Control Policies (SCP)* is a list of allowed or blocked IAM actions
- Can be applied at either an OU level or account level
- Does not apply to management account, only member accounts
- Applies to all users and roles in the account including the root user
- Service-lined roles enable other AWS services to integrate with AWS Organizations and thus can't be restricted by SCPs
- SCPs must have an explicit allow from the root of each OU in the path to the target account
