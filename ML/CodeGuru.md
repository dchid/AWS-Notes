# Code Guru

- *CodeGuru reviewer* automates static code analysis and reviews
- *CodeGuru Profiler* analyses performance during runtime

# Reviewer

- The reviewer analyzes commits and tries to detect vulnerabilities, bugs, and potential optimizations
- Supports Java and Python
- Supports Guthub, BitBucket, and CodeCommit
- The reviewer can detect hard coded secrets such as API keys, SSH keys and credentials, and automatically move those secrets to AWS Secrets Manager

# Profiler

- The profiler detects the most CPU intensive parts of a program through a logging routine
- The profiler can provide a heap summary for memory optimization
- Supports on premise applications
- Can integrate with Lambda functions by (either or):
    - using a decorator `@with_lambda_profiler` with the `codeguru_profiler_agent` added as a lambda layer
    - Enabling Profiling in the function config
