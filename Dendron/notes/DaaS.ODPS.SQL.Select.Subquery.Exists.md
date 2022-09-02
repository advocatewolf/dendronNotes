---
id: rk3xfkcvm5l06is2y26qqn3
title: EXISTS
desc: ''
updated: 1662017981836
created: 1662014935409
---
[ref.](https://www.alibabacloud.com/help/en/maxcompute/latest/subqueries#li-t1n-u8r-xck)

- if `EXISTS` subquery clause returns at least one row of data, TRUE is returned.

### `select <select_expr> from <table_name1> where exists (select <select_expr> from <table_name2> where <table_name2_colname> = <table_name1>.<colname>);`

- Parameter description:
    - `select_expr`: format of `col1_name`, `col2_name`, [[Regular Expressions|DaaS.ODPS.SQL.regex]], ...
        - indicates common columns or partition key columns that you want to query
        - indicates regular expressions that are used for a query
    - `table_name1` and `table_name2`: specifies names of tables.
    - `col_name`: specifies name of a column in the table.

#### EXAMPLE
`SELECT * from mytable1 where exists (select * from mytable2 where id = mytable1.id);`


-- is equivalent to

`Select * From mytable1 a left outer join mytable2 B on A. ID = B. ID where B.id is not null;`

---
`select * from sale_detail where exists (select * from shop where customer_id = sale_detail.customer_id);`

-- The preceding statement is equivalent to the following statement: 

`select * from sale_detail a left semi join shop b on a.customer_id = b.customer_id;`

shop_name | customer_id | total_price | sale_date | region | 
----------|-------------|-------------|-----------|--------|-
null | c5 | NULL | 2014 | shanghai | 
s6 | c6 | 100.4 | 2014 | shanghai | 
s7 | c7 | 100.5 | 2014 | shanghai | 
s1 | c1 | 100.1 | 2013 | china | 
s2 | c2 | 100.2 | 2013 | china | 
s3 | c3 | 100.3 | 2013 | china | 