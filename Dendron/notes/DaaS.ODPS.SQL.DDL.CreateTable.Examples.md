---
id: 0v9xagelo4iv79kz2xrrjta
title: Examples
desc: ''
updated: 1661417771697
created: 1661417745546
---

```
--create table
CREATE TABLE IF NOT EXISTS test_adm_glc_kpi_user_stats_ds_${UserName}
(
report_date STRING COMMENT 'report_date'
,active_type STRING COMMENT 'active_type'
,dau_count BIGINT COMMENT 'DAU'
,mau_rolling BIGINT COMMENT 'MAU(rolling 30 days)'
,aau_rolling BIGINT COMMENT 'AAU(roling 365 days)'
)
COMMENT 'GLocal KPI'
PARTITIONED BY ( dt STRING COMMENT 'date，yyyymmdd format' )
LIFECYCLE 36500
;
--create table ... as
create table test_adm_glc_kpi_user_stats_ds_${UserName}_as as
select * from test_adm_glc_kpi_user_stats_ds_${UserName};
--create table ... like
create table test_adm_glc_kpi_user_stats_ds_${UserName}_like like test_adm
_glc_kpi_user_stats_ds_${UserName};
--desc
desc test_adm_glc_kpi_user_stats_ds_${UserName};
desc test_adm_glc_kpi_user_stats_ds_${UserName}_as;
desc test_adm_glc_kpi_user_stats_ds_${UserName}_like;
--Alter the comments of a table
ALTER TABLE test_adm_glc_kpi_user_stats_ds_${UserName} SET COMMENT 'tbl co
mment:GLocal KPI';
--Add column
ALTER TABLE test_adm_glc_kpi_user_stats_ds_${UserName} ADD COLUMNS
( col_name1 string comment 'added column 1'
,col_name2 string comment 'added column 2'
);
--Modify column name
ALTER TABLE test_adm_glc_kpi_user_stats_ds_${UserName} CHANGE COLUMN col_n
ame1 RENAME TO new_col_name1;
--Rename a table
ALTER TABLE test_adm_glc_kpi_user_stats_ds_${UserName} RENAME TO new_test_
adm_glc_kpi_user_stats_ds_${UserName};
--drop table
drop table if exists test_adm_glc_kpi_user_stats_ds_${UserName};
drop table if exists new_test_adm_glc_kpi_user_stats_ds_${UserName};
drop table if exists test_adm_glc_kpi_user_stats_ds_${UserName}_as;
drop table if exists test_adm_glc_kpi_user_stats_ds_${UserName}_like;
```