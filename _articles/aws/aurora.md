---
title: Amazon Aurora
---
Amazon Aurora is a fully managed database service and engine offered by Amazon. It is built on top of [Amazon RDS](/aws/rds.html). It aims to alleviate the burden of designing architecture for scalability, availability, durability, or reliability by automating them in addition to the maintenance automation provided by RDS. Configuration changes are applied to a cluster as opposed to an individual database instance. Aurora is capable of integrating with other AWS security services. It is compatible with [MySQL](/databases/mysql.html) or PostgreSQL, depending on configuration.

The total data that can be stored in one Aurora database instance is capped at 128 TiB.

Amazon Aurora supports MySQL versions up to 5.7. Thus, Amazon Aurora does not support [data dictionaries](/databases/data_dictionary.html).

Aurora instances can use [AWS DMS](/aws/dms.html) for database migration operations.

## Architecture

The design of Aurora can be described as three subsystems called "layers": the application layer, the compute layer, and the storage layer. The storage layer uses a solid state volume, and manages the cluster capacity auto-scaling. The application layer exposes the data for consumption, and includes the AWS RDS Proxy feature. This layer manages authentication and authorization of data consumers. The compute layer manages the database engine and database features such as partitioning and replication.

## Replication

Data written to an Aurora cluster can be replicated across Availability Zones and across regions; a cluster replicated across regions is known as an *Aurora global database*. This is designed to minimize the amount of data that is lost as a result of a major incident, and the amount of time the system takes to recover. Write operations can be forwarded to the master server, while read operations will operate on the nearest read replica. Multiple writers can also be made available by selecting the multi-master configuration option. An Aurora instance can target up to five secondary read-only regions.

All Aurora clusters have their data replicated across six times across at least three Availability Zones. Each zone contains two copies.

Another strategy to increase availability in MySQL-compatible Aurora instances is to enable binary log-based replication to secondary clusters.

## Serverless v1

Amazon Aurora Serverless v1 is a feature of an Aurora cluster that allows compute for the cluster to be provisioned on-demand. As usage of the cluster grows or shrink, the total provisioned memory and processing will scale up or down. During periods when the cluster is being used at all, all compute will pause. This is intended to serve intermittent, unpredictable, or infrequent workloads.

Serverless v1 clusters cannot be global. They also do not support the creation of activity streams.

## Configuration

Like RDS, Amazon Aurora supports parameter groups. Unlike RDS, these parameter groups can be applied at the cluster level rather than the instance level, and a group can include cluster parameters.

Each cluster is deployed into an Amazon Virtual Private Cloud (VPC). Once a cluster has been deployed to a VPC, it cannot be changed.

The only storage engine supported by Aurora with MySQL is InnoDB.

## Backup

When restoring a backup from an external MySQL server, Aurora will not support included stored procedures, triggers, events, or functions.

Aurora supports two kinds of recovery from a backup: point in time recovery and backtracking.

### Point in time recovery

An Aurora cluster can be configured to continuously backup data. The retention period can be anywhere from 0 to 35 days. A backup can be created for any arbitrary point in time if performed manually.

### Backtracking

Backtracking undoes some or all of the operations that occurred in the last 72 hours. This may be useful for undoing mistakes quickly, such as a DELETE. This is not an adequate substitute for creating point in time backups because of the limitations of the backtracking feature.

A table or database in a cluster can only be backtracked if backtracking was enabled on creation or if backtracking was enabled before the operation the operator intends to undo.

## Security

Access control and authorization can be managed in Aurora using [IAM](/aws/iam.html) users, groups, and roles in addition to native MySQL access control. Network access can be controlled using AWS security groups. Data can be ensured to be encrypted in-transit by requiring secure transport - an Aurora instance is initialized with a certificate.

## Monitoring

In addition to all of the monitoring tools offered by RDS, Aurora offers Aurora recommendations.

### Aurora Recommendations

## References

1. <https://explore.skillbuilder.aws/learn/course/8033/play/26693/introduction-to-amazon-aurora-with-mysql>
2. <https://explore.skillbuilder.aws/learn/course/8033/play/26694/understanding-mysql>
3. <https://explore.skillbuilder.aws/learn/course/8033/play/26698/migration-to-aurora-mysql>, Accessed 2023-11-12.
4. <https://explore.skillbuilder.aws/learn/course/8033/play/26699/mysql-performance-troubleshooting-and-advanced-security-risk>, Accessed 2023-11-13.
