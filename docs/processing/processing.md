# Processing

## EMR

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
- LUKS Encryption
- KMS Encryption

### Keep Redshift and RDS in sync

- Materialized View. The disadvantage of the materialized view is that refreshes copy all of the data from the beginning.
- DB Link functionality to copy data from Redshift to RDS. _DB Link is a feature in PostgreSQL that executes query in a remote database._


## References

- [Best Practices for securing EMR](https://aws.amazon.com/blogs/big-data/best-practices-for-securing-amazon-emr/)
- [EMR - What's New?](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-whatsnew.html)