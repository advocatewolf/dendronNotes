---
id: c96owjf3njk3wjnd0zqctl1
title: Window
desc: ''
updated: 1661498487471
created: 1661482164842
---
[ref.](https://www.alibabacloud.com/help/en/maxcompute/latest/builtin-functions-window-functions)

1. [[Limits|#^limit]]

1. [[Table of Window Functions|#^table]]

1. [[ROW_NUMBER|#^row-number]]

1. [[PERCENT_RANK|#^percent-rank]]



## Limits^limit
- Window functions are supported only in `SELECT` statements.
- A window function cannot contain nested window functions or aggregate functions.
- You cannot use window functions together with aggregate functions of the same level.

## Table of Window Functions^table

Function  | Description
----------|------------
ROW_NUMBER  | Calculates the sequence number of a row. The row number starts from 1.
RANK  | Calculates the rank of a row in an ordered group of rows. The ranks may not be consecutive integers.
DENSE_RANK  | Calculates the rank of a row in an ordered group of rows. The ranks are consecutive integers.
PERCENT_RANK  | Calculates the percentile rank of a row in an ordered group of rows.
CUME_DIST  | Calculates the cumulative distribution of data in a partition.
NTILE  | Splits rows of data in a partition into N groups of equal size and returns the number of the group to which the current row belongs. The group number ranges from 1 to N.
LAG  | Obtains the calculated result of the Nth row of data that precedes the current row at a given offset in a window.
LEAD  | Obtains the calculated result of the Nth row of data that follows the current row at a given offset in a window.
FIRST_VALUE  | Obtains the calculated result of the first row of data in the window to which the current row belongs.
LAST_VALUE  | Obtains the calculated result of the last row of data in the window to which the current row belongs.
NTH_VALUE  | Obtains the calculated result of the Nth row of data in a window to which the current row belongs.
CLUSTER_SAMPLE  | Samples random rows of data. If true is returned, the specified row of data is sampled.
COUNT  | Calculates the number of rows in a window.
MIN  | Calculates the minimum value in a window.
MAX  | Calculates the maximum value in a window.
AVG  | Calculates the average value of data in a window.
SUM  | Calculates the sum of data in a window.
MEDIAN  | Calculates the median in a window.
STDDEV  | Returns the population standard deviation of all input values. This function is also called STDDEV_POP.
STDDEV_SAMP  | Returns the sample standard deviation of all input values. 

## ROW_NUMBER^row-number
Calculates the row number, beginning from 1.

### `row_number() over(partition by [col1, col2…]`
### `order by [col1[asc|desc], col2[asc|desc]…])`
- Parameter description:
    - partition by [col1, col2,...]: Specificies columns to use window function
    - order by col1[asc|desc], col2[asc|desc]: Specifies order method for return result.
- Return value:
    - returns `BIGINT` type

#### ROW_NUMBER Examples
```
select
id
,name
,row_number() over(order by id asc) as rn
,rank() over(order by id asc) as rk
from (
select 1 as id ,'test1' as name from dual union all
select null as id ,'unknown' as name from dual union all
select null as id ,'unknown' as name from dual union all
select 2 as id ,'test2' as name from dual union all
select 3 as id ,'test3' as name from dual union all
select 4 as id ,'test4' as name from dual union all
select 5 as id ,'test5' as name from dual union all
select 6 as id ,'test6' as name from dual
) t
order by id;
```
![row_number Example](/assets/images/2022-08-26-15-03-55.png)

## PERCENT_RANK^percent-rank
Calculate relative ranking of a certain row in a group data.

- Parameter description:
    - partition by [col1, col2...]: Specifies columns to use window function.
    - order by col1[asc|desc], col2[asc|desc]: Specifies the order of the value based on the ranking.

- Return Value:
    - returns DOUBLE type
    - scope is [0,1]
    - calculation method of relative ranking is `(rank-1)/(number of rows -1)`.

#### PERCENT_RANK Examples

```
select user_id,ep,PERCENT_RANK() over(order by ep asc) as pct_rank
from
(
select 'A' user_id,10 as ep from dual
union all
select 'B' user_id,10 as ep from dual
union all
select 'C' user_id,20 as ep from dual
union all
select 'D' user_id,15 as ep from dual
union all
select 'E' user_id,50 as ep from dual
union all
select 'F' user_id,30 as ep from dual
union all
select 'G' user_id,45 as ep from dual
union all
select 'H' user_id,60 as ep from dual
union all
select 'I' user_id,70 as ep from dual
) t;
```

![PERCENT_RANK Example](/assets/images/2022-08-26-15-19-27.png)