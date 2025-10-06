# WAF

---

- The *Web Application Firewall (WAF)* protects web applications at the application layer (OSI layer 7)
- Can deploy on multiple services:
    - ALB for localized rules
    - API Gateway for rules running at the regional or edge level
    - CloudFront for global rules on edge locations
    - AppSync to protect GraphQL APIs
- Is **not** used for DDOS protection (Shield is for DDOS protection)
- Works by defining Web ACL
    - Rules can include IP address, HTTP headers, HTTP bodies, or URI strings
    - Protects against SQL injection and XSS
    - Can have rate based rules
    - Can have geo-match
- Can enhance CloudFront Origin security using custom HTTP headers in secrets manager

## Rules

- Rule Actions include:
    - Count
    - Allow
    - Block
    - CAPTCHA
    - Challenge
- WAF has over 190 AWS managed rules
    - *Baseline Rule Groups* give general protections from common threats
    - *Use-Case Specific Rule Groups* give protections for specific software stacks
    - *IP Reputation Rule Groups* Block malicious IPs
    - *Bot Control Managed Rule Group* protects against bot attacks

## Logging

- Can send log groups to CloudWatch at 5 MB/s
- Can send logs to an S3 bucket at 5 minute intervals
- Can send to Data Firehose
