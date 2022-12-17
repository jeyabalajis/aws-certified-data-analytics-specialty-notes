# Collection

## Ongoing collection

- If the data streams must be stored for _at least 3 days_, you must use Kinesis Data Streams which has a configurable data retention of between 1 and 365 days.
- The KPL has the mechanisms in place for retry and batching, as well as asynchronous mode. 
- The Kinesis agent is meant to retrieve server logs with just configuration files.
- Lambda can be a consumer for Kinesis Data Streams (KDS) but not for Kinesis Data Firehose (KDF). However, for transformation needs, Lambda can be used in conjunction with KDF.

### Kinesis Data Streams

- KDS with provisioned capacity does not scale as the load increases. 
- With on-demand scaling, KDS can be used for scaling with increasing data, but if the processing times are in minutes (not seconds), a different approach (such as SQS) could be required.
- For ongoing data collection and when configurable data retention is required, choose _Kinesis Data Streams_ over _Kinesis Data Firehose_.

### Kinesis Data Firehose

- Using KDF, data can be sinked into S3, Redshift, ElasticSearch or Splunk.
- 
