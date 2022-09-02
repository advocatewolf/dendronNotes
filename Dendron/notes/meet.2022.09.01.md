---
id: vajnvb98jrth2mzu9bblrss
title: 'Intro for DaaS Data Protect Project'
desc: ''
updated: 1662023837831
created: 1662019515375
traitIds:
  - meetingNote
---

## Attendees
- @christianDominic
- @amielLabana
- @ralphNono

<!-- Meeting attendees. If you prefix users with an '@', you can then optionally click Ctrl+Enter to create a note for that user. -->

## Goals
Introduce DaaS Data Protect Project to new members, @ralphNono and @christianDominic by @amielLabana.
<!-- Main objectives of the meeting -->

## Agenda
- Introduction to GCASH/MYNT Organization
  - Technology
    - EASI
      - Data Governance
        - Data Steward
        - Data Protect
      - DE (Data Engineer) @johnArcenal
        - work closely
  - CI&A
    - BA (Business Analytics)
      - for reports
    - DA (Data Analytics)
  - AA (Advanced Analytics)
    - Data Modelling work

### Data Protect
  - Data from Data Warehouse refer to [[Data Asset|DaaS.dataAsset]]
  - Extract Task (data source from oceanbase for example)
    - Each job has a script
      - each script has query
  - Objective:
  1. [[identify and classify all data entering DaaS|#^dataProfiling]]
  1. Sensitive data should be hashed or masked based on MISG & DP.
  1. Enable and configure security center in DaaS/DataWorks for column level access control
  1. review data (table & column) access of Daas
  1. hand-over DSG to

  - Example:
    - using RegEx to check patterns
    - using Python to automate pattern checking
      - e.g. returns "50% of data in this column is PII"
#### - Current  
  - Data desentisization
    - no hashing or masking
  - Trace Leak Source
    - no data watermarking
      - if data leak happens, hard to trace source.
  - Data Access Control
    - not user-friendly
  - Data Auditing
    - review if user still needs the role with IS
  - Identify sensitive data
    - No idetification or classification of sensitive data
  - Monitor Data risks
    - no rules configured

#### - FUTURE
  - continous monitoring 
### DataWorks
  - web-based IDE similar but better to DaaS
  - focus on Data Security Guard (DSG)

#### - Data Profiling^dataProfiling
  - ODS 
  - regex to identtify for PII(Personal Identification Information) or SPI(Sensitie Personal Information)
  - Focus on ODS layer (mostly KYC) for checking of Sensitive Data
    - KYC (Know Your Custome/Client)
      - KYC8 (aggregated)
      - KYC9 (separated)
<!-- Agenda to be covered in the meeting -->

#### SQL Example
  - if partition, always use `dt = @@{yyyyMMdd}`
  **- desc <table_name>**
## Minutes
- GCASH/MYNT Organization (00:00 - 10:00)
- Data Governance (10:00~)
- Data Protect (10:15~)
- DataWorks Interface (20:00~)
- Data profiling (26:30~)
- Query Example (39:30~)
<!-- Notes of discussion occurring during the meeting -->

## Action Items

<!-- You can add any follow up items here. If they require more detail, you can use `Create Task Note` to create each follow up item as a separate note. -->

- Follow Up Task 1
- Follow Up Task 2
