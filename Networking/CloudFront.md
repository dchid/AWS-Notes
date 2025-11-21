# CloudFront

- CloudFront is a global CDN with 216 edge locations for caching all around the world 
- Uses Web Application Firewall for DDoS protection
- Supports Geo Restriction
- Supports signed URLs for private content using key pairs
    - CloudFront key pairs can **only** be created by the root user

## Origins

- S3 buckets
    - Enhanced security with Origin Access Control
    - CloudFront can be used as an ingress (upload data to S3)
- Custom Origin HTTP
    - Application Load Balancer
    - EC2 Instances
    - S3 Websites
    - Any other HTTP backend
- ALB can be used to access private instances from CloudFront

## Logging

- CloudFront Access Logs sends logging data to S3
- CloudFront supports several reports:
    - Cache Statistics Report
    - Popular Objects Report
    - Top Referrers Report
    - Usage Reports
    - Viewer reports
- Sends 4xx and 5xx status codes

## Caching

- Cache is based on:
    - Headers
    - Session Cookies
    - Query String Parameters
- Can control *Time To Live TTL* using header
    - Between 0 seconds to 1 year
- Cache can be manually invalidated using CreateInvalidation API call
- There are options to forward all headers, a whitelist of headers, or default headers only
- Whitelists can be set in the Behavior settings
- The Origin Custom Headers setting sets a constant header value for all requests to origin
- Maximize cache hits by separating static and dynamic distributions
    - Dynamic distributions make calls REST APIs or HTTP servers
    - Static distributions make calls to static assets
- Forward cookies for session affinity from ALB to CloudFront to enable stickiness

