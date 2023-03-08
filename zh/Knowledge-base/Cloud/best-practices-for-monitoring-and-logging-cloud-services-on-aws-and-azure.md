---
title: 在 AWS 和 Azure 上监控和记录云服务的最佳实践”
description: 
published: true
date: 2023-02-11T15:17:20.110Z
tags: 
editor: markdown
dateCreated: 2023-02-11T15:17:18.825Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Best Practices for Monitoring and Logging Cloud Services on AWS and Azure"***English** document is available*](/en/Knowledge-base/Cloud/best-practices-for-monitoring-and-logging-cloud-services-on-aws-and-azure)
{.links-list}



# 在 AWS 和 Azure 上监控和记录云服务的最佳实践

许多组织正在使用云服务来运行他们的业务应用程序和系统。虽然云提供了许多好处，但它也为监控和日志记录带来了新的挑战。在本文中，我们将分享一些在 AWS 和 Azure 上监控和记录云服务的最佳实践。

## 收集日志

监视和日志记录最重要的方面之一是收集日志。日志可以提供对系统操作的宝贵见解，并可用于解决问题。

有几种不同的方法可以从云服务中收集日志。一种选择是使用像 CloudWatch Logs Insights 这样的工具。此工具允许您实时查询日志数据以查找特定信息。另一种选择是使用像 CloudTrail 这样的工具。 CloudTrail 提供您 AWS 账户中所有 API 活动的记录，这对于审计和故障排除很有用。

## 监控云服务

收集日志后，您需要监控它们是否存在任何问题。您可以寻找的一些不同的东西包括：

- 日志量的意外变化
- 日志内容的意外变化
- 错误或警告

如果您看到任何这些问题，您可以进一步调查以找出原因。

## 记录云服务

除了监视日志之外，您还需要记录它们。日志记录允许您存储日志以供将来参考。有几种不同的方法来记录云服务。一种选择是使用像 CloudWatch Logs 这样的工具。 CloudWatch Logs 允许您将日志存储在 AWS 中并在 CloudWatch 控制台中查看它们。另一种选择是使用 Azure Monitor 等工具。 Azure Monitor 允许您将日志存储在 Azure 中并在 Azure 门户中查看它们。

## 结论

监控和记录云服务是成功开展业务的重要组成部分。通过遵循本文中讨论的最佳实践，您可以更有效地收集、监视和记录您的云服务。