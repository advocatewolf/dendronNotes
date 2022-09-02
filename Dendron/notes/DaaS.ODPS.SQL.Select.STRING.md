---
id: jk2ggnb1s0eo6ynpmszo3ip
title: STRING
desc: ''
updated: 1661507942354
created: 1661482383633
---
[ref.](https://www.alibabacloud.com/help/en/maxcompute/latest/string-functions)

1. [[TABLE of STRING Functions|#^table]]
1. [[GET_JSON_OBJECT|#^get-json-object]]
1. [[Substr|#^substr]]
1. [[KEYVALUE|#^keyvalue]]
1. [[REGEXP_EXTRACT|#^regexp-extract]]

## Table of STRING Functions^table

Function  | Description
----------|------------
ASCII  | Returns the ASCII code of the first character in a specified string.
CHAR_MATCHCOUNT  | Calculates the number of characters of String A that appear in String B.
CHR  | Converts an ASCII code into a character.
CONCAT  | Concatenates all the specified strings and returns the final string.
CONCAT_WS  | Concatenates all input strings in an array by using a specified delimiter.
ENCODE  | Encodes a string in the specified encoding format.
FIND_IN_SET  | Returns the position of the specified string among multiple strings that are separated by commas (,).
FORMAT_NUMBER  | Converts a number into a string in the specified format.
FROM_JSON  | Returns data of the ARRAY, MAP, or STRUCT type based on a given JSON string and a given output format.
GET_JSON_OBJECT  | Extracts a single string from a standard JSON string based on a specified method.
INSTR  | Returns the position of String A in String B.
IS_ENCODING  | Determines whether a string can be converted from one character set to another character set.
KEYVALUE  | Splits a string into key-value pairs, separates the key-value pairs, and then returns the value that corresponds to a specified key.
KEYVALUE_TUPLE  | Splits a string into key-value pairs, separates the key-value pairs, and then returns the values that correspond to the keys.
LENGTH  | Returns the length of a string.
LENGTHB  | Calculates the length of a string in bytes.
LOCATE  | Returns the position of a specified string in another string.
LTRIM  | Removes the characters from the left side of a string.
MD5  | Returns the MD5 value of a string.
PARSE_URL  | Parses a URL and returns the specified part of the URL.
PARSE_URL_TUPLE  | Parses a URL and returns multiple parts of the URL.
REGEXP_COUNT  | Returns the number of substrings that match a specified pattern from a specified position.
REGEXP_EXTRACT  | Splits a string into groups based on a specified pattern and returns the string in a specified group.
REGEXP_INSTR  | Returns the start or end position of a substring that starts at a specified position and matches a specified pattern for a specified number of times.
REGEXP_REPLACE  | Uses a string to replace a substring of another string if the substring matches a specified pattern for a specified number of times.
REGEXP_SUBSTR  | Returns a substring in a string that matches a specified pattern for a specified number of times from a specified position.
REPEAT  | Returns a string that repeats a specified string for a specified number of times.
REVERSE  | Returns the characters of a string in reverse order.
RTRIM  | Removes the characters from the right side of a string.
SPACE  | Generates a space string.
SPLIT_PART  | Uses a delimiter to split a string into substrings and returns a substring of the specified part of the string.
SUBSTR  | Returns a substring that has a specified length from a specified position of a string. The string is of the STRING type.
SUBSTRING  | Returns a substring that has a specified length from a specified position of a string. The string is of the STRING or BINARY type.
TO_CHAR  | Converts data of the BOOLEAN, BIGINT, DECIMAL, or DOUBLE type into the STRING type.
TO_JSON  | Converts data of a complex data type into a JSON string.
TOLOWER  | Converts uppercase letters in a string into lowercase letters.
TOUPPER  | Converts lowercase letters in a string into uppercase letters.
TRIM  | Removes the characters from both of the left and right sides of a string.
URL_DECODE  | Encodes the input string in the application/x-www-form-urlencoded MIME format and returns the encoded string.
URL_ENCODE  | Converts an input string that is in the application/x-www-form-urlencoded MIME format into a standard string.
JSON_TUPLE  | Extracts strings from a standard JSON string based on a set of input keys.
LPAD  | Left pads a string to a specified length.
RPAD  | Right pads a string to a specified length.
REPLACE  | Replaces a substring in String A that matches String B with another substring.
SOUNDEX  | Converts a string into a string of the SOUNDEX type.
SUBSTRING_INDEX  | Truncates a string from a specified delimiter.
TRANSLATE  | Replaces the part of String A that appears in String B with String C.
REGEXP_EXTRACT_ALL  | Finds all substrings that match the pattern of a regular expression in a string and returns the substrings as an array. 


## get_json_object^get-json-object
Extracts a single string from a standard JSON string based on <path>.

Original data is read each time this function is called.
    - repeated calls may affect system performance and increase costs.
        - you can use `GET_JSON_OBJECT` with UDTFs (User-Defined Table Functions) to prevent repeated calls.

### `string get_json_object(string <json>, string <path>)`

- Parameter Description:
    - json: `STRING` type. 
        - standard JSON object in format of `{Key:Value, Key:Value, ...}`.
        - If string contains double quotation mark ("), use two backlashes (\\\\) to escape.
        - if string contains single quotation mark ('), use a single backlash (\\)to escape.
    - path: STRING type.
        - specifies path in the value of json, starts with `$`.
            - `$`: indicates root node
            - `.` or `['']`: indicates child node.
            - `[] ([number])`: indicates an array subscript, starts from 0.
            - `*`: indicates wildcard for `[]`, returns an entire array.
                - cannot be escaped.
- Return value:
    - if format of json is valid and path exists, related `STRING` is returned.
    - if json parameter is empty or inalid, NULL is returned.

#### GET_JSON_OBJECT Examples
```    
select get_json_object(content,'$.event_name') as event_name,count(1) as cnt
from mynt_dw.ods_bigquery_content_hh
    where dt='${bizdate}'
group by get_json_object(content,'$.event_name')
order by event_name;
```

## Substr^substr
Returns a substring that starts from **start_position** in a string specified by **str** and has a length specified by **length**.

### `STRING substr(STRING <str>, BIGINT <start_position>[, BIGINT <length>])`

- Parameter description:
    - str: STRING type.
        - if `BIGINT`, `DECIMAL`, `DOUBLE`, or `DATETIME`, implicitly converted to `STRING`.
    - start_position: `BIGINT` type, default value: 1
        - if set to 0, null is returned.
    - length: `BIGINT` type, optional.
        - must be greater than 0.
- Return value:
    - STRING type is returned
    - if **str** is not `STRING`, `BIGINT`, `DECIMAL`, `DOUBLE`, or `DATETIME`, error is returned.
    - if value of **length** is not of `BIGINT` type or less than or equal to 0, error is returned.
    - if **length** is not specified, substring from **start_position** to the end of **str** is returned.

#### Substr Examples
```
select substr('abc', 2);
-- The return value is bc. 

select substr('abc', 2, 1);
-- The return value is b. 

select substr('abc',-2 , 2);
-- The return value is bc. 
```

```
select substr(ip_role_id,-2,1) last1_id,substr(ip_role_id,-3,2) as last2_id
,count(1) as cnt
from dwd_pty_mbr_core_agent_base_dd
where dt='${bizdate}'
    and ip_role_id is not null
group by substr(ip_role_id,-2,1),substr(ip_role_id,-3,2)
order by last1_id,last2_id;
```

## KEYVALUE^keyvalue
splits **srcStr** into **key-value** pairs by **split1** and separate **key-value** pairs by **split2**. 

Return the value corresponding to key.

### `KEYVALUE(STRING <srcStr>,STRING <split1>,STRING <split2>, STRING <key>)`
### `KEYVALUE(STRING <srcStr>,STRING <key>) //<split1> = ";"，<split2> = ":"`

- Parameter description:
    - scrStr: Source `STRING` to be split.
    - key: Specified to return the nth string
        - after source string is split by **split1** and **split2**, return the corresponfing value according to the specification of the **key** value.
    - split1, split2: `STRING` used as delimiters by which **srcStr** is split.
        - if not specified, default value is
            - **split1**: `;`
            - **split2**: `:`
        - if **srcStr** `STRING` has been split by **split1** and has multiple **split2**, return result is not defined.
- Return value:
    - STRING type.
    - if **split1** or **split2** is NULL, return NULL.
    - if **srcStr** and **key** value are NULL or in case of no matched **key**, return NULL
    - if multiple **key-value** matches, return the value corresponding to the first matched key.

#### KEYVALUE Examples
```
select transid,keyvalue(keyvalue_str,';',':','description') as description
from (
select
158173773 as transid
,'filter:1;_uTrustCapsFlag:1;description:Pre-Midnight Sweeping 2019-05-18;confirmation_rule:1;_uTrustCapFlgPre:1;_globetranflag:1' as keyvalue_str
from dual
) t
;
```
transid | description
--------|------------
158173773 | Pre-Midnight Sweeping 2019-05-18

## SPLIT_PART^split-part
Split the `STRING` **str** according to **separator** and return the substring from the nth **start** path to nth **end** part.

### `STRING split_part(STRING <str>, STRING <separator>, BIGINT <start>[, BIGINT <end>])

- Parameter description:
    - str: `STRING` type.
        - `STRING` to be split
        - if `BIGINT`, `DOUBLE`, `DECIMAL`, or `DATETIME`, it is implicitly converted to `STRING`.
        - if other data type, exception.
    - separator: `STRING` type.
        - separator use to split the string
        - can be a character or a string
        - if not `STRING`, exception.
    - start: `BIGINT` type.
        - indicates start number of the return part.
        - must be greater than 0
        - if not constant or other data type, exception.
    - end: `BIGINT` type.
        - indicates end number of the return part.
        - must be greater than or equal to **start**, otherwise exception.
        - if not constant or other data type, exception.
        - can be excluded, indicates last part.
- Return value:
    - `STRING` type.
    - if any parameter is null, return null.
    - if separator is an empty string, return source string **str**.

#### Notes:
- if **separator** does not exist in **str**, and **start** is 1, return entire str.
- if input value is an empty string, output value is an empty string.
- if the start value is greater than the number of parts after split, return empty string.
    - e.g.,
    ```
    split_part('a,b,c,d', ',', 1) = 'a'
    split_part('a,b,c,d', ',', 1, 2) = 'a,b'
    split_part('a,b,c,d', ',', 10) = ''
    ```

## REGEXP_EXTRACT^regexp-extract
- split the string **source** according to Regex **pattern**, return the characters of the **occurence**(nth) group.
- [[Regex (Regular Expressions) Rules|DaaS.ODPS.SQL.regex]]

### ` STRING regexp_extract(STRING <source>, STRING <pattern>[, BIGINT <occurence>])`

- Parameter description:
    - source: `STRING` type.
        - string to be searched.
    - pattern: `STRING` type constant.
        - if pattern is null, exception
        - if 'group' is not specified in pattern, exception.
    - occurence: `BIGINT` type constant.
        - must be greater than or equal to 0.
        - if other type or less than 0, exception
        - if not specified, default value is 1.
        - if equal to 0, return substrings that satisfy the entire **pattern**
- Return value:
    - STRING type
    - if any input is NULL, return NULL

#### REGEXP_EXTRACT Examples
```
regexp_extract('foothebar', 'foo(. *?)( bar)', 1) = the
regexp_extract('foothebar', 'foo(. *?)( bar)', 2) = bar
regexp_extract('foothebar', 'foo(. *?)( bar)', 0) = foothebar
regexp_extract('8d99d8', '8d(\\d+)d8') = 99

-- If regular SQL is submitted on MaxCompute, two "\" must be used as the s
hift character.
regexp_extract('foothebar', 'foothebar')

-- The exception is thrown. ‘group’ is not specified in ‘pattern’.
```

```
select
dt
,count(1) as cnt
,min(to_char(dateadd(to_date(get_json_object(regexp_extract(content,'\\|({.*?)\001\\|'),'$.event_time'),'yyyy-mm-dd hh:mi:ss'),8,'hh'),'yyyy-mm-dd hh:mi:ss')) as min_date
,max(to_char(dateadd(to_date(get_json_object(regexp_extract(content,'\\|({.*?)\001\\|'),'$.event_time'),'yyyy-mm-dd hh:mi:ss'),8,'hh'),'yyyy-mm-dd hh:mi:ss')) as max_date
,min(substr(regexp_extract(content,'(.*?) - \001\\|'),1,19)) as min_logtime
,max(substr(regexp_extract(content,'(.*?) - \001\\|'),1,19)) as max_logtime
from ods_log_apgauss_af_push_hm_auto_delta
where dt>=${bizdate}
group by dt
order by dt;
```



