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

## Kinesis Data Streams API

- If your application cannot use the KPL because it cannot incur any additional processing delay, consider using the Kinesis Data Streams API directly.