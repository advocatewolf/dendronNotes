---
id: h4pfbav9blr6q2680hykpyl
title: NOT IN
desc: ''
updated: 1662014827255
created: 1661846041823
---
[ref.](https://www.alibabacloud.com/help/en/maxcompute/latest/subqueries#section-f9k-trj-brn)

- used in a similar manner to `LEFT ANTI JOIN`. 
- if value of a row are NULL for a specified column in the table
    - value of the expression in `NOT IN` subquery is NULL
        - `WHERE` condition is invalid and no data is returned.

1. [[Syntax 1|#^syntax1]]
1. [[Syntax 2|#^syntax2]]
1. [[Syntax 3|#^syntax3]]
1. [[Examples|#^example]]

### SYNTAX^syntax

#### Syntax 1^syntax1

### `select <select_expr1> from <table_name1> where <select_expr2> not in (select <select_expr2> from <table_name2>);`


-- The preceding statement is equivalent to the following statement with `LEFT ANTI JOIN`. 

### `select <select_expr1> from <table_name1> <alias_name1> left anti join <table_name2> <alias_name2> on <alias_name1>.<select_expr1> = <alias_name2>.<select_expr2>;`

##### Note:
- If `select_expr2` specifies partition key columns, `select <select_expr2> from <table_name2>` is not converted into `LEFT ANTI JOIN`. 
    - A separate job is started to run a subquery. 
        - MaxCompute compares the subquery results with the columns specified in `select_expr2` in sequence. 
            - If the partitions of the table specified by `table_name1` contain the columns in `select_expr2` and these columns are not included in the results, MaxCompute does not read data from these partitions. This ensures that partition pruning is still valid. 

#### Syntax 2^syntax2

- MaxCompute supports `NOT IN` subquery and correlated conditions. where <table_name2_colname> = <table_name1>.<colname> in a subquery is a correlated condition.
- These expressions are part of the `ON` condition in `ANTI JOIN` operations.

### `select <select_expr1> from <table_name1> where <select_expr2> not in (select <select_expr2> from <table_name2> where <table_name2_colname> = <table_name1>.<colname>);`

#### Syntax 3^syntax3
- [ref.](https://www.alibabacloud.com/help/en/maxcompute/latest/subqueries#li-t1n-u8r-xck)

### Examples^example

#### Examples using Syntax 1

`SELECT * from mytable1 where id not in (select id from mytable2);`

-- is equivalent to

`SELECT * from mytable1 a LEFT OUTER JOIN mytable2 b on a.id=b.id where b.id is null;`

----------------

-- Create a table named shop1 and insert data into the table. 

`create table shop1 as select shop_name,customer_id,total_price from sale_detail;`

`insert into shop1 values ('s8','c1',100.1);`

`select * from shop1 where shop_name not in (select shop_name from sale_detail);`

shop_name | customer_id | total_price
----------|-------------|------------
s8 | c1 | 100.1

#### Examples using Syntax 2

`select * from shop1 where shop_name not in (select shop_name from sale_detail where customer_id = shop1.customer_id);`

shop_name | customer_id | total_price
----------|-------------|------------
s8 | c1 | 100.1