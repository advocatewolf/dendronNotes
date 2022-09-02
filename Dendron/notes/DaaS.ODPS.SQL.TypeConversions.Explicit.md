---
id: lyngblomultsqovtygkiipn
title: Explicit Type Conversion
desc: ''
updated: 1661411651830
created: 1661407165806
---
# Explicit Type Conversion
- An explicit conversion uses the [[cast|DaaS.ODPS.SQL.BuiltInFunctions.cast]] function to convert the data type of a value. The following table describes the rules of explicit conversions supported by MaxCompute SQL.

![SQL-Explicit-Type Conversions](/assets/images/2022-08-25-13-54-41.png)

From/To | **BIGINT** | **DOUBLE** | **STRING** | **DATETIME** | **BOOLEAN** | **DECIMAL** | **FLOAT**
--------|--------|--------|--------|----------|---------|---------|------
BIGINT | N/A | Y | Y | N | Y | Y | Y
DOUBLE | Y | N/A | Y | N | Y | Y | Y
STRING | Y | Y | N/A | Y | Y | Y | Y
DATETIME | N | N | Y | N/A | N | N | N
BOOLEAN | Y | Y | Y | N | N/A | Y | Y
DECIMAL | Y | Y | Y | N | Y | N/A | Y
FLOAT | Y | Y | Y | N | Y | Y | N/A

## Example

```
SELECT CAST(user_id AS DOUBLE) AS new_id;
SELECT CAST('2015-10-01 00:00:00' AS DATETIME) AS new_date;
SELECT CAST(ARRAY(1,2,3) AS ARRAY<STRING>);
SELECT CONCAT_WS(',', CAST(ARRAY(1, 2) AS ARRAY<STRING>));
```
![](/assets/images/2022-08-25-14-36-17.png)

## Notes


- If a value of the **DOUBLE** type is converted into that of the **BIGINT** type, digits after the decimal point are removed. For example, you can execute 
    - `CAST(1.6 AS BIGINT) = 1` to convert **1.6** of the **DOUBLE **Type to **1** of the **BIGINT** type.
- If a value of the **STRING** type that meets the format of the **DOUBLE** type is converted into the **BIGINT** type, the **STRING** type is first converted into the **DOUBLE** type and then to the **BIGINT** type. 
    - During the conversion, the digits after the decimal point are removed. For example, you can execute 
        - `CAST("1.6" AS BIGINT) = 1` to convert **1.6** of the **STRING** type to **1** of the** **BIGINT**** type.
- If a value of the **STRING** type that meets the format of the **BIGINT** type is converted into the **DOUBLE** type, one digit is retained after the decimal point. For example, you can execute 
    - `CAST("1" AS DOUBLE) = 1.0 to convert 1` of the **STRING** type to **1.0** of the **DOUBLE** type.
- The default format `yyyy-mm-dd hh:mi:ss` is used during the conversion that involves the **DATETIME** type.
- Some data types cannot be explicitly converted, but can be converted by using SQL built-in functions. 
    - For example, you can use the [[TO_CHAR|DaaS.ODPS.SQL.BuiltInFunctions.TO_CHAR]] function to convert the **BOOLEAN** type into the **STRING** type. For more information. . 
    - You can also use the [[TO_DATE|DaaS.ODPS.SQL.BuiltInFunctions.TO_DATE]] function to convert the **STRING** type into the **DATETIME** type. For more information.
- If the value of the **DECIMAL** type exceeds its value range, the `CAST STRING TO DECIMAL` operation may cause errors, such as overflow of the most significant bit or removal of the least significant bit.
- A conversion from the **DECIMAL** type to the **DOUBLE** or **FLOAT** type results in a loss of precision. In scenarios where high precision is required, for example, 
    - when you calculate the bill amount or premium rate, we recommend that you retain the **DECIMAL** type.
- MaxCompute allows you to convert complex data types. 
    - Implicit conversions between complex data types can be implemented only when their subtypes support implicit conversions. 
    - Explicit conversions between complex data types can be implemented only when their subtypes support explicit conversions. 
    - If you convert the **STRUCT** type, field names can be inconsistent, but the number of fields must be consistent and these fields must support implicit or explicit conversions. Examples:
        - `ARRAY<BIGINT>` can be implicitly or explicitly converted to `ARRAY<STRING>`.
        - `ARRAY<BIGINT>` can be explicitly converted to `ARRAY<INT>`. Implicit conversions are not supported.
        - `ARRAY<BIGINT>` cannot be implicitly or explicitly converted to `ARRAY<DATETIME>`.
        - `STRUCT<a:BIGINT,b:INT>` can be implicitly converted to `STRUCT<col1:STRING,col2:BIGINT>`. Implicit or explicit conversions to `STRUCT<a:STRING>` are not supported.

for [[Implicit Conversions|DaaS.ODPS.SQL.TypeConversions.Implicit]]