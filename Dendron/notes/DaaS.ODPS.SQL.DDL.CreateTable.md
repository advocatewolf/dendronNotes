---
id: 76a87p76ki92jlvfxt8loie
title: Create Table
desc: ''
updated: 1661417860160
created: 1661417389612
---
[ref.](https://www.alibabacloud.com/help/en/maxcompute/latest/ddl-sql-table-operations#section-ixi-bgd-948)
```
-- Create a table. 
 create [external] table [if not exists] <table_name>
 [(<col_name> <data_type> [not null] [default <default_value>] [comment <col_comment>], ...)]
 [comment <table_comment>]
 [partitioned by (<col_name> <data_type> [comment <col_comment>], ...)]
 -- Configure the shuffle and sort properties of a clustered table that you want to create. 
 [clustered by | range clustered by (<col_name> [, <col_name>, ...]) [sorted by (<col_name> [asc | desc] [, <col_name> [asc | desc] ...])] into <number_of_buckets> buckets] 
 -- Used only for external tables. 
 [stored by StorageHandler] 
 -- Used only for external tables. 
 [with serdeproperties (options)] 
 -- Used only for external tables. 
 [location <osslocation>] 
 -- Set the table to a transactional table. You can later modify or delete the data of the transactional table. Transactional tables have specific limits. Create a transactional table base on your business requirements. 
 [tblproperties("transactional"="true")]   
 [lifecycle <days>];

-- Create a table based on an existing table and replicate data from the existing table to the new table. Partition properties are not replicated. 
create table [if not exists] <table_name> [lifecycle <days>] as <select_statement>;

-- Create a table that has the same schema as an existing table. Data in the existing table is not replicated. 
create table [if not exists] <table_name> like <existing_table_name> [lifecycle <days>];
```


## Other Table?

```
create table if not exists dwd_evt_trd_core_trans_adjustment_di_testing
(
log_id STRING comment 'log id,concat with created with yyyymm formart a
nd transid'
,modify_id string comment 'modify id concat gmt_modified converted into yy
yymm format and trans_id'
,trans_id STRING comment 'core transaction id'
,trans_type STRING comment 'trans type'
,gmt_create STRING comment 'transaction create time'
,gmt_modified STRING comment 'transaction modify time'
,status_code STRING comment 'transaction status code'
,status_desc STRING comment 'transaction status description'
,channel_code STRING comment 'transaction channel code'
,channel_desc STRING comment 'transaction channel description'
,initiator_agentid STRING comment 'initiator agent id'
,initiator_msisdn STRING comment 'initiator msisdn'
,initiator_mothers_maiden_name STRING comment 'initiator mothers_maiden_n
ame'
,trans_amount DECIMAL comment 'transaction amount'
,src_agentid STRING comment 'source agent id'
,src_accountid STRING comment 'source account id'
,src_msisdn STRING comment 'source msisdn'
,src_mothers_maiden_name STRING comment 'source mothers_maiden_name'
,src_begin DECIMAL comment 'source begin balance'
,src_end DECIMAL comment 'source end balance'
,src_typecode STRING comment 'source type code'
,src_caplist STRING comment 'source caps list'
,tgt_agentid STRING comment 'target agent id'
,tgt_accountid STRING comment 'target account id'
,tgt_msisdn STRING comment 'target msisdn'
,tgt_mothers_maiden_name STRING comment 'target mothers_maiden_name'
,tgt_begin DECIMAL comment 'target begin balance'
,tgt_end DECIMAL comment 'target end balance'
,tgt_typecode STRING comment 'target type code'
,tgt_caplist STRING comment 'target caps list'
,description STRING comment 'description'
,result_namespace STRING comment 'result namespace'
,result_code STRING comment 'result'
,result_name string comment 'transaction result name'
,result_desc string comment 'transaction result description'
,child_order STRING comment 'child order'
,batchid STRING comment 'batch id'
,parent STRING comment 'parent transid'
,trans_group STRING comment 'trans group'
,business_trans_id STRING comment 'business trans id'
,business_trans_date STRING comment 'business trans date'
,filter STRING comment 'td_key=filter'
,channel STRING comment 'td_key=channel'
,trans_ext_reference STRING comment 'td_key=trans_ext_reference'
,confirmation_rule STRING comment 'td_key=confirmation_rule'
,voucher_number STRING comment 'td_key=voucher_number'
,__is_batch_rollback STRING comment 'td_key=__is_batch_rollback'
,_globetranflag STRING comment 'td_key=_globetranflag'
,_uTrustCapFlgPre STRING comment 'td_key=_uTrustCapFlgPre'
,_uTrustCapsFlag STRING comment 'td_key=_uTrustCapsFlag'
,key_batchId STRING comment 'td_key=batchId'
,category STRING comment 'td_key=batchId'
,key_description STRING comment 'td_key=description'
,key_details STRING comment 'td_key=details'
,failed_line STRING comment 'td_key=failed_line'
,message STRING comment 'td_key=message'
,suppress_confirm STRING comment 'td_key=suppress_confirm'
,suppress_sms STRING comment 'td_key=suppress_sms'
,details STRING comment 'details,from td_key=description'
)
COMMENT 'core trans base for adjustment trans_type'
PARTITIONED BY (dt STRING COMMENT 'date，yyyymmdd format')
LIFECYCLE 36500;
```
