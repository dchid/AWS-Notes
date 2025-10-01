# CodeArtifact

- Storing and retrieving software dependencies is called *artifact management*
- CodeArtifact is a scalable artifact management service
- Has integration with common package management and build tools such as:
    - Maven
    - Gradle
    - npm
    - yarn
    - twine
    - pip
    - NuGet
- Both developers and CodeBuild can retrieve dependencies straight from CodeArtifact
- CodeArtifact acts as a proxy to public artifact repos like NPM which enables caching
- CodeArtifact is integrated with CodeBuild and CodePipeline
- External access to CodeArtifact can be managed using a resource policy
    - This can restrict access to a specific packages

## Upstream Repositories

- CodeArtifact repos can use other CodeArtifact repos as upstream repositories
- External Connections are connections between a CodeArtifact repo and a public repository
- Packages are not cached in intermediate repositories
- CodeArtifact *Domains* are common storage for dependencies that span across multiple accounts
- Domains have all assets and metadata encrypted with one KMS key
