# Elastic Beanstalk

- Elastic Beanstalk is a managed service which automates deploying of all components for an application via CloudFormation
- Elastic Beanstalk has several components:
    - *Application*: The collection of components such as environments, versions, and configurations
    - *Application Version*: an iteration of code
    - *Environment* (dev, test, prod)
- Elastic Beanstalk supports several programming languages and runtimes
    - Golang
    - Java
    - C#
    - Powershell
    - NodeJS
    - PHP
    - Python
    - Ruby
    - Packer Builder
    - Docker
    - Custom Platforms
- Elastic Beanstalk has a single instance deployment mode designed for dev/test environments and a high availability mode designed for prod
- Elastic Beanstalk supports web server and worker environments
    - Web server tier is the traditional model with traffic and ELB routing traffic to EC2 instances in an autoscaling group
    - The worker tier model has traffic routed by an SQS queue to the autoscaling group via SQS messages
- Workers are ideal for longer tasks
- There are two deployment modes:
- *Single Instance* is ideal for dev environments
- *High Availability* is good for prod environments
- The service itself is free, but the resources provisioned are charged to the user
- Elastic Beanstalk automatically handles load balancing, scaling, monitoring and configuration
- When an RDS instance is linked to a beanstalk deployment, deleting the beanstalk app will delete the db as well

## Deployment Options for Updates

- There are several ways to update a beanstalk deployment:
    - *All at once*: Fastest deployment with no aditional cost, but with downtime
    - *Rolling*: Update a few at a time in a group called a *bucket* and move onto the next bucket after successful healthchecks
    - *Rolling with additional batches*: Spins up new instances and switches once they're healthy (old app still available)
    - *Immutable*: Deploy completely new instances
    - *Blue Green*: Create a new environment and switch over
    - *Traffic Splitting*: Send a small percentage to the new deployment (Canary Testing)

| Deployment Type | Deployment Time | Cost | Deployed Instances | Impact of Deployment Failure |
|-----------------|-----------------|------|--------------------|------------------------------|
| All at Once     | Lowest          | $    | Existing           | Downtime                     |
| Rolling         | Medium          | $$   | Existing           | Single batch out of service  |
| Rolling Batches | High            | $$$  | New and Existing   | Minimal if first batch fails |
| Immutable       | Highest         | $$$$ | New                | Minimal                      |
| Blue Green      | Highest         | $$$$ | New                | New version traffic impacted |
| Traffic Split   | Highest         | $$$$ | New                | Minimal                      |
