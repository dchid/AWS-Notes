# ECR

---

- *Elastic Container Registry* is a registry to store and manage Docker images on AWS

## Features

- ECR supports both public and private repos
- ECR is fully integrated with ECS and backed by S3
- Supports image vulnerability scanning, versioning, image tags
- ECR images are good for providing dependencies for code build

## Lifecycle Policies

- The lifespan of ECR images can be managed by *Lifecycle Policies*
- Lifecycle policies are written in JSON
- Images can be retired based on the age of the image in days or keeping only one untagged image and expiring all others
- Each policy contains one or more rules which are evaluated simultaneously and applied on priority
- Images are expired 24 hours after meeting the criteria
- Retiring images helps reduce storage costs

