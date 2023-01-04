# Storage

- Operational Data Store (OLTP Data Store): 
    - Row store, 
    - low latency, 
    - High Throughput, 
    - Concurrent, 
    - High Velocity, 
    - Caching
- Analytical Data Store: Divided into OLAP and Decision Support System (DSS). 
    - Columnar store
    - Large data sets, Partioned
    - Large Compute Size
    - Regularly performs complex joins and aggregations
    - Bulk Loading or Trickle Inserts
    - Low Change Velocity
- OLAP: OLAP systems provide a more responsive framework for real-time feedback and ad-hoc queries. 
- DSS Systems: DSS systems, such as data lakes and data warehouses, are useful for long-running query aggregations and projections, where latency is less important.


## OLTP stores

- RDS: Scales vertically. Reliable and durable: Multi-AZ and automated backups, snapshots, and failover.
- DynamoDB: Scales horizontally. Reliable and durable. Offers *global tables* for multi-region replication.
- ElastiCache: Extreme performance. ElastiCache for Redis offers multi-az storage with automatic failover.
- Neptune: Fast and scalable (billions of relationships & queries with milliseconds latency). Six replicas of data across three AZ. 

## Analytic

- S3: Object store, fast & reliable platform to store and query structured and semi-structured data. Athena & Redshift can read from S3. Reliable and Durable (data replicated across 3 AZ, except for single AZ storage class), cross-region replication.
- Redshift: Columnar storage to improve I/O efficiency and parallelize queries. Data loads linearly. Fastest query results with higher storage cost. Reliable and durable: Continuously backs up your data to S3 (11 9s of durability)   

## DynamoDB

- Use DAX (DynamoDB compatible) for micro-second responses.
- Partition Key (or) Primary Key: Choose a column with high cardinality. User ID is good. Error code is bad.
- Secondary indexes: *access pattern*. hese indexes can use alternate sort and/or primary keys to match secondary access patterns. 
    - The careful design of secondary indexes allows fast and efficient access to data.
    - Can choose local or global secondary indexes.
    - LSI: Same partition key, but different sort key. Both eventual and strong. Cannot be deleted, choose when you create table.
    - GSI: Both partition and sort keys can be different. *Global* 'cos the data can span all partitions. Only eventual consistency.

### Provisioned Capacity Mode

- With provisioned capability mode, you specify the number of reads (RCUs) and writes (WCUs) per second that you expect your application to require. 
- 1 RCU represents one strongly consistent read or 2 eventually consistent reads per second for an item up to 4 KB in size. 
- 1 WCU represents one write per second for an item up to 1 KB in size. 
- You can provision any amount of throughput to a table and use auto scaling to automatically adjust your table’s capacity based on the specified utilization rate to ensure application performance while reducing costs.

### Global Tables

- Uses DynamoDB streams

> To help ensure eventual consistency, DynamoDB global tables use a last-writer-wins reconciliation between concurrent updates, in which DynamoDB makes a best effort to determine the last writer.

## Redis

- You can use Redis Hashes to maintain a list of likes & dislikes for a product code (product recommendation use case)

## S3

### S3 Select and Glacier Select

#### S3 Select

- S3 Select enables applications to retrieve only a subset of data from an object by using simple SQL expressions. 
- By using S3 Select to retrieve only the data needed by your application, you can achieve drastic performance increases (sometimes upto 400% improvement)
- Amazon Athena, Amazon Redshift, and Amazon EMR as well as partners like Cloudera, DataBricks, and Hortonworks will all support S3 Select.

#### Glacier Select

- Some companies in highly regulated industries like Financial Services, Healthcare, and others, write data directly to Amazon Glacier to satisfy compliance needs like SEC Rule 17a-4 or HIPAA. 
- Many S3 users have lifecycle policies designed to save on storage costs by moving their data into Glacier when they no longer need to access it on a regular basis. 
- Cold data stored in Glacier can now be easily queried within minutes (vis-a-vis weeks with Tape solutions).
- Glacier Select allows you to to perform filtering directly against a Glacier object using standard SQL statements.

### Glacier
- To prevent deletion in Glacier, you must use a Glacier Vault Lock Policy.
- Glacier Select allows you to perform filtering directly against Glacier objects using standard SQL statements. It is the simplest, quickest, and most cost-effective option for querying cold data stored in Glacier.

### Encryption

### SSE-KMS

- When you create an object, you can specify the use of server-side encryption with AWS Key Management Service (AWS KMS) keys to encrypt your data. This encryption is known as SSE-KMS. 
- You can apply encryption when you are either uploading a new object or copying an existing object.
- SSE-KMS will allow you to use different KMS keys to encrypt the objects, and then you can grant users access to specific sets of KMS keys to give them access to the objects in S3 they should be able to decrypt.

> If you want to allow multiple users to decrypt and use different sets of objects (per each user), go with SSE-KMS and specific
> SSE-KMS key per each of these sets of objects. A bucket policy becomes complex in this case.

### Large Files

- To validate checksum of upload of large files, use thw S3 ETag (sent in the response) against the local MD5 hash.

## Redshift

### Storage Options

- While Amazon RDS, DynamoDB, and Neptune are all built in SSDs, Amazon Redshift offers you a choice of **SSD** or **HDD** storage. 
- Amazon Redshift offers three different node types to best accommodate your workloads. You can select *RA3*, *DC2*, or *DS2*, depending on your required performance and data size.
    - DC2: Compute Intensive with local SSD
    - DS2: Legacy, uses HDD for lower cost, not recommended
    - RA3: with managed storage, allows you to optimize your datawarehouse by scaling and paying for compute and storage independently. 

### Workload Management (WLM)

- You can use workload management (WLM) to define multiple query queues and to route queries to the appropriate queues at runtime.
-  For example, suppose that one group of users submits occasional complex, long-running queries that select and sort rows from several large tables. Another group frequently submits short queries that select only a few rows from one or two tables and run in a few seconds. In this situation, the short-running queries might have to wait in a queue for a long-running query to complete. 
- WLM helps manage this situation by pushing these queries into separate queues.

### Short Query Acceleration (SQA)

- Short query acceleration (SQA) prioritizes selected short-running queries ahead of longer-running queries. 
- SQA runs short-running queries in a dedicated space, so that SQA queries aren't forced to wait in queues behind longer queries.
- If you enable SQA, you can reduce or eliminate workload management (WLM) queues that are dedicated to running short queries.
- In addition, long-running queries don't need to contend with short queries for slots in a queue, **so you can configure your WLM queues to use fewer query slots**.

### Resizing

- AWS generally recommends using elastic resize, assuming you can tolerate 10 minutes or so of read-only access. Elastic Resize works for both node count and type changes.
- Classic resize takes more time to complete, but it can be useful in cases where the change in node count or the node type to migrate to doesn't fall within the bounds for elastic resize. This can apply, for instance, when the change in node count is really large.

> As a general rule of thumb, choose elastic resize instead of classic resize (unless the change node count is really large).

> You can also use classic resize to change the cluster encryption. _For example, you can use it to modify your unencrypted cluster to use AWS KMS encryption_.

> To be sure that the cluster is available during a classic resize operation, copy the existing cluster.  Then, resize the new cluster. If data is written to the source cluster after a snapshot is taken, the data must be manually copied over.

#### Elastic resize: 
- If elastic resize is available as an option, use elastic resize to change the node type, number of nodes, or both. Note that when you only change the number of nodes, the queries are temporarily paused and connections are kept open. An elastic resize takes between 10-15 minutes. During a resize operation, the cluster is read-only.

#### Classic resize: 

- Use classic resize to change the node type, number of nodes, or both. Choose this option when you're resizing to a configuration that isn't available through elastic resize. A resize operation takes two hours or more, or can take up to several days depending on your data size. During the resize operation, the source cluster is read-only.


#### Snapshot, restore, and resize: 

- To be sure that the cluster is available during a classic resize operation, copy the existing cluster. Then, resize the new cluster. If data is written to the source cluster after a snapshot is taken, the data must be manually copied over. The manual data copy to the newly created target cluster must take place after the migration completes.

#### Fast Classic Resize: 

- Fast classic resize is as quick as elastic resize and functions similar to classic resize. 
- In this resize operation there are two main stages. In stage 1 (critical path), data is migrated from the source to a target cluster and the cluster is in read only mode. 
- In stage 2 (off critical path) redistributing of the data, done in the previous data distribution style, is completed in the background. The duration of this stage depends on the volume to distribute and cluster workload.

> Classic resize: Use classic resize to change the node type, number of nodes, or both.

### Copy of Data

> Amazon Redshift can automatically load in parallel from multiple compressed data files. However, if you use multiple concurrent COPY commands to load one table from multiple files, Amazon Redshift is forced to perform a serialized load. This type of load is much slower and requires a VACUUM process at the end if the table has a sort column defined. 

### Compression encodings

- Raw Encoding
- AZ64 Encoding
- Byte-Dictionary Encoding
- Delta Encoding
- LZO Encoding
- Mostly Encoding
- Runlength Encoding
- Text255 and Text32k Encodings
- Zstandard Encoding

## RDMS

- If you are working on an on-premise PostgreSQL database, you can use _DMS (Database Management Service)_ to replicate data to RDS, and offload analytical queries on it.

> If you are working with Amazon Aurora, read replicas help to offload analytical queries execution.

### Row-Level Security

- Row-Level Security for IAM users is now supported in both RDS and DynamoDB. 
- Web Identity Federation is required to allow end users to use their Federated accounts with IAM. 

## DynamoDB

- DynamoDB Streams do not have direct integration with Firehose. If you need to move data from DynamoDB to ElasticSearch, you need to involve Lambda functions in the middle. 

### WCU & RCU

- 1 WCU = 1 KB/second. _If you expect about 400 games to be written per second to your database, with each game emitting 80 KB of data, the WCU required is:_ 80 KB * 400 KB/second = 32000 WCU.
- 1 RCU = 2 eventually consistent reads per second of 4 KB. 1800 eventually consistent reads per second will require 1800 * 80/8 = 18000 RCU.
