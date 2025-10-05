# Autoscaling

---

- Autoscaling groups automate horizontal scaling
- ASGs have a minimum, desired, and maximum capacity
- LBs can forward health checks to ASGs which can then replace unhealthy instances

## Launch Templates

- ASGs use a launch template containing:
    - AMI and instance type
    - EC2 user data
    - EBS Volumes
    - Security Groups
    - SSH heys
    - IAN roles for instances
    - Network and subnet information
    - Load Balancer information
- Launch templates are newer compared to launch configurations, which did not support versioning

## Scaling Policies

- ASGs use scaling policies based on CloudWatch metrics and alarms
- During a cool down period (default 300 seconds) the ASG won't terminate or launch instances

### Types of Policies

- *Dynamic Scaling* is for unpredictable patterns
    - *Target Tracking Scaling* is the easiest to set up and is based on average usage
    - *Simple/Step Scaling* is based on CloudWatch alarms
- *Scheduled Actions* anticipates scaling based on known usage patterns
- *Predictive Scaling* creates predictive models over time using ML models

## Lifecycle Hooks

- ASG Lifecycle Hooks allow running start-up or shutdown scripts for instances in between pending and in-service states
- Lifecycle hooks cab be used for cleanup during EC2 terminated state, or perform health checks during a 
- Lifecycle Hooks integrate with EventBridge, SNS, and SQS
- ASG have three health checks available:
    - EC2 Status Checks
    - ELB Health Checks
    - Custom Health Checks (send instances health using CLI or SDK)
- Autoscaling CLI can use the `set-instance-health` option for custom health checks or `terminate-instance-in-autoscaling-group` to terminate instances

## Termination Policies

- *Termination Policies* determine which instances to terminate first during scale in events
- The default termination policy:
    - Selects AZs with more instances
    - Terminates instance with oldest launch template or launch configuration
    - If instances were launched using the same launch template, terminate the instance that is closest to the next billing hour
- Other termination policies include:
    - `AllocationStrategy` aligns with an allocation strategy (e.g. lowest price for spot instances or lower priority on-demand instances)
    - `OldestLaunchTemplate` terminates instances with the oldest launch template
    - `OldestLaunchConfiguration` terminates instances with the oldest launch configuration
    - `ClosestToNextInstanceHour` terminates instances closest to the next billing hour
    - `NewestInstance` terminated newest instance (good for testing)
    - `OldestInstance` terminates oldest instance
- You can use one or more termination policies and specify an evaluation order
- You can define custom termination policies based on a Lambda function

## Metrics

- CloudWatch metrics for ASG are collected every minute
- ASG level metrics (opt in) include:
    - Min, Max, desired capacity
    - In-service, pending, stand-by instances
    - `GroupTerminatingInstances`
    - `GroupTotalnstances`
- EC2 level metrics (enabled and collected at either 1 or 5 minute intervals)
    - `CPUUtilization`
    - `RequestCountPerTarget`

## Notifications

- ASG supports SMS notifications using the following events
    - `EC2_INSTANCE_LAUNCH`
    - `EC2_INSTANCE_LAUNCH_ERROR`
    - `EC2_INSTANCE_TERMINATE`
    - `EC2_INSTANCE_TERMINATE_ERROR`
- ASG supports EventBridge to get more detailed events from EC2

## Warm Pools

- *Warm Pools* are groups of pre-initialized instances to reduce scale out latency
- Instances in the warm pool are moved into the ASG during scale out events
- Warm pools require the use of Lifecycle hooks
- Warm pools have several settings
    - Minimum, maximum, and preferred number of instances in the warn pool
    - Warm pool instance state is the state to keep instances in the warm pool (Running, Stopped, or Hibernated)
- Instances in warm pools don't effect ASG metrics until they are moved into the ASG
- An *Instance Reuse Policy* moves instances back into the warm pool during scale in events instead of terminating the instance

## Application Autoscaling

- Monitors your apps and automatically optimizes capacity
- Point to a selected app and select the services to be scaled
- Search for resources using CloudFormation Stacks, tags, EC2 ASG
- Build *Scaling Plans* to automatically add or remove capacity from resources
- Supports, Target Tracking, Step, and Scheduled Scaling Policies

