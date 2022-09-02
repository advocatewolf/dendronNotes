---
id: 7dydfflaz49dxhbdmv2idbf
title: Date
desc: ''
updated: 1661486419891
created: 1661419563759
---
[ref.](https://www.alibabacloud.com/help/en/maxcompute/latest/date-functions)

1. [[Table of Date Functions|#^table]]
1. [[GETDATE|#^getdate]]
1. [[UNIX_TIMESTAMP|#^unix-timestamp]]
1. [[FROM_UNIXTIME|#^from-unixtime]]
1. [[DATEDIFF|#^datediff]]
1. [[Examples|#^examples]]



## Table of DATE Functions^table

Function  | Description
----------|------------
DATEADD  | Changes a date value based on the time unit specified by datepart and the interval specified by delta.
DATE_ADD  | Adds or subtracts a number of days to or from a date value based on the interval specified by delta. The DATE_ADD function is the inverse of the DATE_SUB function.
DATE_FORMAT  | Converts a date value into a string in a specified format.
DATE_SUB  | Adds or subtracts a number of days to or from a date value based on the interval specified by delta. The DATE_SUB function is the inverse of the DATE_ADD function.
DATEDIFF  | Calculates the difference between two date values based on the time unit specified by datepart.
DATEPART  | Returns a specified component of a date value based on the time unit specified by datepart.
DATETRUNC  | Truncates a date value based on the time unit specified by datepart.
FROM_UNIXTIME  | Converts a UNIX timestamp of the BIGINT type into a date value of the DATETIME type.
GETDATE  | Returns the current system time as a date value.
ISDATE  | Determines whether a date string can be converted into a date value in a specified format.
LASTDAY  | Returns the last day of the month in which a date value falls.
TO_DATE  | Converts a string into a date value in a specified format.
TO_CHAR  | Converts a date value into a string in a specified format.
UNIX_TIMESTAMP  | Converts a date value into a UNIX timestamp that is an integer.
WEEKDAY  | Returns a number that represents the day of the week in which a date value falls.
WEEKOFYEAR  | Returns a number that represents the week of the year in which a date value falls.
ADD_MONTHS  | Returns a date value that is obtained after a number of months are added to a specified date.
CURRENT_TIMESTAMP  | Returns the current timestamp.
DAY  | Returns the day in which a date value falls.
DAYOFMONTH  | Returns the day component of a date value.
EXTRACT  | Returns a specified component of a timestamp.
FROM_UTC_TIMESTAMP  | Converts a UTC timestamp into a timestamp for a specified time zone.
HOUR  | Returns the hour component of a date value.
LAST_DAY  | Returns the last day of the month in which a date value falls.
MINUTE  | Returns the minute component of a date value.
MONTH  | Returns the month in which a date value falls.
MONTHS_BETWEEN  | Returns the number of months between specified date values.
NEXT_DAY  | Returns the date of the first weekday that is later than a date value.
QUARTER  | Returns the quarter in which a date value falls.
SECOND  | Returns the second component of a date value.
TO_MILLIS  | Converts a date value into a UNIX timestamp that is accurate to the millisecond.
YEAR  | Returns the year in which a date value falls. 

## GETDATE^getdate
Get present system time. 
### `datetime getdate()`

- Use UTC+8 as MaxCompute standard time.
- Return value:
    - Datetime type, return present date and time.

#### Note
- In a MaxCompute SQL task (executed in a distributed manner), ‘getdate’ always returns a fixed value. 
- The return result is any time in MaxCompute SQL execution period
- the precision of time is accurate to seconds.

## UNIX_TIMESTAMP^unix-timestamp
Convert the date of Datetime type to UNIX format date of Bigint type.

### `bigint unix_timestamp(datetime date)`

- Parameter description:
    - date: Datetime type date value. 
        - If the input is ‘string’ type, it is converted to ‘datetime’ type and involved in calculation. 
        - If it is another type, an exception indicated.
    - Return value:
        - `bigint` type, it indicates UNIX format date value. 
        - If ‘date’ is NULL, return NULL.

## FROM_UNIXTIME^from-unixtime
Convert the numeric UNIX time value 'unixtime' to datetime value

### `datetime from_unixtime(bigint unixtime)`
- Parameter description:
    - `unixtime`: bigint type, number of seconds, UNIX format date time value
        - if input is `STRING`, `DOUBLE`, it is converted to `BIGINT` by implicit conversion
- Return Value:
    - `DATETIME` type date value
    - if `unixtime` is NULL, return NULL

#### Note:
- if you have `set odps.sql.hive.compatible=true;`, and input type is `STRING`, the return type will be `STRING` too.

## DATEDIFF^datediff
Calculate the difference between two `DATETIME` date1 and date2 in specified time unit 'datepart'

### `bigint datediff(datetime date1, datetime date2, string datepart)`
- Parameter description:
    - date1, date2: `DATETIME` type, minuend, meiosis.
        - if input is `STRING`, converted to `DATETIME` by implicit conversion.
        - if another data type, exception.
    - datepart: `STRING` constant.
        - extensional date format is supported
        - if datepart does not meet specified format or is other data type, exception.
- Return Value
    - Return `BIGINT` type.
    - If any input parameter is NULL, return NULL
    - if date1 is less than date2, return value may be negative.

#### Note:
- lower unit part is cut off according to 'datepart' in the calculation process and then calculate the result
    - e.g., 
```
If start = 2005-12-31 23:59:59, end = 2006-01-01 00:00:00:
    datediff(end, start, 'dd') = 1
    datediff(end, start, 'mm') = 1
    datediff(end, start, 'yyyy') = 1
    datediff(end, start, 'hh') = 1
    datediff(end, start, 'mi') = 1
    datediff(end, start, 'ss') = 1

    datediff('2013-05-31 13:00:00', '2013-05-31 12:30:00', 'ss') = 1800
    datediff('2013-05-31 13:00:00', '2013-05-31 12:30:00', 'mi') = 30

If start = 19:33:23. 234, end = 19:33:23. 250 .Dates with milliseconds do not belong to the standard datetime style, and cannot be converted implicitly directly.Explicit conversion is required here:

datediff(to_date('2018-06-04 19:33:23.250', 'yyyy-MM-dd hh:mi:ss.ff3'),to_date('2018-06-04 19:33:23.234', 'yyyy-MM-dd hh:mi:ss.ff3') , 'ff3') = 16
```
## Examples^examples
```


--SendMoney Core KPI
--Current Month:concat(substr('${bizdate}',1,6),'01')
--Current Year:concat(substr('${bizdate}',1,4),'0101')
--30days rolling:to_char(dateadd(to_date('${bizdate}','yyyymmdd'),-30,'dd'),'yyyymmdd')
--365days rolling:to_char(dateadd(to_date('${bizdate}','yyyymmdd'),-365,'dd'),'yyyymmdd')
select
  '${bizdate}' as report_date 

--P2P Active Users
  
  ,count(
    distinct case when report_date = '${bizdate}' then gcash_wallet elsenull end
  ) as p2p_activeusers_1d,
  count(
    distinct case when report_date > to_char(
      dateadd(to_date('${bizdate}', 'yyyymmdd'), -30, 'dd'),
      'yyyymmdd'
    )
    and report_date <= '${bizdate}' then gcash_wallet else null end
  ) as p2p_activeusers_30d,
  count(
    distinct case when report_date > to_char(
      dateadd(to_date('${bizdate}', 'yyyymmdd'), -365, 'dd'),
      'yyyymmdd'
    )
    and report_date <= '${bizdate}' then gcash_wallet else null end
  ) as p2p_activeusers_365d,
  count(
    distinct case when report_date >= concat(substr('${bizdate}', 1, 6), '01')
    and report_date <= '${bizdate}' then gcash_wallet else null end
  ) as p2p_activeusers_mtd,
  count(
    distinct case when report_date >= concat(substr('${bizdate}', 1, 4), '0101')
    and report_date <= '${bizdate}' then gcash_wallet else null end
  ) as p2p_activeusers_ytd 

--P2P Sender Users
  
  ,count(
    distinct case when report_date = '${bizdate}'
    and peer_type = 'sender' then gcash_wallet else null end
  ) as p2p_senderusers_1d,
  count(
    distinct case when report_date > to_char(
      dateadd(to_date('${bizdate}', 'yyyymmdd'), -30, 'dd'),
      'yyyymmdd'
    )
    and report_date <= '${bizdate}'
    and peer_type = 'sender' then gcash_wallet else null end
  ) as p2p_senderusers_30d,
  count(
    distinct case when report_date > to_char(
      dateadd(to_date('${bizdate}', 'yyyymmdd'), -365, 'dd'),
      'yyyymmdd'
    )
    and report_date <= '${bizdate}'
    and peer_type = 'sender' then gcash_wallet else null end
  ) as p2p_senderusers_365d,
  count(
    distinct case when report_date >= concat(substr('${bizdate}', 1, 6), '01')
    and report_date <= '${bizdate}'
    and peer_type = 'sender' then gcash_wallet else null end
  ) as p2p_senderusers_mtd,
  count(
    distinct case when report_date >= concat(substr('${bizdate}', 1, 4), '0101')
    and report_date <= '${bizdate}'
    and peer_type = 'sender' then gcash_wallet else null end
  ) as p2p_senderusers_ytd 

--P2P Receiver Users
  
  ,count(
    distinct case when report_date = '${bizdate}'
    and peer_type = 'receiver' then gcash_wallet else null end
  ) as p2p_receiverusers_1d,
  count(
    distinct case when report_date > to_char(
      dateadd(to_date('${bizdate}', 'yyyymmdd'), -30, 'dd'),
      'yyyymmdd'
    )
    and report_date <= '${bizdate}'
    and peer_type = 'receiver' then gcash_wallet else null end
  ) as p2p_receiverusers_30d,
  count(
    distinct case when report_date > to_char(
      dateadd(to_date('${bizdate}', 'yyyymmdd'), -365, 'dd'),
      'yyyymmdd'
    )
    and report_date <= '${bizdate}'
    and peer_type = 'receiver' then gcash_wallet else null end
  ) as p2p_receiverusers_365d,
  count(
    distinct case when report_date >= concat(substr('${bizdate}', 1, 6), '01')
    and report_date <= '${bizdate}'
    and peer_type = 'receiver' then gcash_wallet else null end
  ) as p2p_receiverusers_mtd,
  count(
    distinct case when report_date >= concat(substr('${bizdate}', 1, 4), '0101')
    and report_date <= '${bizdate}'
    and peer_type = 'receiver' then gcash_wallet else null end
  ) as p2p_receiverusers_ytd 

--P2P Transaction Count

  ,sum(
    case when report_date = '${bizdate}'
    and peer_type = 'sender' then txncnt_1d else 0 end
  ) as p2p_txncnt_1d,
  sum(
    case when report_date > to_char(
      dateadd(to_date('${bizdate}', 'yyyymmdd'), -30, 'dd'),
      'yyyymmdd'
    )
    and report_date <= '@@{yyyyMMdd}'
    and peer_type = 'sender' then txncnt_1d else 0 end
  ) as p2p_txncnt_30d,
  sum(
    case when report_date > to_char(
      dateadd(to_date('${bizdate}', 'yyyymmdd'), -365, 'dd'),
      'yyyymmdd'
    )
    and report_date <= '@@{yyyyMMdd}'
    and peer_type = 'sender' then txncnt_1d else 0 end
  ) as p2p_txncnt_365d,
  sum(
    case when report_date >= concat(substr('${bizdate}', 1, 6), '01')
    and report_date <= '${bizdate}'
    and peer_type = 'sender' then txncnt_1d else 0 end
  ) as p2p_txncnt_mtd,
  sum(
    case when report_date >= concat(substr('${bizdate}', 1, 4), '0101')
    and report_date <= '${bizdate}'
    and peer_type = 'sender' then txncnt_1d else 0 end
  ) as p2p_txncnt_ytd 
  
--P2P Transaction Amount

  ,sum(
    case when report_date = '${bizdate}'
    and peer_type = 'sender' then txnamt_1d else 0 end
  ) as p2p_txnamt_1d,
  sum(
    case when report_date > to_char(
      dateadd(to_date('${bizdate}', 'yyyymmdd'), -30, 'dd'),
      'yyyymmdd'
    )
    and report_date <= '${bizdate}'
    and peer_type = 'sender' then txnamt_1d else 0 end
  ) as p2p_txnamt_30d,
  sum(
    case when report_date > to_char(
      dateadd(to_date('${bizdate}', 'yyyymmdd'), -365, 'dd'),
      'yyyymmdd'
    )
    and report_date <= '${bizdate}'
    and peer_type = 'sender' then txnamt_1d else 0 end
  ) as p2p_txnamt_365d,
  sum(
    case when report_date >= concat(substr('${bizdate}', 1, 6), '01')
    and report_date <= '${bizdate}'
    and peer_type = 'sender' then txnamt_1d else 0 end
  ) as p2p_txnamt_mtd,
  sum(
    case when report_date >= concat(substr('${bizdate}', 1, 4), '0101')
    and report_date <= '${bizdate}'
    and peer_type = 'sender' then txnamt_1d else 0 end
  ) as p2p_txnamt_ytdfrom dws_evt_trd_transfer_wallet_dswhere report_date > to_char(
    dateadd(to_date('${bizdate}', 'yyyymmdd'), -365, 'dd'),
    'yyyymmdd'
  )
  and report_date <= '${bizdate}';
```
