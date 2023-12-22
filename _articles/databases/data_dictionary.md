---
title: Data Dictionary
---
A data dictionary is a meta-table that stores information about other database tables and their fields. Because it is a table, it can be transacted upon and queried just like any other table.

Data dictionaries became available in MySQL in version 8.0, and are also available in recent versions of PostgreSQL.

## Usage

Internally, the data dictionary is used to validate field names referenced in incoming queries. Externally, database users can query the `INFORMATION_SCHEMA` to learn more about a particular table or its fields - this table is a view of the data dictionaries.

## Drawbacks

Operating a table's schema, such as by adding fields or removing fields, takes longer when data dictionaries are used as opposed to metadata files.
