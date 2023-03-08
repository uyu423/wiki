---
title: AWS Kinesis: Processing Real-Time Streaming Data in the Cloud
description: 
published: true
date: 2023-02-14T04:55:43.715Z
tags: 
editor: markdown
dateCreated: 2023-02-14T04:55:36.664Z
---

- [AWS Kinesis: procesamiento de datos de transmisión en tiempo real en la nube***Spanish** document is available*](/es/Knowledge-base/Cloud/aws-kinesis-processing-real-time-streaming-data-in-the-cloud)
{.links-list}
- [AWS Kinesis：在云端处理实时流数据***Chinese Simplified** document is available*](/zh/Knowledge-base/Cloud/aws-kinesis-processing-real-time-streaming-data-in-the-cloud)
{.links-list}
- [AWS Kinesis: 클라우드에서 실시간 스트리밍 데이터 처리***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-kinesis-processing-real-time-streaming-data-in-the-cloud)
{.links-list}

      

# AWS Kinesis: Processing Real-Time Streaming Data in the Cloud

Real-time data processing is a complex and challenging task for any organization. It requires the ingestion of data from multiple sources, the transformation of that data into useful information, and the delivery of that information to the correct people at the correct time. All of this must be done quickly and accurately, while also ensuring that data is not lost or corrupted in the process.

AWS Kinesis is a cloud-based platform that makes it easy to process real-time streaming data at scale. Kinesis can ingest data from multiple sources simultaneously and process it using multiple Amazon EC2 instances in parallel. This allows for quick and accurate processing of large amounts of data.

Kinesis is a managed service, which means that AWS takes care of the infrastructure and scaling for you. This makes it easy to get started with Kinesis and eliminates the need to provision and maintain your own servers. Kinesis is also serverless, so you only pay for the resources you use.

## Getting Started with AWS Kinesis

To get started with AWS Kinesis, you first need to create a stream. A stream is a logical entity that represents a group of shards. A shard is a unit of data storage that can be used to store and process data.

You can create a stream using the AWS Management Console, the AWS Command Line Interface (CLI), or the AWS SDK.

Once you have created a stream, you can start ingesting data into it. Data can be ingested from multiple sources, such as log files, application events, social media streams, and sensor data.

Kinesis Data Streams can ingest data at a rate of up to 1MB per second per shard. If you need to ingest data at a higher rate, you can increase the number of shards in your stream.

Once data has been ingested into a stream, it can be processed using Kinesis Data Analytics, Kinesis Data Firehose, or a custom application.

Kinesis Data Analytics is a fully managed service that makes it easy to analyze streaming data in real time. Kinesis Data Analytics can be used to perform complex transformations on data, such as aggregations, filtering, and joins.

Kinesis Data Firehose is a fully managed service that makes it easy to load streaming data into AWS data stores, such as Amazon S3, Amazon Redshift, and Amazon Elasticsearch Service.

You can also process data in a stream using a custom application. A custom application can be written in any programming language and can be deployed on Amazon EC2, Amazon ECS, or AWS Lambda.

## Processing Data in a Stream

Kinesis Data Streams uses a concept called shards to provide scalability and performance. A shard is a unit of data storage that can be used to store and process data.

Kinesis Data Streams is designed to scale horizontally, which means that you can increase the number of shards in a stream to increase its throughput.

Data in a stream is processed in parallel by multiple Amazon EC2 instances. Each instance processes data from one or more shards in the stream.

Kinesis Data Streams uses a partition key to distribute data evenly across all shards in a stream. The partition key is an attribute of the data record that is used to determine which shard the data record will be assigned to.

When data is ingested into a stream, Kinesis Data Streams uses the partition key to determine which shard to ingest the data into. Kinesis Data Streams will also use the partition key to determine which instance to process the data record.

Data records in a stream are processed in the order that they are received. However, because data is distributed across multiple shards, the order in which data records are processed is not guaranteed.

If you need to process data records in a specific order, you can use the sequence number attribute of a data record. The sequence number is assigned by Kinesis Data Streams when a data record is ingested into a stream.

Data records with the same partition key will be processed in order based on their sequence number. However, data records with different partition keys may be processed out of order.

## Conclusion

AWS Kinesis is a powerful platform for processing real-time streaming data at scale. Kinesis can ingest data from multiple sources simultaneously and process it using multiple Amazon EC2 instances in parallel. This allows for quick and accurate processing of large amounts of data.

Kinesis is a managed service, which means that AWS takes care of the infrastructure and scaling for you. This makes it easy to get started with Kinesis and eliminates the need to provision and maintain your own servers. Kinesis is also serverless, so you only pay for the resources you use.

## Further Reading

- [AWS Kinesis Data Streams Developer Guide](https://docs.aws.amazon.com/kinesis/latest/datastreams/developer-guide.html)
- [AWS Kinesis Data Analytics Developer Guide](https://docs.aws.amazon.com/kinesisanalytics/latest/java/getting-started.html)
- [AWS Kinesis Data Firehose Developer Guide](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html)