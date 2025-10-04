# Route 53

- Route 53 is a DNS service for AWS
- Route 53 is also a domain registrar
- Lets users manage DNS records
- CNAME records require subdomain
- The amount of time a record is cached is defined by the time to live (TTL)
- Aliases allow pointing to a specific AWS resource
    - Aliases can point root domains to resources
    - Aliases can target ELB, CloudFront, S3 Websites, VPC endpoint, API gateway
- Supports health checks (for public resources only)
- Calculated health checks allow combining health checks using AND, OR, NOT logic
- Can automatically switch an instance from primary to secondary in event of failover
- Supports 3rd party registrars like GoDaddy
- S3 websites need to have buckets with the same name as the domain

## DNS Records

- There are several record types
    - `A`: IPv4 address
    - `AAAA`: IPv6 address
    - `CNAME`: alias of one name to another
    - `NS`: delegated a DNS zone to use the given authoritative name servers

## Hosted Zones

- Public Hosted Zones are accessible through the public internet
- Private Hosted Zones are accessible only within a VPC and have no public IP address, only private

## Hybrid DNS

- Hybrid DNS is used to resolve queries between the Route 53 resolver and other DNS resolvers
- Inbound `Resolver Endpoints` are used to forward DNS queries to Route 53 Resolver
- Outbound `Resolver Endpoints` are used to forward DNS queries to on premise resolvers
- Resolver rules are used to manage private DNS

## Routing Policies

- Routing policies define how Route 53 responds to DNS queries
- Routing policies include:
    - Simple
    - Weighted: Control percentage of requests going to a specific record
    - IP: Based on client's IP
    - Failover: Automate failover in event of health check failure
    - Latency Based: Redirect queries to record with lowest latency
    - Geolocation: Based on where the user is based
    - Multi-Value Answer: Return multiple resources
    - Geoproximity: Shift more or less traffic to resources based on bias

