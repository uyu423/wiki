---
title: 使用 AWS 和 Azure 数据库
description: 
published: true
date: 2023-02-17T04:18:31.059Z
tags: 
editor: markdown
dateCreated: 2023-02-17T04:17:31.042Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Working with AWS and Azure Databases***English** document is available*](/en/Knowledge-base/Cloud/working-with-aws-and-azure-databases)
{.links-list}


# 使用 AWS 和 Azure 数据库

本指南概述了如何使用 Amazon Web Services (AWS) 和 Microsoft Azure 在云中处理数据库。它涵盖了两个平台之间的主要区别，提供了设计基于云的数据库的技巧，并为 IT 开发提供了实用信息和实际解决方案。

## AWS 与 Azure 数据库

AWS 和 Azure 数据库之间有几个关键区别，在设计基于云的数据库解决方案时需要考虑这些重要区别。

### 成本

AWS 提供按需付费的定价模式，无需预付费用，而 Azure 按月收费。

### 贮存

AWS 为所有数据库类型提供无限存储，而 Azure 将 SQL 数据库的存储限制为 10 GB，将 NoSQL 数据库限制为 50 GB。

### 备份与恢复

AWS 为所有数据库类型提供自动备份和恢复，而 Azure 仅为 SQL 数据库提供此功能。

### 可扩展性

AWS 为所有数据库类型提供水平可扩展性，而 Azure 仅为 SQL 数据库提供垂直可扩展性。

## 设计基于云的数据库的技巧

在设计基于云的数据库时，需要考虑几个重要因素。

### 贮存

考虑数据库的存储要求以及是否需要无限存储。如果没有，Azure 可能是一个更具成本效益的选择。

### 备份与恢复

如果不需要自动备份和恢复，Azure 可能是一个更具成本效益的选择。

### 可扩展性

考虑数据库的可伸缩性要求。如果不需要水平可扩展性，Azure 可能是一个更具成本效益的选择。

## 实用信息和现实世界的解决方案

以下部分提供了在云中使用数据库的实用信息和实际解决方案。

### 在 AWS 中创建数据库

要在 AWS 中创建数据库，请使用 Amazon RDS 控制台。

1. 在 Amazon RDS 控制台上，选择 **创建数据库**。

2. 选择您要使用的数据库引擎。

3. 指定数据库配置细节。

4. 选择实例大小。

5. 选择存储类型。

6. 配置安全设置。

7. 查看数据库配置。

8. 选择**创建数据库**。

### 在 Azure 中创建数据库

要在 Azure 中创建数据库，请使用 Azure 门户。

1. 在 Azure 门户上，选择 **创建资源**。

2. 选择**数据库**。

3. 选择您要使用的数据库引擎。

4. 指定数据库配置细节。

5. 选择实例大小。

6. 选择存储类型。

7. 配置安全设置。

8. 查看数据库配置。

9. 选择**创建**。

### 连接到 AWS 中的数据库

要连接到 AWS 中的数据库，请使用 Amazon RDS 控制台。

1. 在 Amazon RDS 控制台上，选择您要连接的数据库。

2. 选择**连接**选项卡。

3. 选择**创建新连接**。

4. 指定连接细节。

5. 选择**创建连接**。

6. 复制连接字符串。

7. 将连接字符串粘贴到您的应用程序代码中。

### 连接到 Azure 中的数据库

要连接到 Azure 中的数据库，请使用 Azure 门户。

1. 在 Azure 门户上，选择要连接的数据库。

2. 选择**概览**选项卡。

3. 选择**显示连接字符串**。

4. 复制连接字符串。

5. 将连接字符串粘贴到您的应用程序代码中。

## 外部资源

有关使用 AWS 和 Azure 数据库的更多信息，请参阅以下资源：

- [AWS 数据库服务](https://aws.amazon.com/databases/)
- [Azure 数据库服务](https://azure.microsoft.com/en-us/services/database/)
- [设计基于云的关系数据库](https://aws.amazon.com/articles/17286/designing-cloud-based-relational-databases/)
- [设计基于云的 NoSQL 数据库](https://aws.amazon.com/articles/16989/designing-cloud-based-nosql-databases/)