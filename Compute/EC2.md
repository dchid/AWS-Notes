# EC2

---

## Features

- Elastic Compute Cloud (EC2) is a server rental service from AWS
- EC2 Servers are called *Instances*
- EC2 supports x86 and ARM backed instances
- Instances have several states:
  - Pending
  - Running
  - Stopping
  - Stopped
  - Shutting Down
  - Terminated
- Amazon Machine Images (AMIs) are images to initialize an EC2 instance
- Enhanced Networking (SR-IOV) Gives Higher bandwidth more packets per second and lower latency
- Use `modinfo ena` command to check for ENA kernel module data
- Amazon Linux 2 has ENA kernal modules installed and enabled by default
- Two types of of SR-IOV:
  - Elastic Network Adapter up to 100 Gb/s
  - Intel 82588VF up to 10 Gb/s for legacy
- Elastic Fabric Adapter (EFA) is an improved ENA for HPC on Linux
  - Great for inter-node communications and tightly coupled workloads
  - Used Message Passing Interface (MPI) standard
  - Bypasses OS for low latency, reliable transport
- Termination protection won't work if shutdown behavior is set to terminate and the instance is shutdown via SSH
- InstanceLimitExceeded means that the max number of vCPUs per region has been reached
- InsufficientCapacity Means that AWS lacks OnDemand capacity in a particular AZ
- Instance Terminates Immediately is an EBS or AMI issue
- Burst instances (T2/T3) overall have ok CPU performance but can boost to be very good when needed
  - If the machine bursts, it uses a _burst credit_ which are accumulated over time
  - Great for handling unexpected traffic
  - Unlimited credit balance is available at extra cost
- Elastic IP:
  - Public IPv4 changes whenever instances are restarted
  - can be attached to one instance at a time and can remap across instances
  - Elastic IPs only cost money when they aren't mapped to a server
  - 5 elastic IPs per account by default
  - Avoid using Elastic IP is possible; use load balances in most cases
- _EC2 Hibernate_ saves the instance's RAM to the root EBS volume (which must be encrypted)
  - Hibernate won't work for RAM amounts greater than 150 GB
  - Hibernation can't last longer than 60 days

## Monitoring

- CloudWatch provided metrics for EC2:
    - _basic monitoring_ with 5 minute intervals by default
    - can be configured to use _detailed monitoring_ with 1 minute intervals
    - Monitors CPU, Network, Disk, Status Checks (RAM **not** included)
- Custom metric for EC2:
    - Can use *basic resolution* at 1 minute
    - *High resolution* can go up to 1 second
    - Includes RAM and application level metrics
- CloudWatch Agent forwards metrics and logs from your server to
- CloudWatch Agent has centralized config using Systems Manager (SSM) parameter store
- *Procstat plugin* collect information on individual processes on instance
    - Monitor by PID or RegEx

### Status Checks

- *Status Checks* are automated checks to identify issues
- There are three types of status checks
    - *System Status Checks* monitor problems with AWS hardware that the instance runs on
    - *Instance Status Checks* monitor the software and network configurations of the instance
    - *Attached EBS Status Checks* validate that EBS volumes are mounted to instances and can complete I/O operations
- When status checks fail, recovery can be automated using either CloudWatch alarms, or auto scaling groups
- Status checks have several CloudWatch metrics
    - `StatusCheckFailed_System`
    - `StatusCheckFailed_Instance`
    - `StatusCheckFailed_AttachedEBS`
    - `StatusCheckFailed` (for any)

## Cost

- EC2 purchasing options:
  - On Demand: Short workload, predictable, pay per second
  - Reserved: 1-3 year lease, long workloads, flexible, offers none | partial | all upfront payments
  - Savings Plans: 1-3 year lease, long workloads, commitment to huge amount of usage
  - Spot Instances: Short workloads, cheap, can lose at any time, offer lowestPrice | diversified | capacityOptimized | capacityOptimized fleets.
  - Dedicated Instances: No other customers share hardware
  - Dedicated Hosts: Book entire physical server
  - Capacity Reservations: Reserve capacity in specific AZ for any duration
- Instances are only billed in running state except for reserve instances

## Placement Strategy

- Placement Groups allow for control of EC2 instance placement strategy
- Three types of placement groups: Cluster, Spread, Partition
- Cluster
  - Low latency
  - single AZ
  - If the rack fails, all instances fail
- Spread
  - Spreads across hardware
  - Max 7 instances per group per AZ
  - Used to minimize failure risks and maximize availability
- Partition
  - Spreads across partitions within AZ
  - Up to 7 partitions per AZ
  - Scales to hundreds of instances per group
  - Used for Hadoop, Kafka and Casandra
