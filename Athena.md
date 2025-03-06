# Athena:
- Amazon Athena is a service that enables data analysts to perform interactive queries in the web based cloud storage service i.e. Amazon Simple Storage Service (S3).
- Athena used a distributed SQL engine called Presto, which is used to run the SQL queries.
- Presto is based on the populate open source technology Hive, to store structured, semi structured and unstructured data.

# Benefits of Amazon Athena:
- **Serverless :** There is no need to manage any underlying compute infrastructure to use the tool.i.e. no need of allocation of memory, no cluster creation
- Athena also enables cross-account access to S3 buckets owned by another user.
- Amazon athena can process unstructured, semistructured and structured data sets. This is useful for research and log analysis.
- Data in athena can be inserted through simple AWS Lambda. As AWS Lambda is serverless and Athena is also serverless, so model or anything can be created which will have very less cost.

# Limitations of Athena include:
- Optimization is limited to queries. e.g. data already stored in S3 cannot be optimized.
- No indexing options. Indexing options commonly appear in traditional databases.
- When querying a table with thousands of partitions, Athena can time out. Athena's partition limit is 20,000 per table.

# Partitioning Athena tables:
- By partitioning your Athena tables, you can restrict the amount of data scanned by each query.
- thus improving the performance and reducing the costs. Partitioning divides your table into parts and keeps related data together based on column values.
- partitions act as virtual columns and help reduce the amount of data scanned per query.

Partitioning can be done in two types:
1) Along with the giving partition key in table in query, we have to create folder wise partition in bucket also, so that it will match the partition given. Partition will not be created by self they will be created in bucket folder wise also 

**Partitioning naming convention - #1**<br>
Partition column name followed by  '=' symbol.
Example: s3://bucket/data/year=2019/month=12/day=31

s3://yourbucket/pathToTable/<PARTITION_COLUMN_NAME>=<VALUE>/<PARTITION_COLUMN_NAME>=<VALUE>/

//Load the partitions<BR>
MSCK REPAIR TABLE table_name;

**Partitioning naming convention -#2**<br>
if the S3 path doesn't have '=' symbol <br>
*Example :*  s3://bucket/data/2019/12/31 <br>

s3://yourBucket/pathToTable/YYYY/MM/DD/ <br>

**//Load the partitions**<br>
Alter table <tablename> add Partition(PARTITION_COLUMN_NAME= <VALUE>, 
PARTITION_COLUMN2_NAME = <VALUE>) LOCATION 'S3://yourBucket/pathToTable/YYYY/MM/DD';

**Creating Athena tables**<br>
There are 3 main ways to create a new table for Athena:
1. using AWS Glue Crawler
2. defining the scehma manually
3. through SQL DDL queries
