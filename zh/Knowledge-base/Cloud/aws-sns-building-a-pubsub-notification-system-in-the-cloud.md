---
title: AWS SNS：在云中构建发布/订阅通知系统
description: 
published: true
date: 2023-02-11T08:55:13.896Z
tags: 
editor: markdown
dateCreated: 2023-02-11T08:55:12.289Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [AWS SNS: Building a Pub/Sub Notification System in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-sns-building-a-pubsub-notification-system-in-the-cloud)
{.links-list}


# AWS SNS：在云中构建发布/订阅通知系统

在本文中，我们将了解如何使用 AWS SNS（简单通知服务）设置简单的发布/订阅通知系统。我们将涵盖从设置 SNS 主题到创建订阅和发送通知的所有内容。

## 设置 SNS 主题

第一步是创建 SNS 主题。这可以通过 AWS 管理控制台、AWS CLI 或 SDK 完成。

创建主题是一个简单的过程：

1. 转到 SNS 控制台并单击 **创建主题**。
2. 输入**主题名称**和**显示名称**。
3. 单击**创建主题**。

您现在应该在主题列表中看到您的新主题。

## 创建订阅

现在我们有了一个主题，我们需要创建一个订阅。这将允许我们指定我们的通知将传递到的端点。

1. 转到 **订阅** 选项卡并单击 **创建订阅**。
2. 在**主题 ARN** 下拉列表中选择您创建的主题。
3. 在**协议**下拉列表中，选择您要用于交付的协议。 AWS SNS 支持多种协议，包括 HTTP、HTTPS、电子邮件等。
4. 输入订阅的**端点**。这将是通知将发送到的 URL 或电子邮件地址。
5. 单击**创建订阅**。

您现在应该会在订阅列表中看到您的新订阅。

## 发送通知

现在我们已经设置了主题和订阅，可以发送第一个通知了。

1. 转到 **主题** 选项卡并选择您要向其发送通知的主题。
2. 单击**发布到主题**。
3. 输入通知的 **主题** 和 **消息**。
4. 点击**发布消息**。

您的通知现在将传送到您订阅中指定的端点。

## 结论

在本文中，我们了解了如何使用 AWS SNS 设置简单的发布/订阅通知系统。我们涵盖了从创建主题到创建订阅和发送通知的所有内容。借助 AWS SNS，可以轻松设置可用于向各种终端节点发送通知的通知系统。