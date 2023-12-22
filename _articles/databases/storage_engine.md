---
title: Storage Engine
---
A storage engine handles the storage of storage of table data to memory or disk. MySQL generally supports nine different kinds of storage engine.

## InnoDB

InnoDB is a storage engine compatible with the MySQL database engine. InnoDB supports point in time recovery, asynchronous reads, and predictive storage of result sets into a memory buffer (read-ahead). It also supports a *doublewrite buffer technique*, where data is first written to an in-memory buffer called the *doublewrite buffer.* Once the buffer has been finished being written to, InnoDB writes the data to the appropriate data files on the mounted storage volume (filesystem).

## MyISAM

MyISAM supports high-speed writing and reading operations on **non-transactional tables.** This database engine was the first database engine that MySQL was compatible with. Due to the restriction against transactional tables, this database engine is not [ACID compliant](acid_compliance.md?fileId=24665) and can cause data loss or corruption in the event of a crash.

## References

<https://explore.skillbuilder.aws/learn/course/8033/play/26694/understanding-mysql>

<https://explore.skillbuilder.aws/learn/course/8033/play/26695/mysql-storage-processing-and-backup-and-recovery>
