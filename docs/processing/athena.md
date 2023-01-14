# Athena

Amazon Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL. Athena is serverless, so there is no infrastructure to manage, and you pay only for the queries that you run.

## Best Practices

- Partition your data
- Bucket your data
- Use compression
- Optimize file size
- Optimize columnar data store generation

## Cost Control

Amazon Athena allows you to set two types of cost controls:
- per-query limit
- per-workgroup limit (a.k.a workgroup-wide data usage control limit)

- The per-query control limit specifies the total amount of data scanned per query. If any query that runs in the workgroup exceeds the limit, it is canceled.
- Use workgroups to separate users, teams, applications, or workloads, to set limits on the amount of data that each query or the entire workgroup can process, and to track costs. 
- Because workgroups act as resources, you can use resource-level identity-based policies to control access to a specific workgroup. 
- You can also view query-related metrics in Amazon CloudWatch, control costs by configuring limits on the amount of data scanned, and create thresholds and trigger actions, such as Amazon SNS, when these thresholds are breached.

## References

- [Create Tables in Athena from Nested JSON and mappings using JSON Serde](https://aws.amazon.com/blogs/big-data/create-tables-in-amazon-athena-from-nested-json-and-mappings-using-jsonserde/)

## Athena vs. ElasticSearch

- Amazon Elasticsearch Service can be relatively more expensive as you have to run an EC2 instance that charges you per-hour. 
- Amazon Athena is more suitable for ad-hoc analysis.