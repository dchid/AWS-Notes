# CodeDeploy

- *CodeDeploy* is a managed continous deployment service
- Supports automated rollback and gradual deplpoyment control
- Deployments are configured by a YAML file called `appspec.yml`
- CodeDeploy can deploy to EC2 and on premise servers
- There are three deployment speeds
	- AllAtOnce
	- HalfAtATime
	- OneAtATime
	- Custom
- A *Blue/Green Deployment* is a deployment where two sets of servers host two different software versions: a stable old (blue) version, and a new updated (green) version being deployed
- Blue/Green Deployments need a load balancer to route traffic to either a blue or green autoscaling group
- CodeDeploy agent requires sufficient S3 permissions attached to the EC2 instance to get deployment bundles from S3
- CodeDeploy can help automate traffic shifts between lambda aliases which can be used to shift traffic from old versions to new versions of a lambda function
- CodeDeploy can publish notifications to SNS during deployment success, deployment failure, or instance failure
- There are a three ways to shift versions for lambda:
    - **Linear**: grow traffic by 10% every N minutes until 100% (N set to either 3 or 10)
    - **Canary**: grow traffic by X percent, then 100% (after 5 or 30 minuts)
    - **All at Once**

## Redeploy and Rollbacks

- Rollbacks can occur automatically or manually
- Automatic rollbacks can occur when a WloudWatch alarm is triggered or when a deployment fails
- Rollbacks can be disabled
- If there is a date and time error between and EC2 instance and an AWS service, then the error `InvalidSignatureException` will occur
- Sometimes errors will occur when too few instances in deployment groups pass health checks or the deployment failed on too many instances
- Ensure that the CodeDeploy Agent is installed and running when needed, and that the CodeDeploy Service Role or IAM instance profile has appropriate permissions
- CodeDeploy failures can be intercepted using EventBridge
- If a deployment ASG is underway and a scale out event occurs the new instances will be updated with the version most recently deployed (not the application that's currently being deployed)
    - When this happens, CodeDeploy will automatically update the out of date instances

## EC2 Integration

- The *CodeDeploy Agent* is installed on EC2 and on-premise servers to run CodeDeploy as a service
- Use either EC2 tags (Manual Deployment) or autoscaling groups (Automatic Deployment) to determine which servers to deploy to
- *Deployment Hooks* are one or more scripts run during the update lifecycle
- Deployment Hooks have the following stages
    1. BeforeBlockTraffic
    2. BlockTraffic
    3. AfterBlockTraffoc
    4. ApplicationStop
    5. DownloadBundle
    6. BeforeInstall
    7. AfterInstall
    8. ApplicationStart
    9. ValidateService
    10. BeforeAllowTraffic
    11. AllowTraffic
    12. AfterAllowTraffic
- The first three and last three steps are only run when using a load balancer
- Scripts can be run during any of these stages except BlockTraffic, DownloadBundle, Install, and AllowTraffic as these steps are reserved by CodeDeploy.
- apspec.yml file defines which scripts run during each step of deployment
- During a blue/green deployment, old instances can be automatically terminated, or kept running but deregistered from the ELB and autscaling group
    - Default termination time is after 1 hour, maximum after two days

## ECS Integration

- CodeDeploy can automate the deployment of a new ECS task definition for blue/green using linear, canary, or all at once
- The service must be connected to a load balancer and must already be created
- The ECS task revision and the load balancer info are placed in the `appspec.yml` file
- CodePipeline can be used to automate the entire deployment of a new ECS definition

## Lambda Integration

- CodeDeploy can be used to create a new version of a lambda function and reference it with an alias
- The `appspec.yml` file requires:
    - Name
    - Alias
    - CurrentVersion
    - TargetVersion
- The deployment hooks for Lambda are:
    - BeforeAllowTraffic
    - AllowTraffic
    - AfterAllowTraffic
- Lambda functions for the deployment may not be run during the AllowTraffic stage
