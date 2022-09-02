---
id: df5ubcomy2quhfdrsdnw9zw
title: Math
desc: ''
updated: 1661496351800
created: 1661482113986
---
[ref.](https://www.alibabacloud.com/help/en/maxcompute/latest/mathematical-functions)

Index:

1. [[Table|#^table]]

1. [[Round|#^round]]

1. [[Trunc|#^trunc]]

1. [[RAND|#^rand]]

1. [[DECIMAL|#^decimal]]




## Table of Math Functions^table

Function  | Description
----------|------------
ABS  | Calculates the absolute value.
ACOS  | Calculates the arccosine.
ASIN  | Calculates the arcsine.
ATAN  | Calculates the arctangent.
CEIL  | Rounds up a number and returns the nearest integer.
CONV  | Converts a number from one number system to another.
COS  | Calculates the cosine.
COSH  | Calculates the hyperbolic cosine.
COT  | Calculates the cotangent.
EXP  | Calculates the exponential value.
FLOOR  | Rounds down a number and returns the nearest integer.
LN  | Calculates the natural logarithm.
LOG  | Calculates the logarithm.
POW  | Calculates the nth power of a value.
RAND  | Returns a random number.
ROUND  | Returns a value rounded to the specified decimal place.
SIN  | Calculates the sine.
SINH  | Calculates the hyperbolic sine.
SQRT  | Calculates the square root.
TAN  | Calculates the tangent.
TANH  | Calculates the hyperbolic tangent.
TRUNC  | Truncates the input value to the specified decimal place.
BIN  | Calculates the binary code.
CBRT  | Calculates the cube root.
CORR  | Calculates the Pearson correlation coefficient.
DEGREES  | Converts a radian value into a degree.
E  | Calculates the value of e.
FACTORIAL  | Calculates the factorial.
FORMAT_NUMBER  | Converts a number into a string in the specified format.
HEX  | Converts an integer or a string into a hexadecimal number.
LOG2  | Calculates the logarithm of a number with the base number of 2.
LOG10  | Calculates the logarithm of a number with the base number of 10.
PI  | Calculates the value of π.
RADIANS  | Converts a degree into a radian value.
SIGN  | Returns the sign of the input value.
SHIFTLEFT  | Shifts a value left by a specific number of places.
SHIFTRIGHT  | Shifts a value right by a specific number of places.
SHIFTRIGHTUNSIGNED  | Shifts an unsigned value right by a specific number of places.
UNHEX  | Converts a hexadecimal string into a string.
WIDTH_BUCKET  | Returns the ID of the bucket into which the value of a specific expression falls.

## Round^round
Returns a value rounded to the specified decimal place.

### `Double round(Double number, [Bigint Decimal_places])`
### `Decimal round(Decimal number, [Bigint Decimal_places])`

- Parameter Description:
    - number: `DOUBLE` or `DECIMAL`
        - if input is `STRING` or `BIGINT`, converted to `DOUBLE` by implicit conversion
        - if input is another type, error occurs.
- Return value:
    - Returns `DOUBLE` or `DECIMAL` type
    - if number or Decimal_places is NULL, return NULL

#### Round Example
```
round(125.315) = 125.0
round(125.315, 0) = 125.0
Round (125.315, 1) = 125.3
round(125.315, 2) = 125.32
round(125.315, 3) = 125.315
round(-125.315, 2) = -125.32
round(123.345, -2) = 100.0
round(null) = null
round(123.345, 4) = 123.345
round(123.345, -4) = 0.0
```

## TRUNC^trunc
Function to intercept the input number to a specified decimal point place.

### `DOUBLE trunc(DOUBLE number[, BIGINT Decimal_places])`
### `DECIMAL trunc(DECIMAL number[, BIGINT Decimal_places])`

- Parameter description:
    - number: `DOUBLE` or `DECIMAL` type.
        - if input is `STRING` or `BIGINT`, converted to `DOUBLE` by implicit conversion.
        - if input is another type, error occurs.
    - Decimal_places:
        - `BIGINT` type constant, the decimal point place to intercept the number.
        - Other types are implicitly converted to `BIGINT`
        - if parameter is excluded, default to intercept to single digit
- Return value:
    - Return `DOUBLE` or `DECIMAL` type.
    - if number or Decimal_places is NULL, return NULL

#### Note:
- if `DOUBLE` type is returned, the display of the returned result may not be as expected, such as `trunc(125.815, 1)`; problem exists on all systems.
- part to be truncated is supplemented by zero
- Decimal_places can be negative.
    - negative is truncated from the decimal point to the left and delete the decimal part
    - if Decimal_place are greater than the length of the integer, return zero.

#### TRUNC Examples
```
trunc(125.815) = 125.0
trunc(125.815, 0) =125.0
trunc(125.815, 1) = 125.80000000000001
trunc(125.815, 2) = 125.81
trunc(125.815, 3) = 125.815
trunc(-125.815, 2) = -125.81
trunc(125.815, -1) = 120.0
trunc(125.815, -2) = 100.0
trunc(125.815, -3) = 0.0
trunc(123.345, 4) = 123.345
trunc(123.345, -4) = 0.0
```


## RAND^rand
Return a random number (changes row to row)
Specifying the seed makes sure the generated random number sequence is deterministic.
Return value range is from 0 to 1

### `DOUBLE rand(BIGINT seed)`

- Parameter description:
    - seed: `BIGINT` type, random number seed, to determine starting values of the random number sequence
- Return value:
    - Returns `DOUBLE` type.

#### RAND Examples
```
set odps.sql.type.system.odps2=true;
select
id
,coalesce(id,concat('RAND',cast(rand() as string))) as id_r1
,coalesce(id,concat('RAND',rand(100000))) as id_r2
,coalesce(id,concat('RAND',cast(rand(UNIX_TIMESTAMP(current_timestamp()))
as string))) as id_r3
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
order by id,id_r3
;
```
![RAND Example](/assets/images/2022-08-26-14-34-52.png)

## DECIMAL^decimal

#### DECIMAL Example
```
select
cast(1234/100 as decimal) as num1
,1234/100 as num2
,cast(cast(1234 as decimal)/100 as decimal) as num3
from dual;
```

num1 | num2 | num3
-----|------|-----
12.339999999999999858 | 12.34 | 12.34
