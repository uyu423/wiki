---
title: AWS Glue：在云端自动化数据处理和 ETL
description: 
published: true
date: 2023-01-31T22:36:35.014Z
tags: 
editor: markdown
dateCreated: 2023-01-31T22:36:33.406Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [AWS Glue: Automating Data Processing and ETL in the Cloud***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-glue-automating-data-processing-and-etl-in-the-cloud)
{.links-list}


# AWS Glue：在云中自动化数据处理和 ETL

## 介绍

ETL 代表提取、转换和加载。它是从多个来源提取数据，将其转换成可以加载到数据仓库中的格式，然后再加载到数据仓库中的过程。 ETL 是数据处理和分析的关键部分，它可能是一个耗时且复杂的过程。

AWS Glue 是一项完全托管的 ETL 服务，可让您轻松准备和加载数据以进行分析。它可以处理 ETL 的所有方面，从数据发现到数据转换和数据加载。 Glue 可以自动生成代码来提取、转换和加载您的数据。它还可以自动发现和注册您的数据源，并将您的数据映射到适当的数据类型。

## 使用 AWS Glue 提取数据

AWS Glue 可以从各种数据源中发现和提取数据。它可以使用 JDBC 驱动程序连接到数据源，也可以连接到 Amazon S3 数据源。

要从 JDBC 数据源中提取数据，首先需要创建一个 Glue 连接。连接定义连接到数据源所需的参数。创建连接后，您可以使用它来运行爬虫。爬虫是一种 Glue 作业，它会扫描您的数据源并为数据创建架构。该架构存储在 AWS Glue 数据目录中。

运行爬虫后，您可以创建 Glue 作业以从数据源中提取数据。该作业将从数据源读取数据并将其写入 Amazon S3 数据目标。您可以选择将数据写入新的 Amazon S3 存储桶，也可以覆盖现有的 Amazon S3 存储桶。

## 使用 AWS Glue 转换数据

提取数据后，您可以使用 AWS Glue 对其进行转换。 Glue 提供了一个强大的 ETL 引擎，可以处理各种数据转换任务。

要转换数据，您首先需要创建 Glue 作业。 Glue 作业定义将要运行的 ETL 过程。您可以使用 AWS Glue 控制台创建和编辑 Glue 作业。

创建 Glue 作业后，您可以将 Glue 转换添加到作业中。粘合转换用于修改从数据源读取的数据。例如，您可以使用 Glue 转换来过滤数据，或更改列的数据类型。

添加 Glue 转换后，您可以运行 Glue 作业。该作业将从数据源读取数据，应用 Glue 转换，并将转换后的数据写入 Amazon S3 数据目标。

## 使用 AWS Glue 加载数据

转换数据后，您可以将其加载到数据仓库中。 AWS Glue 可以将数据加载到 Amazon Redshift、Amazon DynamoDB 和 Amazon Aurora。

要将数据加载到数据仓库中，您首先需要创建一个 Glue 作业。 Glue 作业定义将要运行的 ETL 过程。您可以使用 AWS Glue 控制台创建和编辑 Glue 作业。

创建 Glue 作业后，您可以向该作业添加 Glue 数据加载转换。 Glue 数据加载转换用于将数据加载到数据仓库中。您可以选择将数据加载到新表中，也可以将数据附加到现有表中。

添加 Glue 数据加载转换后，您可以运行 Glue 作业。该作业将从数据源读取数据，应用 Glue 转换，并将数据加载到数据仓库中。

## 结论

AWS Glue 是一项完全托管的 ETL 服务，可让您轻松准备和加载数据以进行分析。它可以处理 ETL 的所有方面，从数据发现到数据转换和数据加载。 Glue 可以自动生成代码来提取、转换和加载您的数据。它还可以自动发现和注册您的数据源，并将您的数据映射到适当的数据类型。