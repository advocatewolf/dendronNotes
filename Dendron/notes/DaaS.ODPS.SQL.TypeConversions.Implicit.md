---
id: 09fvjklg4rivvsy2pk7ckrd
title: Implicit Type Conversion
desc: ''
updated: 1661411646538
created: 1661407201135
---
# Implicit Type Conversion
- An implicit conversion allows MaxCompute to automatically convert data types based on the context and predefined rules.

![SQL-Implicit-Type1 Conversions](/assets/images/2022-08-25-13-55-19.png)

From/To | BOOLEAN | TINYINT | SMALLINT | INT | BIGINT | FLOAT
--------|---------|---------|----------|-----|--------|------
BOOLEAN | Y | N | N | N | N | N
TINYINT | N | Y | Y | Y | Y | Y
SMALLINT | N | N | Y | Y | Y | Y
INT | N | N | Y | Y | Y | Y
BIGINT | N | N | N | N | Y | Y
FLOAT | N | N | N | N | Y | Y

![SQL-Implicit-Type2 Conversions](/assets/images/2022-08-25-13-56-33.png)

From/To | DOUBLE | DECIMAL | STRING | VARCHAR | TIMESTAMP | BINARY
--------|--------|---------|--------|---------|-----------|-------
DOUBLE | Y | Y | Y | Y | N | N
DECIMAL | N | Y | Y | Y | N | N
STRING | Y | Y | Y | Y | N | N
VARCHAR | Y | Y | N | N | N/A | N/A
TIMESTAMP | N | N | Y | Y | Y | N
BINARY | N | N | N | N | N | Y

### Note:

- MaxCompute V2.0 introduces the methods to define constants of the DECIMAL and DATETIME types. For example, 100BD indicates value 100 of the DECIMAL type. 2017-11-11 00:00:00 indicates a constant of the DATETIME type. Constants can be directly defined in the VALUES clauses and tables.
- If an implicit conversion is used, MaxCompute automatically converts data types based on context. If the types do not match, you can use the CAST function to explicitly convert data types.
- Implicit conversion rules apply to specific scopes. In specific scenarios, only part of the rules take effect.


### Example:
`SELECT user_id+age+'12345', CONCAT(user_name,user_id,age `

`FROM user;`

![](/assets/images/2022-08-25-14-51-16.png)

## Notes:
- Implicit conversions of unsupported types may cause an error.
- If a conversion fails during execution, an exception occurs.
- MaxCompute automatically performs implicit conversions based on the context environment.
- We recommend that you use [[cast|DaaS.ODPS.SQL.BuiltInFunctions.cast]] to perform an explicit conversion when the types do not
- match.
- Implicit conversion rules are applicable to a specific range of scopes. In some scopes, only
- some rules can take effect.