---
id: okfv45c3g2twb7dbv0sfb5r
title: MAPJOIN
desc: ''
updated: 1662019064750
created: 1661482442428
---
[ref.](https://www.alibabacloud.com/help/en/maxcompute/latest/mapjoin-hints)

### Usage Notes^usage
- You can execute `MAPJOIN` only after you add the `/*+ mapjoin(<table_name>) */` hint to a `SELECT` statement.
    - when you reference a small table or a subquery, you must reference the alias of the table or subquery.
    - you can use subqueries as small tables.
    - you can use non-equi joins or combin conditions by using `OR`.
        - calculate Cartesian product by using `MAPJOIN` `ON` `1 =1` without using the `ON`condition, e.g. `select /*+ mapjoin(a) */a.id from shop a join table_name b 1=1;`
            - this calculation method may increase the data volume.
    - Separate multiple small tables in `MAPJOIN` with commas (,), e.g., `/*+ mapjoin(a,b,c)*/`


#### EXAMPLES^examples

Perform `JOIN` operations on the `sale_detail` and the `sale_detail_sj` tables. 

The operations must meet one of the following conditions: 
1. The total values of the total_price column in the `sale_detail_sj` table are less than the total values of the total_price column in the `sale_detail` table. 
2. The sum of values of the total_price column in the `sale_detail_sj` table and values of the total_price column in the `sale_detail` table is less than 500. 

```
select /*+ mapjoin(a) */
        a.shop_name,
        a.total_price,
        b.total_price
from sale_detail_sj a join sale_detail b
on a.total_price < b.total_price or a.total_price + b.total_price < 500;
```
shop_name | total_price | total_price2 
----------|-------------|--------------
s1 | 100.1 | 100.1 | 
s2 | 100.2 | 100.1 | 
s5 | 100.2 | 100.1 | 
s2 | 100.2 | 100.1 | 
s1 | 100.1 | 100.2 | 
s2 | 100.2 | 100.2 | 
s5 | 100.2 | 100.2 | 
s2 | 100.2 | 100.2 | 
s1 | 100.1 | 100.3 | 
s2 | 100.2 | 100.3 | 
s5 | 100.2 | 100.3 | 
s2 | 100.2 | 100.3 | 
---
--Analyse the number of daily registered users distinguished by telecom_type
```
select /* +mapjoin(src_top6,src_top5,src_top4) */
to_char(reg_date,'yyyyMMdd') as reg_date
,if(lower(coalesce(src_top6.telecom_type,src_top5.telecom_type,src_top4.telecom_type)) =lower('globe'),coalesce(src_top6.telecom_type,src_top5.telecom_type,src_top4.telecom_type),'OtherNetwork') as network

,count(distinct msisdn) as msisdn
from (
select * from dwd_pty_mbr_gbase_dd
where dt='${bizdate}'
	and to_char(reg_date,'yyyyMMdd')>='@@{yyyyMMdd-14d}'
	and length(msisdn)=11
	and msisdn rlike ("^09[0-9]{9}$")
	and msisdn like '0%'
) t1

left outer join
(select *
	from dim_rsi_mob_mobileno_prefix_all
where dt='${bizdate}'
	and prefix_type='top6'
	) src_top6
on substr(t1.msisdn,1,6) = src_top6.msisdn_prefix
left outer join
(select *
	from dim_rsi_mob_mobileno_prefix_all
where dt='${bizdate}'
	and prefix_type='top5'
	) src_top5
on substr(t1.msisdn,1,5) = src_top5.msisdn_prefix
left outer join
(select *
	from dim_rsi_mob_mobileno_prefix_all
where dt='${bizdate}'
	and prefix_type='top4'
	) src_top4
on substr(t1.msisdn,1,4) = src_top4.msisdn_prefix
group by to_char(reg_date,'yyyyMMdd'),if(lower(coalesce(src_top6.telecom_type,src_top5.telecom_type,src_top4.telecom_type)) =lower('globe'),coalesce(src_top6.telecom_type,src_top5.telecom_type,src_top4.telecom_type),'OtherNetwork')
order by reg_date,network;
```