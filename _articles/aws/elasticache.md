---
title: Amazon ElastiCache
---

Amazon Elasticache is a service for managing the open-source memory data stores [Redis](/wiki/redis.html) and [Memcached](/wiki/memcached.html) [^1]. These services are often used for boosting application or database performance. Elasticache manages clusters of instances running the data store of a user's choice, and automatically adjusts instance size or number of instances in the cluster depending on traffic.

## Auto-scaling

Depending on traffic, Elasticache can adjust the number of instances or the size of instances running in a particular cluster [^1]. More granularly, it can also manage the number of write shards and read replicas available in the cluster.

## References

[^1]: "Introduction to Amazon Elasticache." "Getting Started with Amzaon ElastiCache." *AWS Skill Builder*, [**explore.skillbuilder.aws/learn/course/14572/play/98126/amazon-elasticache-getting-started**](https://explore.skillbuilder.aws/learn/course/14572/play/98126/amazon-elasticache-getting-started). Accessed 1 Jan 2024.
