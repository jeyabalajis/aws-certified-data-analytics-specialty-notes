# Glue ETL

## Scheduling

- Minimum Precision for Time Based Scheduling is 5 minutes.

## Glue for Streaming Data

- While Glue can process micro-batches, it does not handle streaming data. 
- If your use case requires you to ETL data while you stream it in, 
    - you can perform the first leg of your ETL using Amazon Kinesis, Amazon Kinesis Data Firehose, or Amazon Kinesis Data Analytics. 
    - Then store the data in either Amazon S3 or Amazon Redshift and 
    - trigger an AWS Glue ETL job to pick up that dataset and continue applying additional transformations to that data.

## Scalability

- AWS Glue uses a scale-out Apache Spark environment to load your data into its destination. 
- To scale out, you specify the number of DPUs (data processing units) that you want to allocate to your ETL jobs.