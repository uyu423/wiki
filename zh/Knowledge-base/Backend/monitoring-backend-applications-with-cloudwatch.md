---
title: 使用 CloudWatch 监控后端应用程序
description: 
published: true
date: 2023-02-10T01:55:35.455Z
tags: 
editor: markdown
dateCreated: 2023-02-10T01:55:33.774Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Monitoring Backend Applications with CloudWatch***English** document is available*](/en/Knowledge-base/Backend/monitoring-backend-applications-with-cloudwatch)
{.links-list}


# Monitoring 后端应用程序与 CloudWatch

CloudWatch 是针对 AWS 云资源和运行在 AWS 上的应用程序的监控服务。 CloudWatch 以日志、指标和事件的形式收集监控和操作数据，可用于对您的应用程序进行故障排除和优化。

在本文中，我们将重点介绍如何使用 CloudWatch 监控后端应用程序。我们将涵盖以下主题：

- 什么是 CloudWatch？
- 设置 CloudWatch
- 创建 CloudWatch 警报
- 查看 CloudWatch 日志

## 什么是 CloudWatch？

如前所述，CloudWatch 是针对 AWS 云资源和运行在 AWS 上的应用程序的监控服务。借助 CloudWatch，您可以收集和跟踪指标、设置警报并自动对 AWS 资源的变化做出反应。

CloudWatch 为您提供数据和可操作的见解，以监控您的应用程序、响应系统范围的性能变化、优化资源利用率并获得运营健康状况的统一视图。

## 设置云观察

为了使用 CloudWatch，您首先需要设置一个 AWS 账户并创建一个 Amazon CloudWatch Logs 组。

1. 要设置 AWS 账户，请转到 [https://aws.amazon.com/](https://aws.amazon.com/) 并单击 **Create an AWS Account**。

2. 按照说明创建您的帐户。

3. 创建帐户后，转到 [https://console.aws.amazon.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/) 上的 Amazon CloudWatch 控制台。

4. 在左侧导航面板中，单击 **Logs**。

5. 单击**创建日志组**。

6. 为您的日志组输入一个名称并单击**创建日志组**。

## 创建 CloudWatch 警报

警报会在您指定的时间段内监视指标，并根据相对于您设置的阈值的指标值执行一项或多项操作。这些操作可以是从发送 Amazon SNS 通知到调用 AWS Lambda 函数的任何操作。

在本节中，我们将创建一个警报，在 Amazon EC2 实例的平均 CPU 使用率超过 50% 时发送 Amazon SNS 通知。

1. 转到 [https://console.aws.amazon.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/) 的 Amazon CloudWatch 控制台。

2. 在左侧导航面板中，单击**警报**。

3. 单击**创建警报**。

4. 选择指标 **CPUUtilization** 并单击 **Next**。

5.配置告警如下：

- 对于 **Statistic**，选择 **Average**。
- 对于 **Period**，输入 **60**。
- 对于 **Unit**，选择 **Seconds**。
- 对于 **阈值**，输入 **50**。
- 对于 **评估期**，输入 **2**。
- 对于 **Treat missing data**，选择 **Missing data as breaching**。
- 对于**操作**，选择操作**发送通知**。
- 对于 **Send a notification to**，选择您要接收通知的 Amazon SNS 主题。

6. 单击**创建警报**。

## 查看 CloudWatch 日志

CloudWatch Logs 允许您监控、存储和访问来自 Amazon EC2 实例、Amazon CloudTrail 或其他来源的日志文件。

在本节中，我们将向您展示如何查看 Amazon EC2 实例的 CloudWatch 日志。

1. 转到 [https://console.aws.amazon.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/) 的 Amazon CloudWatch 控制台。

2. 在左侧导航面板中，单击 **Logs**。

3. 选择您要查看其日志的日志组。

4. 选择您要查看的日志流。

5. 日志流将显示在右侧面板中。

## 参考

- [https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
- [https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html)
- [https://aws.amazon.com/blogs/aws/new-cloudwatch-logs-agent/](https://aws.amazon.com/blogs/aws/new-cloudwatch-logs-agent/)
- [https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html)