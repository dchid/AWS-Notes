# Elastic Kubernetes Service

---

- Amazon EKS is a managed Kubernetes service for AWS

## K8s

- K8s pods are organised into nodes
- Pods exist in autoscaling groups

## Node Types

### Managed Node Groups

- Creates and manages EC2 instances for you
- Nodes are part of an ASG managed by EKS
- Supports on-demand or spot instances

### Self-Managed Nodes

- User created nodes registered to an EKS cluster and managed by an ASG
- Compatible with pre-built AMIs and EKS optimized AMI
- Supports on-demand or spot instances

### Fargate

- Pods run in a serverless, managed environment

## Storage

- To mount a volume to an EKS cluster a *StorageClass* manifest needs to be specified
- This leverages a *Container Storage Interface (CSI)* compliant driver
- Supports four storage types
    - EBS
    - EFS (Fargate only)
    - FSx for Lustre
    - FSx for NetApp ONTAP

## Logging

- Logging in CloudWatch logs can be enabled for EKS Control Plane with several log types
    - api
    - audit
    - authenticator
    - controllerManager
    - scheduler
- Nodes and container metrics are forwarded using the CloudWatch Agent
- Nodes and container logs are forwarded using the `Fluent Bit` or `Fluentd` drivers
Container logs are streamed to CloudWatch from `/var/log/containers`
