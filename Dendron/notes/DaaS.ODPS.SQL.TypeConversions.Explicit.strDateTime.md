---
id: x0itbrx72bx7tj0hhssrerp
title: STRING to DATETIME
desc: ''
updated: 1661417109464
created: 1661416131311
---
- MaxCompute supports conversions between the STRING type and DATETIME type. 
- The conversion format is `yyyy-mm-dd hh:mi:ss`

Unit | STRING(case-insensitive) | Value 
-----|--------------------------|-------
Year | yyyy | 0001 - 9999 
Month | mm | 01 - 12 
Day | dd | 01 - 28, 29, 30, 31
Hour | hh | 00 - 23 
Minute | mi | 00 - 59 
Second | ss | 00 - 59

## Notes:
- In the **Value range**, if first digit is 0, it cannot be ignored
    - `2014-1-9 12:12:12` is an invalid DATETIME format and cannot be converted from STRING to DATETIME
        - must be `2014-01-09 12:12:12`
- Only the STRING type that meets the preceding format requirements can be converted to the DATETIME type.
    - e.g., `cast(“2013-12-31 02:34:34” as datetime)` converts STRING to DATETIME
    - similarly, when DATETIME is converted to STRING, default conversion format is `yyyy-mm-dd hh:mi:ss`

## Examples of Conversions returning an Exception
`cast("2013/12/31 02/34/34" as datetime)`

`cast("20131231023434" as datetime)`

`cast("2013-12-31 2:34:34" as datetime)`

- threshold of `dd` depends on the the actual days of a month, if exceeded conversion is aborted with an error

`cast("2013-02-29 12:12:12" as datetime) -- Returns an error because February 29, 2013 does not exist.`

`cast("2013-11-31 12:12:12" as datetime) -- Returns an exception because November 31, 2013 does not exist.`

### Additional Notes:
- MaxCompute provides the [[TO_DATE|DaaS.ODPS.SQL.BuiltInFunctions.TO_DATE]] function to convert the STRING type that does not meet the Date DATETIME ime format to the DATETIME type.