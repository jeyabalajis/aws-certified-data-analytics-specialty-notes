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
- A data processing unit (DPU) is a relative measure of processing power that consists of vCPUs and memory. 
- To improve the job execution time, you can enable job metrics in AWS Glue to estimate the number of data processing units (DPUs) that can be used to scale out an AWS Glue job.

## Glue Catalog

- If AWS Glue doesn’t find a custom classifier that fits the input data format with 100 percent certainty, then AWS Glue invokes the built-in classifiers. 
- The built-in classifier returns either certainty=1.0 if the format matches, or certainty=0.0 if the format doesn't match. 
- If no classifier returns certainty=1.0, then AWS Glue uses the output of the classifier that has the highest certainty.

> If no classifier returns a certainty of higher than 0.0, then AWS Glue returns the default classification string of UNKNOWN. 

> Grok is a tool that is used to parse textual data given a matching pattern. A grok pattern is a named set of regular expressions (regex) that are used to match data one line at a time. AWS Glue uses grok patterns to infer the schema of your data. When a grok pattern matches your data, AWS Glue uses the pattern to determine the structure of your data and map it into fields.

## Handling New Partitions in S3 Bucket (Data Lake)

- When the job finishes, view the new partitions on the console right away, without having to rerun the crawler. 
- You can enable this feature by adding a few lines of code to your ETL script. 
- The code uses the `enableUpdateCatalog` argument to indicate that the Data Catalog is to be updated during the job run as the new partitions are created.

### Sample Code (Python):

```
additionalOptions = {"enableUpdateCatalog": True}
additionalOptions["partitionKeys"] = ["region", "year", "month", "day"]
```