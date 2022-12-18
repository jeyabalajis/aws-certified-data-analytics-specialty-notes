# Kinesis Data Firehose

## Resilience

- Highly resilient & Serverless.

## Record Format Conversion

- **A deserializer to read the JSON of your input data**. You can choose one of two types of deserializers: Apache Hive JSON SerDe or OpenX JSON SerDe.
- **A schema to determine how to interpret that data** – Use AWS Glue to create a schema in the AWS Glue Data Catalog. - Kinesis Data Firehose then references that schema and uses it to interpret your input data.
- **A serializer to convert the data to the target columnar storage format (Parquet or ORC)** – You can choose one of two types of serializers: ORC SerDe or Parquet SerDe.