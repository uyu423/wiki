---
title: AWS Athena：使用无服务器计算对 S3 数据运行 SQL 查询
description: 
published: true
date: 2023-01-31T08:57:38.601Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:57:36.971Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [AWS Athena: Running SQL Queries on S3 Data with Serverless Computing***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-athena-running-sql-queries-on-s3-data-with-serverless-computing)
{.links-list}
 

# AWS Athena：使用无服务器计算对 S3 数据运行 SQL 查询

## 介绍

云计算的最大优势之一是能够根据需要扩展或缩减服务。这对于在一年中的特定时间遇到使用高峰的企业尤为重要。无服务器计算是一种云计算执行模型，其中云提供商运行服务器，客户按使用付费。

AWS Athena 是一种无服务器交互式查询服务，可以使用标准 SQL 轻松分析 Amazon S3 中的数据。雅典娜易于使用。无需设置或管理任何基础设施。数据存储在 S3 中，因此具有高可用性和持久性。 Athena 自动扩展——并行执行查询——因此结果很快，即使是大型数据集和复杂查询。

在本文中，我们将了解如何使用 AWS Athena 设置和查询存储在 S3 中的数据。我们还将了解使用 Athena 的一些优点和缺点。

# # 设置 AWS Athena

在开始使用 Athena 之前，您需要在 AWS 中进行一些设置。

首先，您需要创建一个 S3 存储桶来存储您的数据。您可以通过 AWS 管理控制台执行此操作，也可以使用以下 AWS CLI 命令：

```
aws s3 mb s3://{bucket-name}
```

将 {bucket-name} 替换为您的存储桶名称。

接下来，您需要在 Athena 中创建数据库和表。 Athena 使用 Apache Hive 元存储来存储有关数据库和表的信息。

您可以使用 AWS 管理控制台创建数据库和表，也可以使用以下 Athena 查询编辑器命令：

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

替换以下内容：

- {database-name}：你的数据库的名字
- {table-name}：你的表名
- {column-name}：您的列的名称
- {data-type}：列的数据类型
- {file-format}：数据的文件格式（例如“TEXTFILE”、“PARQUET”等）

创建数据库和表后，需要将数据加载到表中。您可以使用 AWS 管理控制台执行此操作，也可以使用以下 AWS CLI 命令：

```
aws s3 cp {s3-path} {local-path} --recursive
```

替换以下内容：

- {s3-path}：S3 中数据的路径（例如 s3://mybucket/data/）
- {local-path}：要复制数据的本地目录的路径

# # 使用 Athena 查询数据

现在您已经设置了数据，您可以开始使用 Athena 查询它。您可以使用 AWS 管理控制台执行此操作，也可以使用 Athena 查询编辑器。

要使用 Athena 查询编辑器，请打开编辑器并选择要查询的数据库和表。然后在查询编辑器中输入您的 SQL 查询并单击运行查询。

Athena 将执行您的查询并返回结果。

您还可以保存您的查询供以后使用。为此，请选择要保存的查询并单击“保存”按钮。输入查询名称和描述，然后单击保存。

# # 使用 Athena 的好处

使用 Athena 有很多好处，包括：

- 雅典娜易于使用。无需设置或管理任何基础设施。
- 数据存储在S3中，因此具有高可用性和持久性。
- Athena 自动扩展——并行执行查询——因此结果很快，即使是大型数据集和复杂查询。
- Athena 是无服务器的，因此您只需为运行的查询付费。无需担心容量规划或管理服务器。

# # 使用 Athena 的缺点

使用 Athena 也有一些缺点，包括：

- Athena 不适用于需要实时数据分析的用例。 S3 中的数据通常每隔几分钟或几小时更新一次，因此 Athena 查询不会在数据更新后立即返回结果。
- Athena 不适合需要极低延迟数据分析的用例。 S3 中的数据通常每隔几分钟或几小时更新一次，因此 Athena 查询不会在数据更新后立即返回结果。
- Athena 不适合需要高吞吐量数据分析的用例。 S3 中的数据通常每隔几分钟或几小时更新一次，因此 Athena 查询不会在数据更新后立即返回结果。

## 结论

在本文中，我们了解了如何使用 AWS Athena 设置和查询存储在 S3 中的数据。我们还研究了使用 Athena 的一些优点和缺点。