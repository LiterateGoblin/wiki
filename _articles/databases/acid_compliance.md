---
title: ACID
---
ACID is a model that specifies the criteria that need to be met by a read-write system to ensure the ability for *transactions* to occur. Transactions differ from ordinary writes by meeting the following criteria. The criteria are:

- **A** - atomic. Each operation either finishes completely, or fails without making any change. An operation cannot be left in a partial or midway state.
- **CI -** consistency and isolation. Operations occurring at the same time cannot affect each other. For example, a read operation and write operation occurring at the same time will cause the read operation to either read the old data or the new data, not a mix of both.
- **D** \- durability. The results of a write operation are safe from data loss or corruption from a power outage or other incident. If a write operation fails midway, the whole operation is rolled back.

## References

<https://explore.skillbuilder.aws/learn/course/8033/play/26695/mysql-storage-processing-and-backup-and-recovery>
