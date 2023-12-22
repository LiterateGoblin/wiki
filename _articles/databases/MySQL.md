---
title: MySQL
---
MySQL is a database engine that supports several different [storage engines.](../storage_engine.md?fileId=24631).

## Features

### Binary log

The binary log is a log of events performed on a database. The binary log can then be replayed on the same database instance or another database instance in order to replicate the instance or recover the instance in the event of an emergency or failure. Only write events are added to the binary log. Writing to the binary log is transactional to maintain [ACID compliance](acid_compliance.md?fileId=24665).

 The binary log can be formatted in several ways to increase the accuracy of a replication or recovery, at the expense of taking up more space. This parameter is controlled by the `binlog_format`  parameter and can be the following values:

- `STATEMENT`  - the least log data. This was the original format, and was based on the idea of "replaying" statements onto a replica.
- `MIXED` - usually like statement-based logging, but switches to row-based logging in certain cases.
- `ROW` - the most log data. This is the default option. A log is kept of how each row changed.

## Bundled Tools

- mysqldump - a utility for copying a database from one server to another.

## References

1. <https://dev.mysql.com/doc/refman/8.0/en>
2. <https://explore.skillbuilder.aws/learn/course/8033/play/26697/replication-and-data-assurance-in-mysql>
3. <https://explore.skillbuilder.aws/learn/course/8033/play/26698/migration-to-aurora-mysql>, accessed 2023-11-12
