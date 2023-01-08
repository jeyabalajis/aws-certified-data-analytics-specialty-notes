# Processing

## Glue

- Serverless ETL that simplifies the process of maintaining and running jobs. AWS Glue is Apache Spark-based.
- Glue can be used to connect to Athena, Redshift, and Quicksight - as well as being used as a Hive metastore.
- Hourly rate, billed by the second

## EMR

- Provides you with lower-level access to your Hadoop environment and greater flexibility in using tools beyond Spark.
- Per second + Amazon Elastic Compute Cloud (Amazon EC2). EC2 costs can be optimized by using Spot Instances for Task nodes.

### Streaming

- You can use Spark Streaming on EMR to transform data into a format that is easily storable in ElastiCache for Redis.

### EMRFS

- EMRFS provides the convenience of storing persistent data in Amazon S3 for use with Hadoop while also providing features like data encryption.
- EMR allows you use S3 instead of HDFS for HBase’s data via EMRFS.

#### Use cases for EMRFS

- Storage of HBase StoreFiles and metadata on S3
- HBase read-replicas on S3
- Snapshots of HBase data to S3

### EMR Tools

- Ganglia is the operational dashboard provided with EMR.
- Hue and Ambari are graphical front-ends for interacting with a cluster, but only Hue is provided with EMR. 
- Presto is used for querying multiple data stores at once (used by Athena).

### Ganglia

- The Ganglia open source project is a scalable, distributed system designed to monitor clusters and grids while minimizing the impact on their performance.

### Encryption

- SSE-KMS
- LUKS (Linux Unified Key Setup) Encryption: Disk encryption specification that can help encrypt sensitive data at rest.
- KMS Encryption

### Keep Redshift and RDS in sync

- Materialized View. The disadvantage of the materialized view is that refreshes copy all of the data from the beginning.
- DB Link functionality to copy data from Redshift to RDS. _DB Link is a feature in PostgreSQL that executes query in a remote database._

### EMR Auto-scaling

- The ability to scale the number of nodes in your cluster up and down on the fly is among the major features that make Amazon EMR elastic. 
- You can take advantage of scaling in EMR by resizing your cluster down when you have little or no workload. 
- You can also scale your cluster up to add processing power when the job gets too slow. 
- This allows you to spend just enough to cover the cost of your job and little more.
- Task nodes only run Hadoop tasks through YARN and DO NOT store data in HDFS. So they get decommissioned fast and hence can scale down faster.
- HDFS can take relatively longer time to decommission. This is because HDFS block replication is throttled by design through configurations located in hdfs-site.xml.
- Hence, core nodes scaling down takes longer time.

> A common automatic scaling metric for _core nodes_ is _HDFSUtilization_. Common auto scaling metrics for _task nodes_ include _ContainerPendingRatio_ and _YarnMemoryAvailablePercentage_.
> Unless you need the HDFS storage, scaling task nodes is usually a better option, and provides with more processing power.

> For core nodes, you can think of scale-out policies as easily triggered with a low cooldown and small node increments. Scale-in policies should be hard to trigger, with larger cooldowns and node increments.

## Lambda

- Provides real-time stream and file processing and is often used to replace cron jobs.
- Lambda can also be used in conjuction with Kinesis Data Streams (with event sourcing)


## References

- [Best Practices for securing EMR](https://aws.amazon.com/blogs/big-data/best-practices-for-securing-amazon-emr/)
- [EMR - What's New?](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-whatsnew.html)