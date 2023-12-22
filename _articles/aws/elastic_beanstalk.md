---
title: AWS Elastic Beanstalk
---
AWS Elastic Beanstalk is an AWS service that allows users to deploy applications without needing to know about the underlying infrastructure of that application.

## Environment Types

### Web Server Environment

This environment is intended for processes that serve HTTPS traffic and are not compute intensive.

### Worker Environment

This environment is intended for processes that are long-running and compute intensive, such as processing images and video.

## Capabilities

### Load balancing and auto-scaling

### Configuration and update management

### Application monitoring

### Security

Elastic Beanstalk integrates with [AWS Identity and Access Management (IAM)](/aws/iam.html) to ensure that the actions that the service takes are only those that are defined in a permissions policy.

## Supported Runtimes

AWS Elastic Beanstalk can accept code bundles written for the following runtimes:

- Python
- Java
- PHP
- Ruby
- Go
- .NET
- Node.js
