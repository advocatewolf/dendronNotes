---
id: 67064dasfxmyk35qhyjkr5v
title: NOT EXISTS
desc: ''
updated: 1662018270098
created: 1662017867273
---
[ref.](https://www.alibabacloud.com/help/en/maxcompute/latest/subqueries#li-t1n-u8r-xck)

- if `NOT EXISTS` subquery clause returns no data, TRUE is returned, otherwise FALSE.
- MaxCompute supports only the `WHERE` subqueries that have correlated conditions.
### `select <select_expr> from <table_name1> where not exists (select <select_expr> from <table_name2> where <table_name2_colname> = <table_name1>.<colname>);`

- Parameter description:
    - `select_expr`: format of `col1_name`, `col2_name`, [[Regular Expressions|DaaS.ODPS.SQL.regex]], ...
        - indicates common columns or partition key columns that you want to query
        - indicates regular expressions that are used for a query
    - `table_name1` and `table_name2`: specifies names of tables.
    - `col_name`: specifies name of a column in the table.

#### EXAMPLES

`SELECT * from mytable1 where not exists (select * from mytable2 where id = mytable1.id);`

-- is equivalent to

`SELECT * from mytable1 a LEFT OUTER JOIN mytable2 b on a.id=b.id where b.id is null;`

---

`select * from sale_detail where not exists (select * from shop where shop_name = sale_detail.shop_name);`

-- The preceding statement is equivalent to the following statement: 
`select * from sale_detail a left anti join shop b on a.shop_name = b.shop_name;`

shop_name | customer_id | total_price | sale_date | region | 
----------|-------------|-------------|-----------|--------|-
| |