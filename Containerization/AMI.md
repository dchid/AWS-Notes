# AMI

- An *AMI* is a machine image created for customizing EC2 instances
- AMIs are created from EBS Snapshots
- AMIs created from encrypted snapshots will require keys to be used
- The no reboot option allows creation of an AMI without shutting down an instance
- IAM policies can be used to restrict users to only use certain AMIs

## EC2 Image Builder
- *EC2 Image Builder* can automate the creation, maintenance, and testing for AMIs
- EC2 Image Builder can run on a schedule to update AMIs
- Image Builder starts with an ultra minimal *Builder EC2 Instance* and then adds dependencies, then runs tests on a *Test EC2 Instance* before deploying the AMI
- Uses AWS CodePipeline with CodeCommit, CodeBuild, and CloudFormation to build AMIs
- Image Builder uses *Resource Access Manager* to share AMIs across multiple regions or accounts
