---
id: j417b8lllcsgpbj15v0pkag
title: Statement
desc: ''
updated: 1661418980850
created: 1661418952950
---
```
set odps.sql.reshuffle.dynamicpt=false;
insert overwrite table dwd_evt_trd_core_trans_login_di_test partition (dt)
select
trans.created_logid as log_id
,trans.modified_logid as modify_id
,trans.trans_id
,trans.trans_type
,trans.gmt_create
,trans.gmt_modified
,trans.status_code
,trans.status_desc
,trans.channel_code
,trans.channel_desc
,trans.initiator_agentid
,trans.initiator_msisdn
,trans.initiator_mothers_maiden_name
,trans.trans_amount
,trans.src_agentid
,trans.src_accountid
,trans.src_msisdn
,trans.src_mothers_maiden_name
,trans.src_begin
,trans.src_end
,trans.src_typecode
,trans.src_caplist
,trans.tgt_agentid
,trans.tgt_accountid
,trans.tgt_msisdn
,trans.tgt_mothers_maiden_name
,trans.tgt_begin
,trans.tgt_end
,trans.tgt_typecode
,trans.tgt_caplist
,trans.description
,trans.result_namespace
,trans.result as result_code
,trans.result_name
,trans.result_desc
,trans.child_order
,trans.batchid
,trans.parent
,trans.trans_group
,trans.business_trans_id
,trans.business_trans_date
,txn_data._utrustcapsflag
,txn_data._globetranflag
,txn_data._utrustcapflgpre
,txn_data.sessionid
,txn_data.initiator
,txn_data.filter
,txn_data.confirmation_rule
,txn_data.0_notify_ws_id
,txn_data.0_notify_addr
,case when txn_data.user_agent is null and fb_login.session_id is not null
then 'Facebook' else txn_data.user_agent end as user_agent
,txn_data.app_version as app_version
,case when lower(txn_data.user_agent) like '%ios%' then 'ios' when lower(t
xn_data.user_agent) like '%android%' then 'android' else 'unkown' end as
os_type
,txn_data.phone_os_version as phone_os_version
,case when txn_data.client_ip like '%,%' then split(txn_data.client_ip,
',')[0] else txn_data.client_ip end as client_ip
,txn_data.manufacturer as manufacturer
,txn_data.phone_model as phone_model
,txn_data.udid as udid
,txn_data.phone_brand as phone_brand
,txn_data.dfp_token as dfp_token
,case when txn_data.location <> 'not_set' then split(txn_data.location,
',')[0] else cast (null as string) end as longitude
,case when txn_data.location <> 'not_set' then split(txn_data.location,
',')[1] else cast (null as string) end as latitude
,txn_data.mac_address as mac_address
,txn_data.agent_category
,txn_data.new_session_usid as new_session_usid
,to_char(gmt_create,'yyyyMMdd') as dt
from
(select *
from dwd_evt_trd_core_trans_base_full_dd
where dt='${bizdate}'
and trans_type='login'
) trans
left outer join
(select *
from dwd_evt_trd_core_trans_data_dd
where dt='${bizdate}'
) txn_data
on trans.created_logid=txn_data.log_id
left outer join
(select *
from dwd_evt_log_fb_login_dd
where dt='${bizdate}'
) fb_login
on txn_data.sessionid=fb_login.session_id and txn_data.initiator=fb_login.
msisdn
;
```