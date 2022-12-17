# Storage

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

- Classic resize with snapshot / restore / resize minimizes the downtime involved (vis-a-vis Elastic Resize)
- Elastic resize only holds connections open if you only change the number of nodes, not the node type. 
- AWS generally recommends using elastic resize however, assuming you can tolerate 10 minutes or so of read-only access.

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

## RDMS

- If you are working on an on-premise PostgreSQL database, you can use _DMS (Database Management Service)_ to replicate data to RDS, and offload analytical queries on it.

> If you are working with Amazon Aurora, read replicas help to offload analytical queries execution.

## DynamoDB

- DynamoDB Streams do not have direct integration with Firehose. If you need to move data from DynamoDB to ElasticSearch, you need to involve Lambda functions in the middle. 
