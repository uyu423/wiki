---
title: AWS Athena: Running SQL Queries on S3 Data with Serverless Computing
description: 
published: true
date: 2023-01-31T08:57:40.590Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:57:36.970Z
---

- [AWS Athena: 서버리스 컴퓨팅으로 S3 데이터에서 SQL 쿼리 실행***Korean** version of this document is available*](/ko/Knowledge-base/Cloud/aws-athena-running-sql-queries-on-s3-data-with-serverless-computing)
{.links-list}
- [AWS Athena: サーバーレスコンピューティングを使用して S3 データで SQL クエリを実行する***Japanese** version of this document is available*](/ja/Knowledge-base/Cloud/aws-athena-running-sql-queries-on-s3-data-with-serverless-computing)
{.links-list}
- [AWS Athena：使用无服务器计算对 S3 数据运行 SQL 查询***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Cloud/aws-athena-running-sql-queries-on-s3-data-with-serverless-computing)
{.links-list}
 

# AWS Athena: Running SQL Queries on S3 Data with Serverless Computing

## Introduction

One of the biggest advantages of cloud computing is the ability to scale services up or down according to demand. This is especially important for businesses which experience spikes in usage at certain times of the year. Serverless computing is a cloud computing execution model in which the cloud provider runs the server, and the customer pays per use. 

AWS Athena is a serverless interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL. Athena is easy to use. There is no need to set up or manage any infrastructure. Data is stored in S3, so it is highly available and durable. Athena scales automatically—executing queries in parallel—so results are fast, even with large datasets and complex queries.

In this article, we will look at how to set up and query data stored in S3 using AWS Athena. We will also look at some of the benefits and drawbacks of using Athena.

## Setting up AWS Athena

Before you can start using Athena, you need to set up a few things in AWS. 

First, you need to create an S3 bucket to store your data. You can do this through the AWS Management Console, or you can use the following AWS CLI command:

```
aws s3 mb s3://{bucket-name}
```

Replace {bucket-name} with the name of your bucket. 

Next, you need to create a database and table in Athena. Athena uses the Apache Hive metastore to store information about your databases and tables. 

You can create a database and table using the AWS Management Console, or you can use the following Athena Query Editor commands:

```sql
CREATE DATABASE {database-name};

CREATE TABLE {table-name}
(
  {column-name} {data-type}
)
ROW FORMAT SERDE 'org.apache.hive.hcatalog.data.JsonSerDe'
WITH SERDEPROPERTIES (
  'serialization.format' = '1'
)
STORED AS {file-format};
```

Replace the following:

- {database-name}: the name of your database
- {table-name}: the name of your table
- {column-name}: the name of your column
- {data-type}: the data type of your column
- {file-format}: the file format of your data (e.g. 'TEXTFILE', 'PARQUET', etc.)

After you have created your database and table, you need to load your data into the table. You can do this using the AWS Management Console, or you can use the following AWS CLI command:

```
aws s3 cp {s3-path} {local-path} --recursive
```

Replace the following:

- {s3-path}: the path to your data in S3 (e.g. s3://mybucket/data/)
- {local-path}: the path to the local directory where you want to copy the data

## Querying Data with Athena

Now that you have your data set up, you can start querying it with Athena. You can do this using the AWS Management Console, or you can use the Athena Query Editor. 

To use the Athena Query Editor, open the editor and select the database and table you want to query. Then enter your SQL query in the query editor and click Run Query. 

Athena will execute your query and return the results. 

You can also save your queries for later use. To do this, select the query you want to save and click the Save button. Enter a query name and description, and click Save. 

## Benefits of Using Athena

There are many benefits to using Athena, including the following:

- Athena is easy to use. There is no need to set up or manage any infrastructure.
- Data is stored in S3, so it is highly available and durable.
- Athena scales automatically—executing queries in parallel—so results are fast, even with large datasets and complex queries.
- Athena is serverless, so you only pay for the queries you run. There is no need to worry about capacity planning or managing servers.

## Drawbacks of Using Athena

There are also some drawbacks to using Athena, including the following:

- Athena is not suitable for use cases which require real-time data analysis. Data in S3 is typically updated every few minutes or hours, so Athena queries will not return results immediately after data is updated.
- Athena is not suitable for use cases which require very low latency data analysis. Data in S3 is typically updated every few minutes or hours, so Athena queries will not return results immediately after data is updated.
- Athena is not suitable for use cases which require high throughput data analysis. Data in S3 is typically updated every few minutes or hours, so Athena queries will not return results immediately after data is updated.

## Conclusion

In this article, we have looked at how to set up and query data stored in S3 using AWS Athena. We have also looked at some of the benefits and drawbacks of using Athena.