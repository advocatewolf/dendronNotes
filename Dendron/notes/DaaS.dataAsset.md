---
id: 3swkd7cejfjnxdi6fzcnp9q
title: DaaS Data Asset
desc: ''
updated: 1661396529291
created: 1661395904692
---
![Alipay + Data Flow; Data Asset](/assets/images/2022-08-25-10-52-42.png)

## Basic Layer
- store business data extracted from data source
- same table structure as business source
- Types of Extraction:
    - Incremental scale
    - Full scale
## [[Public Layer|DaaS.dataAsset.supportBusiness]]
- redesigned and reorganized data model based on data structure on basic layer
- data model meet data warehouse rule and operation
- data in business detail
- aggregated business summary
## Application Layer
- Data analysis service based on business data provided by public data
    - provided to business end user by External service, system support and operation support