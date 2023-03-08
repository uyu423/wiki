---
title: AWS CloudWatch：监控和调试云应用程序
description: 
published: true
date: 2023-02-09T16:55:41.912Z
tags: 
editor: markdown
dateCreated: 2023-02-09T16:55:35.631Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [AWS CloudWatch: Monitoring and Debugging Cloud Applications***English** document is available*](/en/Knowledge-base/Cloud/aws-cloudwatch-monitoring-and-debugging-cloud-applications)
{.links-list}


# AWS CloudWatch：监控和调试云应用程序

## 介绍

CloudWatch 是针对 AWS 云资源和运行在 AWS 上的应用程序的监控服务。 CloudWatch 提供数据和可操作的见解，以监控应用程序、了解和响应系统范围的性能变化、优化资源利用率并获得运营健康状况的统一视图。 CloudWatch 可用于收集和跟踪指标、设置警报以及自动对 AWS 资源的变化做出反应。

在本文中，我们将了解 CloudWatch 的工作原理以及如何使用它来监控和调试云应用程序。

## CloudWatch 的工作原理

CloudWatch 从 AWS 资源（例如 Amazon EC2 实例、Amazon DynamoDB 表和 Amazon RDS 数据库实例）收集数据。然后使用此数据生成可用于监控资源和应用程序性能的指标。

CloudWatch 还可用于从您的资源和应用程序收集日志数据。此数据可用于解决问题和识别趋势。

## 使用 CloudWatch 进行监控

CloudWatch 可用于通过两种方式监控您的资源和应用程序：

- **指标**：CloudWatch 指标是统计数据点，可用于监控资源和应用程序的性能。指标是根据 CloudWatch 收集的数据生成的。

- **日志**：CloudWatch 日志是您的资源和应用程序活动的记录。日志可用于解决问题和识别趋势。

## 设置 CloudWatch

要使用 CloudWatch，您必须先创建一个 Amazon CloudWatch Logs 组和一个 Amazon CloudWatch Logs 流。

接下来，您需要在 EC2 实例上安装 CloudWatch Logs 代理。 CloudWatch Logs 代理是一个在您的 EC2 实例上运行并将日志数据发送到 CloudWatch 的软件程序。

在您的 EC2 实例上安装并运行 CloudWatch Logs 代理后，您就可以开始将日志数据发送到 CloudWatch。

## 使用 CloudWatch 收集指标

CloudWatch 指标数据每五分钟收集一次，并存储两周。

要使用 CloudWatch 收集指标，您首先需要创建一个指标过滤器。指标筛选器匹配日志数据中的模式并从日志条目中提取指标数据。

接下来，您需要创建一个指标警报。指标警报监视指标并在指标超过阈值时触发操作。

## 使用 CloudWatch 收集日志

CloudWatch 日志数据每隔一分钟收集一次，并存储 14 天。

要使用 CloudWatch 收集日志，您首先需要创建一个日志组。日志组是具有相同保留期的日志的集合。

接下来，您需要创建一个日志流。日志流是来自单一来源的一系列日志事件。

创建日志组和日志流后，您可以开始将日志数据发送到 CloudWatch。

## 使用 CloudWatch 发送通知

CloudWatch 可用于在触发指标警报时发送通知。通知可以通过 Amazon SNS、Amazon SQS 或电子邮件发送。

要使用 CloudWatch 发送通知，您首先需要创建一个 Amazon SNS 主题。 Amazon SNS 主题是允许收件人订阅您的 Amazon SNS 消息的逻辑访问点。

接下来，您需要创建一个 Amazon SQS 队列。 Amazon SQS 队列是一个缓冲区，用于存储消息，直到它们被消费者处理为止。

创建 Amazon SNS 主题和 Amazon SQS 队列后，您可以配置指标警报以向它们发送通知。

## 结论

在本文中，我们了解了 CloudWatch 的工作原理以及如何使用它来监控和调试云应用程序。我们还了解了如何设置 CloudWatch 以及如何使用 CloudWatch 收集指标和日志。最后，我们了解了如何使用 CloudWatch 发送通知。