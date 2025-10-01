# Organizations

- Organizations is a global service used to manage multiple accounts
- The main account is the *Management Account* while others are *member accounts*
- Member accounts can only belong to one organization
- Used for consolidated billing
- Pricing benefits from aggregated use
- To share reserved instances across accounts, turn on the share reserved instances setting
- The *Root Organizational Units (OU)* controls several Management Accounts which then Control Members
- *Service Control Policies (SCP)* are IAM policies applied to OUs
- The `aws:PrincipalOrgID` condition is used in IAM policies to allow access from any IAM principal in all accounts within an organization
- *Tag Policies* can be used to enforce tagging requirements in your account
