# Kinesis Data Firehose

Amazon Kinesis Data Firehose is a fully managed service for _delivering real-time streaming data to destinations_ such as _Amazon Simple Storage Service (Amazon S3), Amazon Redshift, Amazon OpenSearch Service, Amazon OpenSearch Serverless, Splunk, and any custom HTTP endpoint or HTTP endpoints owned by supported third-party service providers, including Datadog, Dynatrace, LogicMonitor, MongoDB, New Relic, and Sumo Logic_.

- Fully managed, send to S3, Splunk, Redshift, ElasticSearch
- Serverless data transformations with Lambda
- Near real time (lowest buffer time is 1 minute)
- Automated Scaling
- No data storage

> KDF is more managed than KDS, but only near-real-time. For real-time, use KDS (but need to write custom code)

## Buffering Logic

- Firehose accumulates records in a buffer
- The buffer is flushed based on time and size rules (_lowest buffer time is 1 minute_)
- Buffer Size (ex: 32MB): if that buffer size is reached, it’s flushed
- Buffer Time (ex: 2 minutes): if that time is reached, it’s flushed
- Firehose can automatically increase the buffer size to increase throughput
    - High throughput => Buffer Size will be hit
    - Low throughput => Buffer Time will be hit

## Resilience

- Highly resilient & Serverless.
- Kinesis Data Firehose runs in a serverless mode, and takes care of host degradations, Availability Zone availability, and other infrastructure related issues by performing automatic migration.

## Record Format Conversion

- **A deserializer to read the JSON of your input data**. You can choose one of two types of deserializers: Apache Hive JSON SerDe or OpenX JSON SerDe.
- **A schema to determine how to interpret that data** – Use AWS Glue to create a schema in the AWS Glue Data Catalog. - Kinesis Data Firehose then references that schema and uses it to interpret your input data.
- **A serializer to convert the data to the target columnar storage format (Parquet or ORC)** – You can choose one of two types of serializers: ORC SerDe or Parquet SerDe.

## Streaming ETL

> Kinesis Data Firehose and Kinesis Data Analytics are integrated with AWS Lambda to perform streaming ETL.

> For sub-second analytics, KDF --> S3 --> Athena is useful. But for near-real time analytics, use KDF --> Amazon OpenSearch service (this provides near-real time analytics capability to consumers)

## Kinesis Agent

- You can install the _Kinesis Agent_ on Linux-based server environments such as web servers, log servers, and database servers. - After installing the agent, configure it by specifying the files to monitor and the delivery stream for the data. 
- After the agent is configured, it durably collects data from the files and reliably sends it to the delivery stream.

## Use Cases

- Cloud Watch Logs --> Subscription Filter --> Kinesis Data Firehose (optional Lambda Transform) --> Amazon ES/S3/Splunk

> For real time, use Lambda instead of Kinesis Data Firehose.

> For real time analytics, use Kinesis data Streams in conjunction with Kinesis Data Analytics.

## Kinesis Data Firehose to S3
- Kinesis Data Firehose can be configured with custom prefixes and dynamic partitioning. 
- Using these features, you can configure the Amazon S3 keys and set up partitioning schemes that better support your use case.
- You can also use partition projection with these partitioning schemes and configure them accordingly.

> For example, you could use the custom prefix feature to get Amazon S3 keys that have ISO formatted dates instead of the default yyyy/MM/dd/HH scheme. You can also combine custom prefixes with dynamic partitioning to extract a property like customer_id from Kinesis Data Firehose messages.