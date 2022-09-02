---
id: os0dti074935j2orfh8jckj
title: Other
desc: ''
updated: 1661841856777
created: 1661482403092
---
[ref.](https://www.alibabacloud.com/help/en/maxcompute/latest/other-functions)

1. [[TABLE|#^table]]
1. [[GREATEST|#^greatest]]
1. [[LEAST|#^least]]
1. [[UUID|#^uuid]]

## Table of OTHER functions^table
Function  | Description
----------|------------
BASE64  | Converts a binary value into a Base64-encoded string.
BETWEEN AND expression  | Returns the values that fall in or fall out of the specified range.
CASE WHEN expression  | Returns values based on the computing result of an expression.
CAST  | Converts the result of an expression into the specified data type.
COALESCE  | Returns the first non-null value in the parameter list.
COMPRESS  | Uses the GZIP algorithm to compress input parameters of the STRING or BINARY type.
CRC32  | Calculates the cyclic redundancy check (CRC) value of a value that is of the STRING or BINARY type.
DECODE  | Implements the IF-THEN-ELSE logic.
DECOMPRESS  | Uses the GZIP algorithm to decompress input parameters of the BINARY type.
GET_IDCARD_AGE  | Returns an age in years based on the ID card number.
GET_IDCARD_BIRTHDAY  | Returns the date of birth based on the ID card number.
GET_IDCARD_SEX  | Returns the gender based on the ID card number.
GET_USER_ID  | Obtains the ID of the current account.
GREATEST  | Returns the maximum value of the input parameters.
HASH  | Calculates a hash value based on the input parameters.
IF  | Checks whether a specified condition is true.
LEAST  | Returns the minimum value of the input parameters.
MAX_PT  | Returns the name of the largest level-1 partition in a partitioned table.
NULLIF  | Checks whether the values of two input parameters are the same.
NVL  | Specifies the return values of the parameters whose values are null.
ORDINAL  | Sorts the values of the input variables in ascending order and returns the value that is ranked at a specified position.
PARTITION_EXISTS  | Checks whether a specified partition exists in a table.
SAMPLE  | Samples all column values that are read and filters out the rows that do not meet sampling conditions.
SHA  | Calculates the SHA-1 hash value of a value that is of the STRING or BINARY type.
SHA1  | Calculates the SHA-1 hash value of a value that is of the STRING or BINARY type.
SHA2  | Calculates the SHA-2 hash value of a value that is of the STRING or BINARY type.
SIGN  | Determines the sign of a value. The sign indicates whether a value is positive or negative.
SPLIT  | Splits a string with a specified delimiter and returns an array.
STACK  | Splits a specified parameter group into a specified number of rows.
STR_TO_MAP  | Splits a string with a specified delimiter and returns a key-value pair.
TABLE_EXISTS  | Checks whether a specified table exists.
TRANS_ARRAY  | Transposes one row of data into multiple rows. This function is a user-defined table-valued function (UDTF) that transposes an array separated by fixed delimiters in a column into multiple rows.
TRANS_COLS  | Transposes one row of data into multiple rows. This function is a UDTF that transposes columns into rows.
UNBASE64  | Converts a Base64-encoded string into a binary value.
UNIQUE_ID  | Returns a unique ID. This function is more efficient than the UUID function.
UUID  | Returns a random ID. 

## GREATEST^greatest
Return the maximum value of the input parameter

### `greatest(<var1>,<var2>, ...)`
- Parameter description:
    - var1/var2: can be `BIGINT`, `DOUBLE`, `DECIMAL`, `DATETIME`, or `STRING` type.
    - if all values are `NULL`, return `NULL`
- Return value:
    - Maximum Value in input parameter
    - return type is same as input parameter type
    - `NULL` is the least value.
    - if input parameter types are differnet:
        - `DOUBLE`, `BIGINT`, `DECIMAL`, and `STRING` type, convert to `DOUBLE` type.
        - `STRING`, and `DATETIME`, convert to `DATETIME` type.
        - Other implicit conversion is not allowed.

## LEAST^least
Return the minimum value of the input parameters.

### `least(<var1>, <var2>, ...)`

### Note: Same parameter description and return value as  [[#^GREATEST]]

## UUID^uuid
Returns a random ID, i.e. 29347a88-1e57-41ae-bb68-a9edbdd94212

### `STRING uuid()`

#### Note:
- UUID returns a random global ID with a low probability of duplication.
