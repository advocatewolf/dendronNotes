---
id: chkim6n0qvqoi30ppfxbugl
title: Create Table ... Like
desc: ''
updated: 1661417739528
created: 1661417562628
---
To allow the destination table to have the same structure as source table, use `create table ... like` statement:

`create table sale_detail_like like sale_detail;`

- table structure of `sale_detail_like` is exactly the same as `sale_detail`.
    - except the life cycle, 
    - attributes, including the column name, column comment, and table comment, of the two tables are the same
    - data in `sale_detail` cannot be copied into the table `sale_detail_like`s