---
title: AWS 和 Azure 上云服务的成本优化
description: 
published: true
date: 2023-02-01T12:17:49.613Z
tags: 
editor: markdown
dateCreated: 2023-02-01T12:17:48.173Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Cost Optimization for Cloud Services on AWS and Azure***English** version of this document is available*](/en/Knowledge-base/Cloud/cost-optimization-for-cloud-services-on-aws-and-azure)
{.links-list}



# AWS 和 Azure 上云服务的成本优化

在托管应用程序和服务时，云已成为许多组织的默认选择。但是，由于云提供商的选择众多，因此很难决定哪一个最适合您的需求。在本文中，我们将比较 AWS 和 Azure 的成本优化策略。

## AWS 成本优化

有一些关键策略可用于优化 AWS 上的成本：

### 1. 使用 Amazon EC2 预留实例

与按需实例定价相比，Amazon EC2 预留实例 (RI) 提供显着折扣（高达 75%）。 RI 还提供容量预留，如果您需要保证一定数量的计算容量始终可用，这会很有用。

要开始使用预留实例，您首先需要选择要预留的实例类型、区域和租期。然后您需要指定持续时间（1 年或 3 年）和付款选项（预付或每月）。

购买预留实例后，您可以在该区域启动实例并使用 RI 定价。

### 2. 使用 Amazon EC2 Spot 实例

Amazon EC2 Spot 实例允许您对未使用的 EC2 容量进行投标。与按需价格相比，Spot 实例通常可提供高达 90% 的折扣。

要使用 Spot 实例，您首先需要选择要使用的实例类型、区域和可用区。然后，您需要指定每小时愿意支付的最高价格。

如果您的出价高于当前的竞价，您的实例将启动并继续运行，直到竞价超过您的竞价。届时，您的实例将终止，您将按实例运行的小时数付费。

### 3.使用自动缩放

Auto Scaling 是一项 AWS 服务，可让您自动扩展或缩减 Amazon EC2 容量以响应需求变化。

Auto Scaling 可以帮助您确保拥有正确数量的计算容量来满足您的需求，同时还能最大限度地降低成本。

要使用 Auto Scaling，您首先需要创建一个 Auto Scaling 组。该组可以包含一个或多个 Amazon EC2 实例。然后，您可以将组配置为扩大或缩小以响应需求变化。

### 4. 使用亚马逊 CloudWatch

Amazon CloudWatch 是一项 AWS 服务，可让您监控 Amazon EC2 实例和其他 AWS 资源。

CloudWatch 可用于设置警报，这些警报将自动扩大或缩小您的 Amazon EC2 容量以响应需求变化。

要使用 Amazon CloudWatch，您首先需要创建一个 CloudWatch 警报。此警报可由各种事件触发，例如 CPU 利用率或网络流量的变化。

然后，您可以配置警报以根据警报增加或减少 Amazon EC2 容量。

### 5. 使用亚马逊 S3

Amazon S3 是一项 AWS 服务，可让您将数据存储在云中。

S3 可用于存储不常访问的数据，或存储不立即需要的数据。这有助于降低在 Amazon EC2 实例上存储数据的成本。

要使用 Amazon S3，您首先需要创建一个 Amazon S3 存储桶。这个桶可以用来存储任何类型的数据。

然后，您可以配置 Amazon S3 存储桶以存储不常访问的数据，或存储不需要立即使用的数据。

### 6. 使用亚马逊 EBS

Amazon EBS 是一项 AWS 服务，可让您在 Amazon EC2 实例上存储数据。

EBS可用于存储经常访问的数据，或存储立即需要的数据。这有助于降低在 Amazon EC2 实例上存储数据的成本。

要使用 Amazon EBS，您首先需要创建一个 Amazon EBS 卷。此卷可用于存储任何类型的数据。

然后，您可以配置 Amazon EBS 卷以存储经常访问的数据，或存储立即需要的数据。

### 7. 使用亚马逊冰川

Amazon Glacier 是一项 AWS 服务，可让您将数据存储在云中。

Glacier 可用于存储不常访问的数据，或存储不立即需要的数据。这有助于降低在 Amazon EC2 实例上存储数据的成本。

要使用 Amazon Glacier，您首先需要创建一个 Amazon Glacier 保管库。该保管库可用于存储任何类型的数据。

然后，您可以配置 Amazon Glacier 保管库以存储不常访问的数据，或存储不需要立即使用的数据。

## Azure 成本优化

有一些关键策略可用于优化 Azure 上的成本：

### 1. 使用 Azure 预留实例

与按需实例定价相比，Azure 预留实例 (RI) 提供显着折扣（高达 80%）。 RI 还提供容量预留，如果您需要保证一定数量的计算容量始终可用，这会很有用。

要开始使用预留实例，您首先需要选择要预留的实例类型、区域和持续时间。然后您需要指定付款选项（预付或每月）。

购买预留实例后，您可以在该区域启动实例并使用 RI 定价。

### 2. 使用 Azure Spot 实例

Azure Spot 实例允许您对未使用的 Azure 容量进行投标。与按需价格相比，Spot 实例通常可提供高达 90% 的折扣。

要使用 Spot 实例，您首先需要选择要使用的实例类型、区域和可用区。然后，您需要指定每小时愿意支付的最高价格。

如果您的出价高于当前的竞价，您的实例将启动并继续运行，直到竞价超过您的竞价。届时，您的实例将终止，您将按实例运行的小时数付费。

### 3. 使用 Azure 自动缩放

Azure Auto Scaling 是一项 Azure 服务，可让你自动扩大或缩小 Azure 计算容量以响应需求变化。

Auto Scaling 可以帮助您确保拥有正确数量的计算容量来满足您的需求，同时还能最大限度地降低成本。

要使用 Auto Scaling，您首先需要创建一个 Auto Scaling 组。该组可以包含一个或多个 Azure VM。然后，您可以将组配置为扩大或缩小以响应需求变化。

### 4. 使用 Azure Monitor

Azure Monitor 是一项 Azure 服务，可让你监视 Azure VM 和其他 Azure 资源。

Monitor 可用于设置警报，这些警报将自动增加或减少 Azure 计算容量以响应需求变化。

要使用 Azure Monitor，首先需要创建一个 Monitor 规则。此规则可由各种事件触发，例如 CPU 使用率或网络流量的变化。

然后，您可以配置规则以增加或减少 Azure 计算容量以响应警报。

### 5. 使用 Azure 存储

Azure 存储是一项 Azure 服务，可让您将数据存储在云中。

存储可用于存储不常访问的数据，或存储不立即需要的数据。这有助于降低在 Azure VM 上存储数据的成本。

要使用 Azure 存储，您首先需要创建一个 Azure 存储帐户。该帐户可用于存储任何类型的数据。

然后，您可以配置 Azure 存储帐户以存储不常访问的数据，或存储不需要立即使用的数据。

### 6. 使用 Azure 托管磁盘

Azure 托管磁盘是一项 Azure 服务，可让你在 Azure VM 上存储数据。

托管磁盘可用于存储经常访问的数据，或存储立即需要的数据。这有助于降低在 Azure VM 上存储数据的成本。

要使用 Azure 托管磁盘，首先需要创建一个 Azure 托管磁盘。该磁盘可用于存储任何类型的数据。

然后可以配置 Azure 托管磁盘来存储经常访问的数据，或存储立即需要的数据。

### 7. 使用 Azure 存档存储

Azure 存档存储是一项 Azure 服务，可让你将数据存储在云中。

归档存储可用于存储不常访问的数据，或存储不需要立即使用的数据。这有助于降低在 Azure VM 上存储数据的成本。

要使用 Azure 存档存储，您首先需要创建一个 Azure 存档存储帐户。该帐户可用于存储任何类型的数据。

然后，您可以配置 Azure 存档存储帐户以存储不常访问的数据，或存储不需要立即使用的数据。