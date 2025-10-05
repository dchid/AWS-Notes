# EventBridge

---

- EventBridge is service to trigger and schedule scripts and jobs

## Features

- EventBridge can use cron jobs, S3 Event or API call from CloudTrail
- EventBridge generates JSON based triggers
- Trigger Destinations include (but not limited to)
    - Lambda
    - CodeBuild
    - CodePipeline
    - Step Functions
- EventBridge rules are JSON documents that trigger events based on sources and destinations
- The *Default Event Bus* consists of data sources from AWS
- The *Partner Event Bus* consists of AWS SaaS partners
- The *Custom Event Bus* allows custom apps to be event sources
- Events can be archived for replaying
- The *Schema Registry* allows code generation for an application that will know how data is structured in the event bus
    - Schemas can be versioned
- Input transformation allows users to modify the JSON schema for input into a destination
- Resource based policies can manage cross account compatibility
- Content Filtering allows the filtering of events based on certain criteria
    - Prefix Matching
    - Suffix Matching
    - Anything-but Matching
    - Numeric Matching
    - IP Address Matching
    - Equals-ignore-case Matching
    - Complex example with multiple Matching 
    - Complex example with $or Matching
