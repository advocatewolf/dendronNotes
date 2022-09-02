---
id: egvqmb9kl3cj5yz6daq6bb7
title: OPDS-architecture
desc: ''
updated: 1661395677055
created: 1661395168824
---
![ODPS-Architecture](/assets/images/2022-08-25-10-39-47.png)

## Apsara (Bottom Layer)
- storage data
- service management
- object deployment
- object management
- object monitor
- object security

## Functions
- SQL
    - ODPS SQL, a subset of standard SQL
    - no database characteristics, e.g. transaction, primary key constraints, index, etc.
- Xlib
    - supports data mining algorithm
    - dispatched by system together with SQL and MapReduce
    - focus on statistics analysis, and machine learning algorithm
- MapReduce
    - Java API for processing data in ODPS
        - e.g., data platform use MR to upload wallet detail data to PayTM
- Graph
    - directed graph, composed of vertices and edges
    - two-dimensional table only


    