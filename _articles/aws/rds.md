---
title: Amazon Relational Database Service (RDS)
---
Amazon Relational Database Service (RDS) is a managed database service offered by Amazon. It aims to free up administration time associated with performing common database maintenance tasks by automating them.

## Configuration

RDS offers *parameter groups*, a group of configuration values that gets applied to the database instance. The cluster will use a default parameter group before any custom parameter groups have been created.

RDS instances can be integrated with several storage engines, one of them being [InnoDB](/databases/storage_engine.html).

## Migration

An on-premises server can be migrated to or from by using the *mysqldump* utility. This is a native MySQL utility. A database can be exported from an RDS database by configuring an external database for replication with the source database. Then, once the mysqldump has been imported into the destination database, replication can be disabled.

## Monitoring

### Activity streams

*Activity streams* are near real-time audit logs of activity occurring in an Aurora database. Each event describes either a read or write, called *access* and *change* events respectively. Two kinds of activity stream session modes are available for PostgreSQL - synchronous and asynchronous. The synchronous mode favors durability at the cost of performance, and vice versa for the asynchronous mode. MySQL only has support for asynchronous session modes for activity streams. For security and compliance, database administrators are not recommended to have access to enabling and disabling the activity streams.

### RDS events

*Events* are changes in an environment that are captured by RDS. These are coarser than activity streams. They can signify changes in resources such as proxies, instances, and clusters. RDS events can be integrated with AWS Simple Notification Service (SNS) to send a notification to a person or application.

### Database logs

Database logs can provide a record of what activities have been performed on a database. Logs can be published to CloudWatch, and individual log files can be downloaded from an API that RDS exposes for each database.

### Enhanced Monitoring

Enhanced monitoring can be enabled per database. This kind of monitoring is different from the typical monitoring for two reasons:

- RDS accesses data from CloudWatch Logs in order to determine the values of metrics
- An agent on the instance running the database sends metrics rather than the instance hypervisor

Enhanced monitoring is recommended for investigating how much CPU or memory each individual thread or process uses.

### Amazon RDS Performance Insights

This is a dashboard that is used to monitor database performance in aggregate. Metrics are collected and displayed about the database load and maximum CPU. Database load can be filtered by various dimensions, such as the top SQL query or the number of wait events.

## References

1. <https://explore.skillbuilder.aws/learn/course/8033/play/26693/introduction-to-amazon-aurora-with-mysql>
2. <https://explore.skillbuilder.aws/learn/course/8033/play/26699/mysql-performance-troubleshooting-and-advanced-security-risk>, Accessed 2023-11-21.
3. <https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/DBActivityStreams.Overview.html>, Accessed 2023-11-13
4. <https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Events.Messages.html>, Accessed 2023-11-13
5. <https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/working-with-events.html>, Accessed 2023-11-13
