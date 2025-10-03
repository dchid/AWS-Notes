# Elastic Container Service

---

- Amazon ECS is a fully managed container orchestration service
- AWS launcher Docker containers by creating *ECS Tasks* on *ECS Clusters*

## Task Definitions

- An ECS *Task Definition* is a JSON document that describes parameters for one or more containers in an application
- Some parameters in a task definition include:
    - Docker image
    - Compute resources allocation per task or container
    - memory and CPU requirements
    - OS of the container
    - Docker networking mode
    - Logging config
    - Whether the task continues the container finishes or fails
    - Commands to run on container start
    - data volumes
    - IAM role
- An *ECS Task* is a running instance of a task definition

## Clusters

- An *ECS Cluster* is a logical grouping of of tasks and services which provide capacity for ECS tasks
- When using ECS with EC2, a cluster will contain one or more EC2 instances

## Launch Types

- ECS can luanch containers either:
    - in EC2 instances managed by the user
    - in AWS Fargate (serverless) managed by AWS

### EC2 Launch Type

- The *ECS agent* agent can be installed on a EC2 instance to associate it with an ECS cluster
- ECS automates starting and stopping docker containers on EC2 instances within an ECS cluster
- An ECS instance profile give the ECS agent on EC2 instance permissions to make calls to ECS, ECR, and CloudWatch

### Fargate Launch Type

- Fargate can be used to launch Docker containers in a serverless environment
- When launching container in Fargate AWS will allocate compute resources based on the task definition

## Load Balancing

- ALBs are recommended for load balancing ECR in most situations
- NLBs are recommended for ECS tasks with high throughput or performance requirements, or pairing with AWS Private Link
- Classic load balancers are not recommended

## Autoscaling

- There are three metrics which can be autoscaled for ECS:
    - CPU
    - RAM
    - ALB request count per target
- *Target Tracking* scales based on a specific CloudWatch metric
- *Step Scaling* scales based on CloudWatch alarms
- *Scheduled Scaling* scales based on a specific date/time
- Scaling ECS at a task level is **not** the same as scaling EC2 instances
- *ECS Cluster Capacity Provider* is used to autoscale infrastructure for ECS tasks pared with an ASG
    - This is preferred over using an ASG to add more EC2 instances to an ECS cluster

## Storage

- EFS can be used to mount NFS file volumes to multiple ECS tasks
- EFS volumes can be used with both the EC2 and Fargate launch types
- S3 is **not** supported as a storage type

## Logging

- Logs generated in an ECS container can be sent to CloudWatch logs or Splunk
    - To do this on EC2, you need to run the `awslogs` driver and configure `logConfiguration` in task definitions
    - Using the Fargate launch type, the task definition requires certain permissions
    - Using the Cloudwatch agent and ECS agent to forward logs can save space on EBS volumes
    - Enable logging in `ECS_AVAILABLE_LOGGING_DRIVERS` in `/etc/ecs/ecs.config`
- Logging with a sidecar container is when a separate container is used to process logs in a cluster 
