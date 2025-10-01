# VPC

- A *Virtual Private Cloud (VPC)* is a private cloud
- IPv6 can be enabled to operate subnets in a dual-stack mode
- *Egress Only Internet Gatway* is like NAT Gateway but for IPv6
- The default NACL allows all inbound and outbound traffic
- *Ephemeral Ports* are open only as long as a connection is active
- An *Internet Gateway (IGW)* is used for a VPC to connect to the internet
- The IGW connects to a Router managed by a *Route Table* which the connects to a subnet
- *Bastion Hosts* are EC2 instances in a public subnet used as proxies for instances in a private subnet
    - Security groups of Bastion Hosts need to only permit traffic from instances they are supposed to connect to
- A * Network Address Translation (NAT) Instance* allows EC2 instances in private subnets to public instances
    - NAT instances are **outdated and no longer used**
- NAT Gateways are AWS managed NAT instances
    - Resilient only in a single AZ, but can create multiple NAT Gateways in multiple AZs
- There are two DNS settings in VPCs
    - *enableDnsSupport* decides if Route 53 resolver is supported for the VPC
    - *enableDnsHostnames* decides if instances in public subnets can have public DNS
- *VPC Reachability Analyzer* is a network diagnostics tool that troubleshoots connectivity between two endpoints
- VPC Peering can be used to connect two VPCs
    - Peering is not transitive
    - Requires updated route tables
    - Can peer across accounts and regions
- *VPC Endpoints* are used by resources in private subnets to access other AWS services without sending traffic through the public internet
    - Redundant and scale horizontally
    - *Gateway Endpoints* are used to connect only to S3 and DynamoDB and need rout table configuration while *Interface Endpoints* are used for all services
- *Flow Logs* capture information about traffic going into interfaces
    - There are flow logs at the VPC, Subnet, and Elastic Network Interface (ENI) levels
    - Can be sent to CloudWatch, Kinesis, S3
- *Site-to-Site VPN* can be used to link a VPC to an on premise data center
    - Always encrypted
    - Uses *Virtual Private Gateway (VPG)* on cloud side and a *Customer Gateway (CGW)* on client side
    - *AWS VPN CloudHub* provides secure connections between multiple sites
- *Direct Connect (DX)* provides a private connection from a remote network to a VPC
    - Is not encrypted by default
    - Two modes of resiliency: high resiliency and maximum resiliency
    - Site-to-Site VPN can be used as a backup
- *AWS Private Link* can be used to provide a single service to a VPC without peering, internet gateway, or NAT
- *Transit Gateway* is used for transitive peering between thousands of VPC and on premise connections
    - Can work cross region and cross account
    - Managed by a route table
    - Supports IP Multicast
    - *Equal Cost Multi Path ECMP* routing allows forwarding packets over multiple best path
- Use *VPC Traffic Mirroring* allows capturing and inspection of network traffic within VPC

## Security
- VPCs have public and private subnets
- *Network Acess Control Lists (NACL)* are used to manage what traffic can flow in and out of a VPC
- *Security Groups* are used to manage what traffic can flow in and out of a Subnet
- Security Groups are stateful, while NACLs are stateless
- A newly created NACL will deny everything

- *AWS Network Firewall* protects an entire VPC
    - Works from network layers 3 to 7
    - Uses Gateway Load Balancer (level 3)
    - Rules can be managed cross account
    - Can send logs to S3, CloudWatch Logs, Kinesis

## CIDR
- *CIDR* blocks are used to define IP address ranges
- CIDR has a base IP and a *Subnet Mask*
- Subnet Masks define how many bits can change in the IP
    - The number of IPs available with a subnet mask of n is 2^(32-n)
- VPC CIDRs should not overlap

## Subnets
AWS reserves the first 4 IPs and the last IP of a subnet, so they can't be assigned to an EC2 instance
    - 0 is used for Network address
    - 1 is used for VPC router
    - 2 is used for DNS
    - 3 is reserved for future use
    - 255 is reserved for broadcast address
