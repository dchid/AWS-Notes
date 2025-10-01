# CodeBuild

- CodeBuild is a managed service for compiling and building artifacts for an application
- Can user CodeCommit, S3, or 3rd party version control as a source
- Builds can be triggered upon different events such as git push or merge request approvals
- Compute size can be configured depending on RAM and CPU requirements
- Build instructions are configured in a YAML file called buildspec.yml
- Output logs can be stored in either S3 or CloudWatch logs
- EventBridge can be used to trigger actions on failed or canceled builds
- CodeBuild supports several environments:
    - Java
    - Ruby
    - Python
    - Go
    - NodeJS
    - Android
    - .NET Core
    - PHP
- Custom environments can be created using Docker
- Files can be cached between builds using S3
- CodeBuild runs outside of a VPC by default, but can run inside of a VPC to access resources within a VPC
- To run CodeBuild within a VPC, specify the following:
    - VPC ID
    - VPC ID
    - Security Group ID

## buildspec.yml

- The `buildspec.yml` file must be at the root directory of the code repo to work
- env allows the defining of variables that are either:
    - Plaintext
    - Stored in SSM Parameter Store
    - Stored in AWS Secrets Manager
- phases defines what CodeBuild will be doing including
    - install
    - pre_build
    - build
    - post_build
- artifacts defines what to upload to S3 
- cache defines which paths should be cached in S3

## Environment Variables
- Default environment variables are provides and defined by AWS:
    - AWS\_DEFAULT\_REGION
    - CODEBUILD\_BUILD\_ARN
    - CODEBUILD\_BUILD\_ID 
    - CODEBUILD\_BUILD\_IMAGE
- Custom environment variables are user defined
    - Static variables are defined at build time, but can be overridden using a start-build API call
    - Dynamic variables are defined using SSM Parameter Store or Secrets Manager

## Local Builds

- Building locally can be useful for debugging 
- local builds can be run on a desktop using docker
- Use the CodeBuild Agent for local builds

## Testing

- CodeBuild can provide visual test reports
- Test reports support testing frameworks which output in the following formats
    - JUnit XML
    - NUnit XML
    - NUnit3 XML
    - Cucumber JSON
    - TestNG XML
    - Visual Studio TRX
To create a test report, you need to add a Report Group name in buildspec.yml with information about the tests
- *Build Badges* can be accessed using a public URL to dynamically display a build's status
    - Badges are available at the branch level
- CodeCommit can be used to validate a pull request

## Security

- CodeBuild Service Role allows access to AWS resources
- Data is encrypted in transit and at rest
- Artifacts are encrypted using KMS
