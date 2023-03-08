---
title: 优化 AWS 和 Azure 上的资源使用和成本
description: 
published: true
date: 2023-02-01T13:43:24.552Z
tags: 
editor: markdown
dateCreated: 2023-02-01T13:43:23.152Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Optimizing Resource Usage and Cost on AWS and Azure***English** version of this document is available*](/en/Knowledge-base/Cloud/optimizing-resource-usage-and-cost-on-aws-and-azure)
{.links-list}



# 优化 AWS 和 Azure 上的资源使用和成本

开发人员一直在寻找优化资源使用和成本的方法。在使用云服务时尤其如此，其中资源按小时或分钟计费。在本文中，我们将了解如何优化 AWS 和 Azure 上的资源使用和成本。

## AWS

有几种方法可以优化 AWS 上的资源使用和成本。首先，您可以使用保留实例。预留实例是长期合同，可为特定实例类型的每小时费率提供高达 75% 的折扣。例如，如果您在 us-east-1 中有一个 m4.large 实例的预留实例，您需要支付每小时 0.1 美元，而不是每小时 0.4 美元的按需费率。

在 AWS 上优化资源使用和成本的另一种方法是使用自动缩放。自动缩放允许您根据需要扩展或缩减资源。例如，您可以设置一个自动缩放组，根据传入请求的数量向上或向下缩放您的 Web 服务器实例。

最后，您可以使用 AWS Lambda 运行代码以响应事件。 Lambda 是一个无服务器计算平台，它根据请求的数量和代码执行所需的时间向您收费。 Lambda 是运行不需要一直运行的代码的好方法，例如处理图像或发送电子邮件的代码。

## 蔚蓝

有几种方法可以优化 Azure 上的资源使用和成本。首先，您可以使用保留实例。预留实例是长期合同，可为特定实例类型的每小时费率提供高达 80% 的折扣。例如，如果您在 eastus2 中有一个 D4s_v3 实例的预留实例，您需要支付每小时 0.08 美元，而不是每小时 0.4 美元的按需费率。

在 Azure 上优化资源使用和成本的另一种方法是使用自动缩放。自动缩放允许您根据需要扩展或缩减资源。例如，您可以设置一个自动缩放组，根据传入请求的数量向上或向下缩放您的 Web 服务器实例。

最后，您可以使用 Azure Functions 运行代码以响应事件。 Functions 是一个无服务器计算平台，它根据请求数量和代码执行时间向您收费。函数是运行不需要一直运行的代码的好方法，例如处理图像或发送电子邮件的代码。

## 结论

有几种方法可以优化 AWS 和 Azure 上的资源使用和成本。您可以使用预留实例、自动缩放和无服务器计算来节省云费用。