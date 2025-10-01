# Route 53

- Route 53 is a DNS service for AWS
- Route 53 is also a domain registrar
- Lets users manage DNS records
- DNS records have a Time to Love (TTL)
- CNAME records require subdomain
- Aliases allow pointing to a specific AWS resource
    - Aliases can point root domains to resources
    - Aliases can target ELB, CloudFront, S3 Websites, VPC endpoint, API gateway
- Supports health checks (for public resources only)
- Calculated health checks allow combining health checks using AND, OR, NOT logic
- Can automatically switch an instance from primary to secondary in event of failover
- Supports 3rd party registrars like GoDaddy
- S3 websites need to have buckets with the same name as the domain

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
    - Latency Based: Redirect to record with lowest latency
    - Geolocation: Based on where the user is based
    - Multi-Value Answer: Return multiple resources
    - Geoproximity: Shift more or less traffic to resources based on bias

