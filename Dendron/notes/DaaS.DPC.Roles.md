---
id: f5u3wlzr954m7wwwyxqf1oa
title: DPC - Roles
desc: ''
updated: 1661337373214
created: 1661335997215
---
1. ## Data Analyst
    - simple data-preprocessing flexible query
    - data analysis using flexible query
    - report genetayion
    - business operation with processed data synchronized from business system.
    1. Data analysis tool ^dataAnalysisTool
        - Multidimensional Data Analysis
        - support [[OLAP|DaaS.OLAP]] operations
            - rotating, slicing, drilling data
    2. Data query tool
        - Data exploration via [[SQL|SQL]].
        - Support Smart Tips and Error Correction for codes.
        - Offline and Online Query.
2. ## ETL Engineer
    - Design job (online or offline)
        - Data Integration
        - Data Monitor
        - Data Maintenance
    1. ETL Tool:
        - Extracting, transforming, and loading data
            - from bottom-layer platform
        - generate highly-efficient processing program
    2. Scheduling Tool:
        - scheduling of background tasks
            - e.g. (ETL, data quality, reports, etc.)
        - **users can directly deploy customized tasks.**
3. ## Data Scientist
    - design, deploy, and optimize data mining models
        - based on data modelling tool
    1. Data mining Tool
        - [[ODPS|DaaS.ODPS]]-based algorithm framework
        - multiple data algorithms
        - algorithm experiment as building blocks
            - linkning assembly with different UI settings
            - set parameters
        - process of mining operations to deployment from:
            - model training
            - model assessment
            - model prediction
4. ## Data Consumer
    - reports through browser, desktop, or mobile device.
    1. Data Analysis Tool: ![[DaaS.DPC.Roles#^dataAnalysisTool]]
    2. Indicators and Reporting tool:
        - statistical indicators
        - unitized report management
        - dashboard design
        - embedding of browser-based reports
        - achieve objectives of design at one place
        - management at one place
        - usage at multiple places