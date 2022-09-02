---
id: epyc3f2p2ubjv73p2xw84nr
title: Special Relational Operators
desc: ''
updated: 1661412070698
created: 1661411701428
---
Includes `LIKE`, `RLIKE`, and `IN`

## Usage of `LIKE` and `RLIKE`
```
source like pattern;
source rlike pattern;
```
- source and patter can only be of the `STRING` type.
- other types can neither be involved in the opertations nor be implicitly converted to the `STRING` type.

## Usage of `IN`

`key in (value1, value2, …)`

- Data in the value column must be consistent.
- To compare keys and values
    - if `BIGINT`, `DOUBLE`, and `STRING` types are compared
        - convert to `DOUBLE`
    - If `DATETIME` and `STRING` types are compared
        - convert to `DATETIME`