# Service Catalog

- *AWS Service Catalogue* is a portal which lets users launch a set of resources (using CloudFormation Templates) authorized by admins
- CloudFormation Templates are referred to as *Products*, and collections of Products are called *Portfolios*
- Manage tags on products using *TagOptions*
- Service Catalog is a good tool to provide self service resource provisioning with minimal privileges
- Can integrate with self service catalogs such as Service Now
- *Stack Set Constraints* allow for the configuring of product deployment using CloudFormation StackSets
- StackSet Constraints can restrict by:
    - Accounts
    - Regions
    - Permissions
- *Launch Constraints* are IAM roles with full CloudFormation permissions that allow users of service catalog to provision resources that they would otherwise lack the permissions for
- Launch Constraints require an S3 bucket to store the templates.
- Service Catalog supports version control
- Available products in a catalog are defined by a file called `mapping.yml` which maps products to CF templates
- Lambda functions can be used to deploy changes to service catalog from git
