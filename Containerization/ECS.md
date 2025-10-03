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

### Fargate Launch Type

- When launching container in Fargate AWS will allocate compute resources based on the task definition
