# NAT Gateway

---

- A *Network Address Translation (NAT) Gateway* is a service that allows private subnets to access the public internet while preventing unsolicited inbound traffic
- AWS NATGW requires no administration and has high bandwidth and availability
- Pay per hour for usage and bandwidth
- NATGW is created and stored in a specific AZ and uses an elastic IP
- Can't be used by EC2 instance in the same subnet, only other subnets
- NATGW resides in a public subnet
- Requires an internet gateway
- 5 GB/s bandwidth with scaling up to 100 GB/s
- No security group needed
- NATGW is resilient within a single AZ, but can create multiple NATGWs in multiple AZs for fault tolerance
