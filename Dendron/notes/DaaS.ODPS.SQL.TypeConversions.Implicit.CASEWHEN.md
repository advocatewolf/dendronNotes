---
id: mirosof7ose617d7waa7gk7
title: CASE WHEN
desc: ''
updated: 1661416059472
created: 1661415900206
---
## Rules:
- if returned values are `BIGINT` and ``DOUBLE``, convert all to `DOUBLE` type.
- if a `STRING` type exist in return types, convert all to the `STRING` type. 
    - if conversion fails, i.e. `BOOLEAN` type conversion, error is returned.
- Conversions between other types are not allowed