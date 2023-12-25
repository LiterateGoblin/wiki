---
title: AWS DynamoDB
---
AWS DynamoDB is a NoSQL (non-relational), serverless database service managed by AWS [^1]. DynamoDB supports both document and key-value data models. Items in DynamoDB are stored in rows and have a partition key, and, if configured, a sort key [^2]. These keys are required (if items are configured to have both, otherwise just the partition key is required). Partition keys are used by DynamoDB to partition data across clusters in order to respond to API calls faster (sharding), though when this occurs is managed by AWS and abstracted away from users. Other item attributes may be optionally specified.

## Attributes

### Types

Attributes can be the following types:

- string
- binary (base64 encoded)
- number
- boolean
- null
- set (unordered container type where elements are homogeneous and unique)
- list (ordered container type where elements are heterogeneous)
- map

### Primary keys

A primary key (partition or combined partition and sort key) must be a unique string, number, or binary attribute or complex of attributes.

## References

[^1]: "Introduction to Amazon DynamoDB for Serverless Architectures." "Amazon DynamoDB for Serverless Architectures." *AWS Skill Builder*, [**explore.skillbuilder.aws/learn/course/67/play/155/amazon-dynamodb-for-serverless-architectures**](https://explore.skillbuilder.aws/learn/course/67/play/155/amazon-dynamodb-for-serverless-architectures). Accessed 24 Dec 2023.
[^2]: "How Amazon DynamoDB Works." "Amazon DynamoDB for Serverless Architectures." *AWS Skill Builder*, [**explore.skillbuilder.aws/learn/course/67/play/155/amazon-dynamodb-for-serverless-architectures**](https://explore.skillbuilder.aws/learn/course/67/play/155/amazon-dynamodb-for-serverless-architectures). Accessed 25 Dec 2023.
