# Open Search

- Amazon OpenSearch Service makes it easy for you to perform interactive log analytics, real-time application monitoring, a website search, and more. 
- OpenSearch is an open-source, distributed search and analytics suite derived from Elasticsearch. 
- Amazon OpenSearch Service is the successor to Amazon Elasticsearch Service and offers the latest versions of OpenSearch.

## Open Search Dashboard

- The OpenSearch dashboard (an open-source visualization tool) is tightly integrated with Amazon OpenSearch. 
- With the simple, browser-based interface OpenSearch Dashboards, you can create and share dynamic dashboards quickly. 
- Using the OpenSearch dashboard is free, and you only have to pay for the infrastructure where you installed the software.

## Performance

### Shards vs. Shard Size

- A good rule of thumb is to try to keep a shard size between 10–50 GiB.
- Large shards can make it difficult for ElasticSearch (ES) to recover from failure.
- Having too many small shards can cause performance issues and out of memory errors. 

> Shards should be small enough that the underlying Amazon ES instance can handle them, but not so small that they place needless strain on the hardware.

## Use Cases

### Document search 

- Extracting structured data from documents and creating a smart index using Amazon Elasticsearch Service (Amazon ES) allows you to search through millions of documents quickly. 
- For example, a mortgage company could use Amazon Textract to process millions of scanned loan applications in a matter of hours and have the extracted data indexed in Amazon ES. 
- This would allow them to create search experiences like searching for loan applications where the applicant's name is Jose Rizal, or searching for contracts where the interest rate is 2 percent.

> Redshift and Athena does not provide visual insights, unlike Kibana.
> Amazon Elasticsearch does not have a direct integration with Amazon QuickSight.

