---
id: dbzu8lfi7vkzqp8xswxhcph
title: Subquery
desc: ''
updated: 1662017854529
created: 1661482425278
---
[ref.](https://www.alibabacloud.com/help/en/maxcompute/latest/subqueries)

- [[IN SUBQUERY|DaaS.ODPS.SQL.Select.Subquery.In]]
- [[NOT IN SUBQUERY|DaaS.ODPS.SQL.Select.Subquery.notIn]]
- [[EXISTS| DaaS.ODPS.SQL.Select.Subquery.Exists]]
- [[NOT EXISTS| DaaS.ODPS.SQL.Select.Subquery.NotExists]]
- [[Example|#^example]]

## Example^example
--the result will be null if the `NOT IN` subquery has NULL value.
```
select t1.*
from (
select 1 as id ,'test1' as name from dual union all
select null as id ,'unknown' as name from dual union all
select 2 as id ,'test2' as name from dual union all
select 3 as id ,'test3' as name from dual union all
select 4 as id ,'test4' as name from dual union all
select 5 as id ,'test5' as name from dual union all
select 6 as id ,'test6' as name from dual
) t1
where id not in
(select null as id from dual union all
select 1 as id from dual
);
```


--------output-------------

 id | name
----|-----
 No Data | No Data

--it will make sense by using left outer join.

```
select t1.*
from (
select 1 as id ,'test1' as name from dual union all
select null as id ,'unknown' as name from dual union all
select 2 as id ,'test2' as name from dual union all
select 3 as id ,'test3' as name from dual union all
select 4 as id ,'test4' as name from dual union all
select 5 as id ,'test5' as name from dual union all
select 6 as id ,'test6' as name from dual
) t1
left outer join
(select null as id from dual union all
select 1 as id from dual
) t2
on t1.id=t2.id
where t2.id is null;
```

--------output-------------

id | name
---|-----
4 | test4 
3 | test3 
2 | test2 
6 | test6 
\N | unknown 
5 | test5 | 





