---
title: AWS DynamoDB
---
AWS DynamoDB is a NoSQL (non-relational), serverless database service managed by AWS [^1]. DynamoDB supports both document and key-value data models. Items in DynamoDB are stored in rows and have a partition key, and, if configured, a sort key [^2]. These keys are required (if items are configured to have both, otherwise just the partition key is required). Partition keys are used by DynamoDB to partition data across clusters in order to respond to API calls faster (sharding), though when this occurs is managed by AWS and abstracted away from users. Other item attributes may be optionally specified. Items stored in DynamoDB are replicated across at least two solid-state disks in separate AWS Availability Zones. The throughput of a table can be provisioned; a number of read capacity units (RCUs) and write capacity units (WCUs) represents how many multiples of 4 KBs may be read at once and how many KBs (multiples of 1) may be written at once, respectively.

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

## Consistency

DynamoDB supports two consistency models: eventually consistent and strongly consistent [^2]. Eventually consistent read requests can potentially return stale data from an Availability Zone that has yet to have the latest data replicated over. These read requests only consume 0.5 RCUs per 4 KBs or less. Strongly consistent read requests always return the data from latest write, determining the correct Availability Zone replica to read from. Strongly consistent reads have a higher charge associated with them, and can be unavailable during certain data center failure scenarios.

## Supported operations

The following operations are a subset of what can be performed on a DynamoDB table [^2]:

| Name              | Read/Write | *CUs consumed                                                                                         | Description                                                                    |
|-------------------|------------|-------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| GetItem           | Read       | Number of KBs of the item divided by 4 and rounded up to the nearest integer                          | Read an item from the table by primary key.                                    |
| BatchGetItem      | Read       | Number of KBs per item, divided by 4 and rounded up to the nearest integer. Then, all RCUs are summed | Read many items from several tables by primary key.                            |
| Scan              | Read       | Number of KBs per item, divided by 4 and rounded up to the nearest integer. Then, all RCUs are summed | Read all items from the table.                                                 |
| Query             | Read       | Summed number of KBs per item divided by 4 and then rounded up to the nearest integer                 | Read items from the table that fulfill criteria in a query expression.         |
| PutItem           | Write      | Number of KBs of the item rounded up to the nearest integer                                           | Put an item in the table with a unique primary key.                            |
| BatchWriteItem    | Write      | Number of KBs per item rounded up to the nearest integer. Then, all WCU are summed                    | Puts or deletes many items into several tables, each with unique primary keys. |
| UpdateItem        | Write      | Number of KBs of the **entire** item rounded up to the nearest integer                                | Update one or several attributes of an existing item.                          |
| DeleteItem        | Write      | Number of KBs of the item rounded up to the nearest integer                                           | Remove an item from the table.                                                 |

Note that of the read operations, Query is the most effective at conserving RCUs since it only rounds after the amount of data retrieved from each item has already been summed. BatchGetItem and BatchPutItem can operate on one or more tables in a single API call [^3][^8]. Each other API call listed above can operate on only one table at a time [^4][^5][^6][^7][^9][^10].

## Secondary indices

A secondary index created for a DynamoDB table allows a user to query a table on a different partition key and sort key than the base table [^2]. There are two kinds of secondary indices available: local and global.

### Local secondary indices

Local secondary indices (LSIs) allow a user to query the table on a different sort key than the original table, but the partition key must remain the same. LSIs can only be up to 10 GB large, and must be created at the same time as the base table. Each LSI is local to a particular partition key - an LSI needs to be created per partition key if the whole table is to have an LSI. An LSI can serve both eventually consistent and strongly consistent reads. The provisioned RCU and WCU limits are inherited from the base table.

### Global secondary indices

Global secondary indices (GSIs) allow a user to query the table on a different sort key *and* partition key than the original table. GSIs have no maximum space requirement, and be created after the table is already in operation. GSIs are not local to a partition. A GSI can only serve eventually consistent reads. The provisioned RCU and WCU limits are indpendent of the base table. This index can be thought of as a whole separate table from the base table that the base table replicates to.

## DynamoDB Streams

A DynamoDB Stream is a log of events on how each item in a DynamoDB table has changed [^2]. DynamoDB streams are compatible with the AWS Kinesis Streams client library.

## References

[^1]: "Introduction to Amazon DynamoDB for Serverless Architectures." "Amazon DynamoDB for Serverless Architectures." *AWS Skill Builder*, [**explore.skillbuilder.aws/learn/course/67/play/155/amazon-dynamodb-for-serverless-architectures**](https://explore.skillbuilder.aws/learn/course/67/play/155/amazon-dynamodb-for-serverless-architectures). Accessed 24 Dec 2023.
[^2]: "How Amazon DynamoDB Works." "Amazon DynamoDB for Serverless Architectures." *AWS Skill Builder*, [**explore.skillbuilder.aws/learn/course/67/play/155/amazon-dynamodb-for-serverless-architectures**](https://explore.skillbuilder.aws/learn/course/67/play/155/amazon-dynamodb-for-serverless-architectures). Accessed 25 Dec 2023.
[^3]: "BatchGetItem." "Amazon DynamoDB API Reference." [**web.archive.org/web/20231209090549/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_BatchGetItem.html**](https://web.archive.org/web/20231209090549/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_BatchGetItem.html). Archived 9 Dec 2023. Accessed 27 Dec 2023.
[^4]: "GetItem." "Amazon DynamoDB API Reference." [**web.archive.org/web/20231213102140/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_GetItem.html**](https://web.archive.org/web/20231213102140/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_GetItem.html). Archived 13 Dec 2023. Accessed 27 Dec 2023.
[^5]: "Scan." "Amazon DynamoDB API Reference." [**web.archive.org/web/20231214071536/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_Scan.html**](https://web.archive.org/web/20231214071536/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_Scan.html). Archived 14 Dec 2023. Accessed 27 Dec 2023.
[^6]: "Query." "Amazon DynamoDB API Reference." [**web.archive.org/web/20231214071537/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_Query.html**](https://web.archive.org/web/20231214071537/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_Query.html). Archived 14 Dec 2023. Accessed 27 Dec 2023.
[^7]: "PutItem." "Amazon DynamoDB API Reference." [**web.archive.org/web/20231208052254/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_PutItem.html**](https://web.archive.org/web/20231208052254/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_PutItem.html). Archived 08 Dec 2023. Accessed 27 Dec 2023.
[^8]: "BatchWriteItem." "Amazon DynamoDB API Reference." [**web.archive.org/web/20231011130308/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_BatchWriteItem.html**](https://web.archive.org/web/20231011130308/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_BatchWriteItem.html). Archived 11 Oct 2023. Accessed 27 Dec 2023.
[^9]: "UpdateItem." "Amazon DynamoDB API Reference." [**web.archive.org/web/20231208052253/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_UpdateItem.html**](https://web.archive.org/web/20231208052253/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_UpdateItem.html). Archived 08 Dec 2023. Accessed 27 Dec 2023.
[^10]: "DeleteItem." "Amazon DynamoDB API Reference." [**web.archive.org/web/20230928005730/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_DeleteItem.html**](https://web.archive.org/web/20230928005730/https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_DeleteItem.html). Archived 28 Sep 2023. Accessed 27 Dec 2023.
