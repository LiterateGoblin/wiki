---
title: AWS Database Migration Service (DMS)
---
AWS Database Migration Service (DMS) is a service that can be used to migrate a database from [AWS RDS](/aws/rds.html) to an on-premises database, an on-premises database to an AWS RDS database, or an AWS RDS database to another AWS RDS database. DMS is typically employed when native database migration utilities are incompatible with an on-premises database server. DMS can perform *heterogenous* migrations, where the target database engine differs from the source database engine (such as migrating MySQL to PostgreSQL).

## Concept

Database migration with strictly minimal downtime requirements typically consist of two phases:

1. Creating a dump of the database's contents at some point in time. The database remains up.
2. Loading the database dump into the destination database, then using database binary log replication to catch up the destination database with the changes that have been made on the source database since the dump.

DMS handles both of these phases. The first phase is known as a *physical* migration, while the second phase is known as a *logical* migration.

## Components

- replication instance - an AWS EC2 instance that runs one or several migration tasks.
- endpoints (source and target) - contains the information necessary for a migration task to read or write data from a data store. These attributes can include the type (source or target), engine type, server name, port, encryption, and credentials.
- replication tasks -  each task reads data from the source endpoint and writes data to the target endpoint.

## References

<https://explore.skillbuilder.aws/learn/course/8033/play/26698/migration-to-aurora-mysql>, Accessed 2023-11-12
