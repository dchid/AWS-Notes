# Firewall Manager

---

- Firewall Manager is a tool that manages all rules in all accounts of an AWS organization

## Features

- Firewall Manager works with:
    - WAF
    - Shield
    - Route 53 resolver DNS firewall
    - Security Groups
- *Security Policies* are common rule sets
    - Policies created at a region level and apply organization-wide
- *Shield Advanced* provides additional features on top of WAF

## Policies

- WAF policy can enforce applying Web ACLs to all ALBs in all accounts in an Organization
    - auto remediation optionally available
- Shield Advanced policy applies Shield Advanced in all accounts in an Organization

### Security group policy types

- Common Security Groups: Enforce applying SGs to all EC2 instances in all accounts in an Organization
- Auditing of Security Groups: Check and manage all SGs rules in all accounts in an Organization
- Usage Audit Security Groups: Monitor unused and redundant SGs and perform cleanup
- Network Firewall: centrally manage all firewalls
    - Distributed: creates and maintains firewall endpoint in each VPC
    - Centralized: creates and maintains firewall endpoint in single VPC
- Route 53 Resolver DNS Firewall: Manage rule groups in all accounts in an Organization

### Security Policies

- WAF: Enforce Web ACLs to all ALBs in all accounts in an Organization
    - Either identity non-compliant resources but don't remediate, or do remediate
- Shield Adavanced: Enforce Shield Advanced protections in all accounts in an Organization
