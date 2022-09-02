---
id: 8ink18ko3vkrd7vnvg71fwn
title: DaaS
desc: ''
updated: 1661395949423
created: 1661332511958
---
# Alipay + DaaS Solution

![Alipay + DaaS Overview](/assets/images/2022-08-24-17-22-27.png)

Starting from the Lowest Level:

## 1. Data Computing and Storage
- Central single Sstorage place named [[ODPS|DaaS_Theory.ODPS]]
- RDS, OTS, OB, OSS, MySql 
## 2. Data Integration Platform
- ETL (Extract, Transform, and Load) development framework
- Job management center
    - Organize different ETL jobs
    - Set schedule and dependency of jobs
## 3. Data Management Platform:
- [[Data Asset|DaaS.dataAsset]]
    - ADM: Data Application Layer
    - DWD: Data Asset Detail Layer, detail layer
    - DWS: Data Asset Sumarize Layer, aggregation layer
    - ODS: incremental/full scale data w/ same structure as source data
- Data Quality, auditing, and meta data.
## 4. Data Service Adaptor:
- Connection between Data Services for business user.

