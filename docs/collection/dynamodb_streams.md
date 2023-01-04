# DynamoDB Streams

## Salient Features

- Each stream record appears exactly once in the stream (Exactly-Once-Guarantee).
- For each item that is modified in a DynamoDB table, the stream records appear in the same sequence as the actual modifications to the item (Ordered Sequence).
- To work with database tables and indexes, your application must access a DynamoDB endpoint. To read and process DynamoDB Streams records, your application must access a DynamoDB Streams endpoint in the same Region.

## Reading and Processing a Stream

- To read and process a stream, your application must connect to a DynamoDB Streams endpoint and issue API requests.
- A stream consists of stream records. 
- Each stream record represents a single data modification in the DynamoDB table to which the stream belongs. 
- Each stream record is assigned a sequence number, reflecting the order in which the record was published to the stream.
- Stream records are organized into groups, or shards. Each shard acts as a container for multiple stream records, and contains information required for accessing and iterating through these records. 
- The stream records within a shard are removed automatically after 24 hours.
- Shards are ephemeral: They are created and deleted automatically, as needed. 
- Any shard can also split into multiple new shards; this also occurs automatically. (It's also possible for a parent shard to have just one child shard.) 
- A shard might split in response to high levels of write activity on its parent table, so that applications can process records from multiple shards in parallel.
- If you disable a stream, any shards that are open will be closed. The data in the stream will continue to be readable for 24 hours.

## Kinesis Adapter

- Because shards have a lineage (parent and children), an application must always process a parent shard before it processes a child shard. 
- This helps ensure that the stream records are also processed in the correct order.
- If you use the DynamoDB Streams Kinesis Adapter, this is handled for you.
- The DynamoDB Streams Kinesis Adapter acts as a transparent layer between the KCL and the DynamoDB Streams endpoint, so that the code can fully use KCL rather than having to make low-level DynamoDB Streams calls.

## Data retention limit for DynamoDB Streams

- All data in DynamoDB Streams is subject to a 24-hour lifetime. 
- You can retrieve and analyze the last 24 hours of activity for any given table. 
- However, data that is older than 24 hours is susceptible to trimming (removal) at any moment.

## Kinesis Data Streams (KDS) for DynamoDB

- You can use Amazon Kinesis Data Streams to capture changes to Amazon DynamoDB.
- Kinesis Data Streams captures item-level modifications in any DynamoDB table and replicates them to a Kinesis data stream. 
- Your applications can access this stream and view item-level changes in near-real time. 
- You can continuously capture and store terabytes of data per hour. 
- You can take advantage of longer data retention time—and with enhanced fan-out capability, you can simultaneously reach two or more downstream applications. 
- Other benefits include additional audit and security transparency.
- Kinesis Data Streams also gives you access to Amazon Kinesis Data Firehose and Amazon Kinesis Data Analytics. 
- These services can help you build applications that power real-time dashboards, generate alerts, implement dynamic pricing and advertising, and implement sophisticated data analytics and machine learning algorithms.

> You can only stream data from DynamoDB to Kinesis Data Streams in the same AWS account and AWS Region as your table.
> You can only stream data from a DynamoDB table to one Kinesis data stream.

