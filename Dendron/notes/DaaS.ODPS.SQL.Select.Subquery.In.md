---
id: zbyljtconsnc577ddo4gqgy
title: IN
desc: ''
updated: 1662014906389
created: 1661845943856
---
[[ref.|https://www.alibabacloud.com/help/en/maxcompute/latest/subqueries#section-kft-z3r-5b2]]

- used in a similar manner to **`LEFT SEMI JOIN`**.
- if value of a row are NULL for a specified column in the table
    - value of the expression in `IN` subquery is NULL
        - `WHERE` condition is invalid and no data is returned.

1. [[Syntax 1|#^syntax1]]
1. [[Syntax 2|#^syntax2]]
1. [[additional|#^additional]]


#### Syntax 1^syntax1
### `select <select_expr1> from <table_name1> where <select_expr2> in (select <select_expr2> from <table_name2>);`

-- The preceding statement is equivalent to the following statement with `LEFT SEMI JOIN`: 

`select <select_expr1> from <table_name1> <alias_name1> left semi join <table_name2> <alias_name2> on <alias_name1>.<select_expr1> = <alias_name2>.<select_expr2>;`

#### Example using Syntax 1:

### `SELECT * from mytable1 where id in (select id from mytable2);`

-- is equivalent to using `LEFT OUTER JOIN`

### `SELECT * from mytable1 a LEFT OUTER JOIN mytable2 b on a.id=b.id where b.id is not null;`

#### Syntax 2^syntax2
MaxCompute supports `IN` subquery and correlated conditions.
- `where <table_name2_colname> = <table_name1>.<colname>` is a correlated condition.
- These expressions are part of the `ON` condition in `SEMI JOIN` operations. 

`select <select_expr1> from <table_name1> where <select_expr2> in (select <select_expr2> from <table_name2> where <table_name2_colname> = <table_name1>.<colname>);`

#### EXAMPLE using SYNTAX 2:

`select * from sale_detail where shop_name in (select shop_name from shop where customer_id = shop.customer_id);`

#### NOTE:
-  MaxCompute supports `IN` subquery that does not serve as a `JOIN` condition. 
    - For example, a non-`WHERE` clause uses IN SUBQUERY, or a `WHERE` clause uses `IN` subquery that cannot be converted into a `JOIN` condition. 
        - In this case, `IN` subquery cannot be converted into `SEMI JOIN`. 
            - A separate job must be started to run a subquery. 
            - Correlated conditions are not supported.

#### ADDITIONAL:^additional
- [[SYNTAX 3|https://www.alibabacloud.com/help/en/maxcompute/latest/subqueries#li-5of-ydh-3ih]]