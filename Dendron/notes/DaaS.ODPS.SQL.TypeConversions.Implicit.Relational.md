---
id: 47ct6kg19xwolgks3b78rmi
title: Relational Operators
desc: ''
updated: 1661411803748
created: 1661411602377
---
## [[Relational Operators|DaaS.ODPS.SQL.RelationalOperators]]

Common | Special
-------|--------
equal to (=) | LIKE
not equal to (<>) | RLIKE
less than (<) | and IN
less than or equal to (<=) | 
greater than (>) | 
greater than or equal to (>=) | 


### Implicit Conversion with Relational Operators
![Implicit Conversion with Relational Operators](/assets/images/2022-08-25-15-10-08.png)

From/To | BIGINT | DOUBLE | STRING | DATETIME | BOOLEAN | DECIMAL
--------|--------|--------|--------|----------|---------|--------
BIGINT | N/A | DOUBLE | DOUBLE | N | N | DECIMAL
DOUBLE | DOUBLE | N/A | DOUBLE | N | N | DECIMAL
STRING | DOUBLE | DOUBLE | N/A | DATETIME | N | DECIMAL
DATETIME | N | N | DATETIME | N/A | N | N
BOOLEAN | N | N | N | N | N/A | N
DECIMAL | DECIMAL | DECIMAL | DECIMAL | N | N | N/A

### Notes:
- If two types cannot be implicitly converted, the relational operation is aborted by an error.