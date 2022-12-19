# Kinesis Data Streams

## Kinesis Producer Library

- _RecordMaxBufferedTime_: Maximum amount of time a record is buffered. Large value provides better performance, but causes delay.

### Aggregation

- Record aggregation allows customers to combine multiple records into a single Kinesis Data Streams record. This allows customers to improve their per shard throughput.

### Collection

- Collection refers to batching multiple Kinesis Data Streams records and sending them in a single HTTP request with a call to the API operation PutRecords, instead of sending each Kinesis Data Streams record in its own HTTP request.
- KPL _aggregates_ multiple records into a single Amazon Kinesis Record, and _collects_ multiple Amazon Kinesis Records into a single _PutRecords_ API call.

## Kinesis Agent

- Kinesis Agent is a stand-alone Java software application that offers an easy way to collect and send data to Kinesis Data Streams. 
- The agent continuously monitors a set of files and sends new data to your stream. 
- The agent handles file rotation, checkpointing, and retry upon failures.
- **Kinesis Agent can send data to KDF (i.e. a delivery stream as well)**

## Kinesis Data Streams API

- If your application cannot use the KPL because it cannot incur any additional processing delay, consider using the Kinesis Data Streams API directly.
- Each PutRecords request can support up to 500 records. 
- Each record in the request can be as large as 1 MB, **up to a limit of 5 MB for the entire request**, including partition keys.
- A PutRecords request can include records with different partition keys. The scope of the request is a stream; each request may include any combination of partition keys and records up to the request limits.

> Prefer the PutRecords operation described in Adding Multiple Records with PutRecords unless your application specifically needs to always send single records per request, or some other reason PutRecords can't be used.

## Integrating with AWS Glue Schema Registry

- 

## Kinesis Consumer Library (KCL)

- KCL takes care of many of the complex tasks associated with distributed computing
- This includes the following:
    - Load balancing across multiple consumer application instances
    - Responding to consumer application instance failures
    - Checkpointing processed records, and 
    - Reacting to resharding

### KCL vs. Data Streams API

> The KCL is different from the Kinesis Data Streams APIs that are available in the AWS SDKs. The Kinesis Data Streams APIs help you manage many aspects of Kinesis Data Streams, including creating streams, resharding, and putting and getting records. 
> **The KCL provides a layer of abstraction around all these subtasks, specifically so that you can focus on your consumer application’s custom data processing logic**.

### KCL Sub Tasks

- Connects to the data stream
- Enumerates the shards within the data stream
- Uses leases to coordinates shard associations with its workers
- Instantiates a record processor for every shard it manages
- Pulls data records from the data stream
- Pushes the records to the corresponding record processor
- Checkpoints processed records
- Balances shard-worker associations (leases) when the worker instance count changes or when the data stream is resharded (shards are split or merged)

## Resilience

- **A record processor could fail.** 
    - This is handled by KCL. 
    - If you find that your application is throttled consistently, you should consider increasing the number of shards for the stream.
- **A worker could fail, or the instance of the application that instantiated the worker could fail.**
    - When the application starts up, it instantiates a new worker, which in turn instantiates new record processors that are automatically assigned shards to process. 
    - These could be the same shards that these record processors were processing before the failure, or shards that are new to these processors.
- **An EC2 instance that is hosting one or more instances of the application could fail.**
    - We recommend that you run the EC2 instances for your application in an Auto Scaling group. 
    - This way, if one of the EC2 instances fails, the Auto Scaling group automatically launches a new instance to replace it. 
    - You should configure the instances to launch your Amazon Kinesis Data Streams application at startup.
- Handling duplicate records.
    - Can occur due to producer retry (or) consumer retry.
    - Your application must anticipate and appropriately handle processing individual records multiple times.
    - **Applications that need strict guarantees should embed a primary key within the record to remove duplicates later when processing.** 
    - Note that the number of duplicates due to producer retries is usually low compared to the number of duplicates due to consumer retries.

> If the destination of the final data can handle duplicates well, **we recommend relying on the final destination to achieve idempotent processing**. For example, with Opensearch you can use a combination of versioning and unique IDs to prevent duplicated processing.