# Amazon EMR

## Apache Ranger on EMR

> Apache Ranger is a role-based access control framework to enable, monitor, and manage comprehensive data security across the Hadoop platform. 

### Key Characteristics

- Centralized security administration and auditing
- Fine-grained authorization across many Hadoop components (Hadoop, Hive, HBase, Storm, Knox, Solr, Kafka, and YARN)
- Syncs policies and users by using agents and plugins that run within the same process as the Hadoop component
- Supports row-level authentication and auditing capabilities with embedded search.

## Amazon EMR & Events

- You can now respond to Amazon EMR cluster state changes with Amazon CloudWatch Events. 
- The new Amazon EMR event types in Amazon CloudWatch Events provide information including state and related severity for Amazon EMR clusters, instance groups, steps, and Auto Scaling policies.

## EMRFS

- EMRFS uses an Amazon DynamoDB database to store object metadata and track consistency in Amazon S3
- EMRFS allows you to define retry rules for processing inconsistencies

> With the release of Amazon S3 strong read-after-write consistency on December 1, 2020, you no longer need to use EMRFS consistent view (EMRFS CV) with your Amazon EMR clusters.

## Notifications

Amazon EMR can only be configured as a publisher to an SNS topic—it cannot subscribe to notifications.

## High Availability

- Amazon EMR supports multiple master nodes to enable high availability for EMR applications. 
- Launch an EMR cluster with three master nodes and support high availability applications like YARN Resource Manager, HDFS Name Node, Spark, Hive, and Ganglia. 
- _EMR clusters with multiple master nodes are not tolerant of Availability Zone failures. In the case of an Availability Zone outage, you lose access to the EMR cluster._
- Using the Amazon EMR version 5.7.0 or later, you can set up a read-replica cluster, which allows you to maintain read-only copies of data in Amazon S3. In the event that the primary cluster becomes unavailable, you can access the data from the read-replica cluster to perform read operations simultaneously.

## Metastore

Using Amazon EMR version 5.8.0 or later, you can configure Hive to use the AWS Glue Data Catalog as its metastore. This configuration is recommended if the metastore is shared by different clusters.