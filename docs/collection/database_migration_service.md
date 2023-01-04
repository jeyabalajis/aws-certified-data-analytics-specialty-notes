# Database Migration Service

> AWS DMS provides one-time migration and continuous replication of your database records and data structures to AWS.

AWS Database Migration Service (AWS DMS) can be used to migrate data 
- from your database that is 
    - on-premises, 
    - on an Amazon Relational Database Service (Amazon RDS) DB instance, 
    - or in a database on an Amazon Elastic Compute Cloud (Amazon EC2) instance 
- to a database on an AWS service.

With AWS DMS, you can create a task that captures ongoing changes after you complete your initial migration to a supported target data store. This process is called ongoing replication or change data capture (CDC). 

## Scalability

- AWS DMS uses Amazon EC2 instances as the replication instance. 
- You can scale up or down your replication instance, depending on utilization.
- You have the option of enabling Multi-AZ which provides a replication stream that is fault-tolerant through redundant replication servers.

## Sources and Targets

### Sources

- Oracle
- Microsoft
- MySQL
- PostgreSQL
- IBM DB2
- MongoDB
- Document DB
- SAP ASE

### Targets

- DynamoDB
- S3
- Kinesis Data Streams
- Apache Kafka
- Document DB
- Neptune
- Redis
- Babelfish

## From RDBMS to S3

- The solution streams new and changed data into Amazon S3 using AWS Database Migration Service (AWS DMS). 
- It reads historical data from source systems, such as relational database management systems, data warehouses, and NoSQL databases, at any desired interval. 
- The solution streams new and changed data into Amazon S3.