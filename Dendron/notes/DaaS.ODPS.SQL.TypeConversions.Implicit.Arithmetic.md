---
id: 45179fty8ut7dy68z945u4i
title: Arithmetic Operators
desc: ''
updated: 1661412435010
created: 1661412094995
---
## Implicit conversions under arithmetic operators

Arithmetic |
-----------|
addition (+) |
subtraction (-) |
multiplication (*) |
division (/) |
modulo (%) |
unary plus (+) |
and unary minus (-) |

### Implicit Conversion Rules
- Only `STRING`, `BIGINT`, `DOUBLE`, and `DECIMAL` types can be involved in the operation
- `STRING` type are implicitly converted to `DOUBLE` type before the operation
- When `BIGINT` and `DOUBLE` Types are involved, `BIGINT` is implicitly converted to `DOUBLE` type.
- `DATETIME` and `BOOLEAN` are not allowed in the arithmetic operation