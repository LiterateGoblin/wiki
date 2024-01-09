---
title: Amazon ElastiCache
---

Amazon ElastiCache is a service for managing the open-source memory data stores [Redis](/wiki/redis.html) and [Memcached](/wiki/memcached.html) [^1]. These services can be used for boosting application or database performance. ElastiCache manages clusters of instances running the data store of a user's choice, and automatically adjusts instance size or number of instances in the cluster depending on traffic.

Data written to an ElastiCache server is stored in the server's primary memory (DRAM) [^2]. An ElastiCache server is often placed "in-between" the application and a database. When the application needs some data, it makes a request to the ElastiCache server rather than the database directly. If the data is stored on the ElastiCache server (called a cache hit) it is returned in the request. If the data could not be found on the ElastiCache server (cache miss), the request is forwarded to the database instead and returned to the requesting application while simultaneously being written to the cache.

Depending on traffic, ElastiCache can adjust the number of instances or the size of instances running in a particular cluster [^1]. More granularly, it can also manage the number of write shards and read replicas available in the cluster.

ElastiCache is capable with integrating with AWS Simple Notification Service (SNS) where it will push notifications that are consumed and potentially trigger events [^2]. Instances will be placed in a subnet within an AWS Virtual Private Cloud (VPC), and can be secured by being placed in a private subnet. For additional security, a Security Group can be placed around the ElastiCache Redis instances that define which IP addresses are allowed to ingress the instances and on which ports.

## Redis

ElastiCache can run Redis in two modes: non-clustered and clustered mode [^2]. Both modes are capable of storing snapshots of the Redis keyspace in an S3 bucket; this snapshot can be restored by ElastiCache. Additionally, both modes support encryption in transit using the TLS protocol and encryption at rest.

### Non-clustered mode

In non-clustered mode, a primary instance that can be both read and written to is supported by some number of replica instances that can only be read from (up to 5) [^2]. The instances can be distributed across subnets in different AWS Availability Zones for higher reliability. Automatic failover can be enabled on these instances - in the event of a failure of the primary instance, a read replica will be promoted to the primary instance. Only one primary instance can exist in the non-clustered mode. Two endpoints are created: one with both the capability of reading and writing, and one that can only be read from.

### Clustered mode

In the clustered mode for ElastiCache Redis, load is distributed across *shards* - groups of read replicas all replicating from a primary instance [^2]. In this mode, multiple primary instances can be created with up to 5 read replicas. These shards do not share all the same data, and a cluster-aware client library is recommended for use by AWS when using ElastiCache in clustered mode. A read replica within a shard can be promoted to the primary instance should the primary instance of that shard fail. One endpoint is created that is used to read, write, and report how many shards there are in the cluster.

## Memcached

ElastiCache can run Memcached nodes in a similar manner to Redis [^2]. All nodes are accessed using a single endpoint for reading, writing, and reporting how many nodes there are in the cluster.

## References

[^1]: "Introduction to Amazon ElastiCache." "Getting Started with Amzaon ElastiCache." *AWS Skill Builder*, [**explore.skillbuilder.aws/learn/course/14572/play/98126/amazon-elasticache-getting-started**](https://explore.skillbuilder.aws/learn/course/14572/play/98126/amazon-elasticache-getting-started). Accessed 1 Jan 2024.
[^2]: "Architecture and Use Cases." "Getting Started with Amzaon ElastiCache." *AWS Skill Builder*, [**explore.skillbuilder.aws/learn/course/14572/play/98126/amazon-elasticache-getting-started**](https://explore.skillbuilder.aws/learn/course/14572/play/98126/amazon-elasticache-getting-started). Accessed 1 Jan 2024.
