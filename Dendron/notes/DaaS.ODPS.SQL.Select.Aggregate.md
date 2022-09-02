---
id: bknshxo3iddkjw132wqy4x4
title: Aggregate
desc: ''
updated: 1661499370912
created: 1661482323692
---
[ref.](https://www.alibabacloud.com/help/en/maxcompute/latest/aggregate-functions)

Index:

1. [[Table of Aggregate Functions|#^table]]
2. [[WM_CONCAT|#^wm-concat]]

## Table of Aggregate Functions^table

Function  | Description
----------|------------
AVG  | Returns the average value of a column.
COUNT  | Returns the number of records that match the specified criteria.
COUNT_IF  | Returns the number of records whose expr value is True.
MAX  | Returns the maximum value of a column.
MIN  | Returns the minimum value of a column.
MEDIAN  | Returns the median value of a column.
STDDEV  | Returns the population standard deviation of all the input values.
STDDEV_SAMP  | Returns the sample standard deviation of all the input values.
SUM  | Returns the sum of a column.
WM_CONCAT  | Concatenates strings with a specified delimiter.
ANY_VALUE  | Returns a non-deterministic value from a specified column.
APPROX_DISTINCT  | Returns the approximate number of distinct input values in a specified column.
ARG_MAX  | Returns the column value of the row that corresponds to the maximum value of a specified column.
ARG_MIN  | Returns the column value of the row that corresponds to the minimum value of a specified column.
COLLECT_LIST  | Aggregates values from a specified column into an array.
COLLECT_SET  | Aggregates only distinct values from a specified column into an array.
NUMERIC_HISTOGRAM  | Returns the approximate histogram of a specified column.
PERCENTILE_APPROX  | Returns approximate percentiles. This function applies to scenarios in which a large amount of data is calculated.
BITWISE_OR_AGG  | Aggregates input values based on the bitwise OR operation.
MAP_AGG  | Returns a map that is created by using a and b. a is the key in the map. b is the value of the key in the map.
MULTIMAP_AGG  | Returns a map that is created by using a and b. a is the key in the map. b is used to create an array, which is used as the value of the key in the map.
MAP_UNION  | Returns a new map that is the union of all input maps.
MAP_UNION_SUM  | Returns a new map that is the union of all input maps. The output map sums the values of the matching keys in all input maps.
HISTOGRAM  | Returns a map that contains the number of times each input value appears. 


## WM_CONCAT^wm-concat
Uses a specific separator to link the value in STR.

### `string wm_concat(string <separator>, string <colname>)`

- Parameter description:
    - Separator: a `STRING` type constant.
        - Constants of other types or non-constants can throw exceptions.
    - colname: `STRING` type.
        - If input is `BIGINT`, `DOUBLE`, or `DATETIME` type, value is converted implicitly into `STRING`.
        - if it is another type, exception.

#### WM_CONCAT Examples
```
select transid,wm_concat(';',concat(td_key,':',value)) as keyvalue_str
from ods_gcash_rep_trans_data_delta_merge
where dt=max_pt('mynt_dw.ods_gcash_rep_trans_data_delta_merge')
and transid='158173773'
group by transid;
```
![WM_Concat Example](/assets/images/2022-08-26-15-31-39.png)