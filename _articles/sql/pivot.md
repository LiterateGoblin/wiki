---
title: Pivot
---
Pivoting is an operation where each record (row) in a result set is transformed such that it becomes a column in the output [^1]. Un-pivoting is the opposite operation: each column is made into its own record.

## Example

Consider the following table with information on pets:

| Name    | Species | Caretaker | Total Vet Visits |
|---------|---------|-----------|------------------|
| Andy    | Rat     | Brian     | 3                |
| Ghost   | Wolf    | Jon       | 0                |
| Minerva | Cat     | Harry     | 1                |

If the total vet visits column is selected and pivoted, the resulting record is the number of vet visits per pet (column names added as a separate part of the query).

| Andy | Ghost | Minerva |
|------|-------|---------|
| 3    | 0     | 1       |

## References

[^1]: "PIVOT and UNPIVOT examples." "Amazon Redshift Database Developer Guide." [**web.archive.org/web/20230401023956/https://docs.aws.amazon.com/redshift/latest/dg/r_FROM_clause-pivot-unpivot-examples.html**](https://web.archive.org/web/20230401023956/https://docs.aws.amazon.com/redshift/latest/dg/r_FROM_clause-pivot-unpivot-examples.html). Archived 1 Apr 2023. Accessed 28 Dec 2023.
