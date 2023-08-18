# Quicksight

## Operational Characteristics

- Cost
    - Amazon QuickSight has two different editions for pricing; standard edition and enterprise edition. 
    - Pricing is based on an annual subscription. 
    - Both standard and enterprise editions include SPICE (Super-fast, Parallel, and In-memory Calculation Engine) capacity, and you can get additional SPICE capacity for a monthly add on cost. 
    - Month to month billing options are available for both the editions.
- Performance
    - Amazon QuickSight is built with SPICE. Built from the ground up for the cloud.
    - SPICE uses a combination of columnar storage, in-memory technologies enabled through the latest hardware innovations, and machine code generation to run interactive queries on large datasets and get rapid responses.
- Durability and availability
    - SPICE automatically replicates data for high availability and enables Amazon QuickSight to scale to hundreds of thousands of users who can all simultaneously perform fast interactive analysis across a wide variety of AWS data sources.
- Scalability & Elasticity
    - Fully managed service that auto-scales
- Interfaces: Amazon QuickSight can connect to a wide variety of data sources including:
    - flat files (CSV, TSV, CLF, ELF)
    - on-premises databases like SQL Server, MySQL, and PostgreSQL
    - AWS data sources including Amazon RDS, Amazon Aurora, Amazon Redshift, Amazon Athena and Amazon S3
    - SaaS applications like Salesforce. 
    - You can also export analyzes from a visual to a file with CSV format.

> Quicksight is integrated with CloudTrail, so all events including non-API events such as deleting dashboards can be stored through CloudTrail into S3.

## Reader Sessions

- Amazon QuickSight Reader sessions are of 30-minute duration each. Each session is charged at $0.30 with maximum charges of $5 per Reader in a month.
- A Reader session starts with a user-initiated action (e.g., login, dashboard load, page refresh, drill-down or filtering) and runs for next 30-minutes. 
- Keeping Amazon QuickSight open in a background browser window/tab does not result in active sessions until the Reader initiates action on page.
- Readers will only be logged out of QuickSight when their authentication expires, which is dependent on the authentication scheme in place (can be one of QuickSight-only users, SAML/Open ID Connect or Active Directory).
- A reader will be charged $0.30 a session up to a maximum of $5/month, after which the reader can access QuickSight at no charge for additional sessions.

## Supported Visualizations

Amazon QuickSight supports assorted visualizations that facilitate different analytical approaches:

|Category|Charts|
|--------|------|
|Comparison and distribution|Bar charts (several assorted variants)|
|Changes over time|Line graphs, Area line charts|
|Correlation|Scatter plots, Heat maps|
|Aggregation|Pie graphs, Tree maps|
|Tabular|Pivot tables|
|show differences in data values across a geographical map|Geo-spatial charts (maps)|
|KPIs|Comparison between a key-value and it's target value|

## Kibana

Kibana is built into Amazon ES.

## Active Directory Integration

> Amazon QuickSight Enterprise edition supports both AWS Directory Service for Microsoft Active Directory and Active Directory Connector. Standard Edition does not support AD Connector.

## Authentication

- Amazon QuickSight Enterprise edition supports both _AWS Directory Service for Microsoft Active Directory_ and _Active Directory Connector_.


## Encryption

 > In Amazon QuickSight Enterprise edition, the data at rest in SPICE is encrypted using block-level encryption with AWS-managed keys. You cannot use customer-provided keys that are imported into AWS KMS.

## S3 Integration
- Datasets created using Amazon S3 as the data source are automatically imported into SPICE. 
- The Amazon QuickSight console allows for the refresh of SPICE data on a schedule.
