# Redshift

## Best Practices

### COPY Data from multiple, evenly sized files

- When loading multiple files into a single table, use a single COPY command for the table, rather than multiple COPY commands.
- Amazon Redshift automatically parallelizes the data ingestion. 
- Using a single COPY command to bulk load data into a table ensures optimal use of cluster resources, and quickest possible throughput.

### Use WLM (Workload Management)

Use Amazon Redshift’s workload management (WLM) to define multiple queues dedicated to different workloads (for example, ETL versus reporting) and to manage the runtimes of queries. As you migrate more workloads into Amazon Redshift, your ETL runtimes can become inconsistent if WLM is not appropriately set up.

### Perform Table Maintenance regularly

Amazon Redshift is a columnar database, which enables fast transformations for aggregating data. Performing regular table maintenance ensures that transformation ETLs are predictable and performant. To get the best performance from your Amazon Redshift database, you must ensure that database tables regularly are VACUUMed and ANALYZEd.

### Perform multiple steps in a single transaction

ETL transformation logic often spans multiple steps. Because commits in Amazon Redshift are expensive, if each ETL step performs a commit, multiple concurrent ETL processes can take a long time to execute.

### Loading Data in Bulk

Amazon Redshift is designed to store and query petabyte-scale datasets. Using Amazon S3 you can stage and accumulate data from multiple source systems before executing a bulk COPY operation. 

The following methods allow efficient and fast transfer of these bulk datasets into Amazon Redshift:

- Use a manifest file to ingest large datasets that span multiple files. The manifest file is a JSON file that lists all the files to be loaded into Amazon Redshift. Using a manifest file ensures that Amazon Redshift has a consistent view of the data to be loaded from S3, while also ensuring that duplicate files do not result in the same data being loaded more than one time.
- Use temporary staging tables to hold the data for transformation. These tables are automatically dropped after the ETL session is complete. Temporary tables can be created using the CREATE TEMPORARY TABLE syntax, or by issuing a SELECT … INTO #TEMP_TABLE query. Explicitly specifying the CREATE TEMPORARY TABLE statement allows you to control the DISTRIBUTION KEY, SORT KEY, and compression settings to further improve performance.
- **Use ALTER table APPEND to swap data from the staging tables to the target table**. Data in the source table is moved to matching columns in the target table. Column order doesn’t matter. After data is successfully appended to the target table, the source table is empty. ALTER TABLE APPEND is much faster than a similar CREATE TABLE AS or INSERT INTO operation because it doesn’t involve copying or moving data.

### Use Redshift Spectrum for ad hoc ETL processing

### Monitor daily ETL health using diagnostic queries