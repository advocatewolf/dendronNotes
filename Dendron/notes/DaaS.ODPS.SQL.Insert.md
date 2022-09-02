---
id: 6dpe5dv0rbodpbo08hfus0m
title: Insert Operation
desc: ''
updated: 1661418986336
created: 1661405551162
---
## Insert Overwrite/Into
- `insert into`
: inserts added data into the table or partition
- `insert overwrite`
: clears source data from the table or partition before inserting data

## Dynamic Partition
- Statement Format

`insert overwrite table tablename partition (partcol1, partcol2 ...) select_statement from from_statement;`

### Notes:
- `select_statement` field, the following field provides a dynamic partition value for the target table.
    - if the target table has only one-level dynamic partition, the last field value of `select_statement` is the dynamic partition value of the target table.
- a single worker can only output up to **512 dynamic partitions** in a distributed environment, otherwise it leads to abnormality.
- dynamic partition SQL cannot generate more than 2000 dynamic partitions; causes abnormality.
- value of dynamic partition cannot be **NULL**
    - also does not support special or **Chinese** characters; exception is thrown:
    
    `FAILED: ODPS-0123031:Partition exception - invalid dynamic partition value:province=xxx`
- if destination table has multi-level partitions
    - allowed to specify parts of partitions to be static partitions through `insert` statement
    - static partitions must be advanced partitions.

### `odps.sql.reshuffle.dynamicpt=true/false`
- dynamic partition can cause some scenarios to slow down, closing can speed up SQL.
- if dynamic partition value is very small, closing the data will not skew.
