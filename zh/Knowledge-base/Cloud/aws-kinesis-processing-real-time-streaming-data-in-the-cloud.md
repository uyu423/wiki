---
title: AWS Kinesis：在云端处理实时流数据
description: 
published: true
date: 2023-02-14T04:55:38.319Z
tags: 
editor: markdown
dateCreated: 2023-02-14T04:55:36.659Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [AWS Kinesis: Processing Real-Time Streaming Data in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-kinesis-processing-real-time-streaming-data-in-the-cloud)
{.links-list}

      

# AWS Kinesis：在云端处理实时流数据

对于任何组织而言，实时数据处理都是一项复杂且具有挑战性的任务。它需要从多个来源获取数据，将这些数据转换为有用的信息，并在正确的时间将该信息传递给正确的人。所有这些都必须快速准确地完成，同时还要确保数据不会在该过程中丢失或损坏。

AWS Kinesis 是一个基于云的平台，可以轻松地大规模处理实时流数据。 Kinesis 可以同时从多个来源获取数据，并使用多个 Amazon EC2 实例并行处理这些数据。这允许快速准确地处理大量数据。

Kinesis 是一项托管服务，这意味着 AWS 会为您负责基础设施和扩展。这让您可以轻松开始使用 Kinesis，并且无需配置和维护您自己的服务器。 Kinesis 也是无服务器的，因此您只需为使用的资源付费。

## 开始使用 AWS Kinesis

要开始使用 AWS Kinesis，您首先需要创建一个流。流是代表一组分片的逻辑实体。分片是一个数据存储单元，可用于存储和处理数据。

您可以使用 AWS 管理控制台、AWS 命令行界面 (CLI) 或 AWS SDK 创建流。

创建流后，您就可以开始向其中摄取数据。数据可以从多个来源获取，例如日志文件、应用程序事件、社交媒体流和传感器数据。

Kinesis Data Streams 可以以每个分片每秒高达 1MB 的速度摄取数据。如果您需要以更高的速率摄取数据，您可以增加流中的分片数量。

一旦数据被引入流中，就可以使用 Kinesis Data Analytics、Kinesis Data Firehose 或自定义应用程序对其进行处理。

Kinesis Data Analytics 是一项完全托管的服务，可以轻松实时分析流数据。 Kinesis Data Analytics 可用于对数据执行复杂的转换，例如聚合、过滤和联接。

Kinesis Data Firehose 是一项完全托管的服务，可以轻松地将流数据加载到 AWS 数据存储中，例如 Amazon S3、Amazon Redshift 和 Amazon Elasticsearch Service。

您还可以使用自定义应用程序处理流中的数据。自定义应用程序可以用任何编程语言编写，并且可以部署在 Amazon EC2、Amazon ECS 或 AWS Lambda 上。

## 处理流中的数据

Kinesis Data Streams 使用称为分片的概念来提供可扩展性和性能。分片是一个数据存储单元，可用于存储和处理数据。

Kinesis Data Streams 旨在水平扩展，这意味着您可以增加流中的分片数量以增加其吞吐量。

流中的数据由多个 Amazon EC2 实例并行处理。每个实例处理来自流中一个或多个分片的数据。

Kinesis Data Streams 使用分区键在流中的所有分片之间均匀分布数据。分区键是数据记录的一个属性，用于确定数据记录将分配给哪个分片。

当数据被提取到流中时，Kinesis Data Streams 使用分区键来确定将数据提取到哪个分片。 Kinesis Data Streams 还将使用分区键来确定要处理数据记录的实例。

流中的数据记录按接收顺序进行处理。但是，由于数据分布在多个分片中，因此无法保证数据记录的处理顺序。

如果需要按特定顺序处理数据记录，可以使用数据记录的序号属性。当数据记录被提取到流中时，序列号由 Kinesis Data Streams 分配。

具有相同分区键的数据记录将根据其序号按顺序处理。然而，具有不同分区键的数据记录可能被乱序处理。

## 结论

AWS Kinesis 是一个用于大规模处理实时流数据的强大平台。 Kinesis 可以同时从多个来源获取数据，并使用多个 Amazon EC2 实例并行处理这些数据。这允许快速准确地处理大量数据。

Kinesis 是一项托管服务，这意味着 AWS 会为您负责基础设施和扩展。这让您可以轻松开始使用 Kinesis，并且无需配置和维护您自己的服务器。 Kinesis 也是无服务器的，因此您只需为使用的资源付费。

## 延伸阅读

- [AWS Kinesis Data Streams 开发人员指南](https://docs.aws.amazon.com/kinesis/latest/datastreams/developer-guide.html)
- [AWS Kinesis Data Analytics 开发人员指南](https://docs.aws.amazon.com/kinesisanalytics/latest/java/getting-started.html)
- [AWS Kinesis Data Firehose 开发人员指南](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html)