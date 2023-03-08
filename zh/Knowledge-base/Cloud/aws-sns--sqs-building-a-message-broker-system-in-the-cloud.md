---
title: AWS SNS 和 SQS：在云中构建消息代理系统
description: 
published: true
date: 2023-02-02T03:23:55.506Z
tags: 
editor: markdown
dateCreated: 2023-02-02T03:23:53.858Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [AWS SNS & SQS: Building a Message Broker System in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-sns--sqs-building-a-message-broker-system-in-the-cloud)
{.links-list}


# AWS SNS 和 SQS：在云中构建消息代理系统

在本文中，我们将了解如何使用 AWS SNS 和 SQS 在云中构建消息代理系统。我们将探索使用消息代理的好处，以及它如何帮助处理和路由不同服务之间的消息。我们还将查看一些代码示例，以展示如何在您自己的应用程序中设置和使用 SNS 和 SQS。

## 什么是消息代理？

消息代理是一种有助于在不同软件应用程序之间处理和路由消息的系统。它可以提供许多好处，例如：

- 通过解耦消息发送和消息处理来提高性能
- 更灵活地路由消息
- 处理大量消息的能力
- 更容易管理消息队列

消息代理通常用于需要处理大量消息的应用程序，或者需要在不同服务之间路由消息的应用程序。例如，消息代理可用于处理来自网站的订单并将它们路由到正确的履行服务。

## 什么是 SNS 和 SQS？

SNS 和 SQS 是来自 Amazon Web Services (AWS) 的两项服务，可用于构建消息代理系统。

SNS 是一种发布/订阅消息服务，可用于向多个不同的订阅者发送消息。它可用于向多个订阅者发送消息，或向特定订阅者发送消息。

SQS 是一种消息队列服务，可用于存储消息，直到它们可以被处理为止。它可以用来解耦消息发送和消息处理，或者批量处理消息。

## 设置 SNS 和 SQS

为了使用 SNS 和 SQS，您需要设置一个 AWS 账户并创建一个新的 SNS 主题和 SQS 队列。

创建 SNS 主题是一个两步过程。首先需要创建主题，然后需要订阅主题。要创建新的 SNS 主题，您可以使用 AWS 管理控制台，也可以使用 AWS CLI。

要使用 AWS 管理控制台创建新的 SNS 主题，请登录控制台并导航至 SNS 服务。单击“创建主题”按钮并为您的主题输入名称和描述。创建主题后，您可以通过单击“订阅主题”按钮并输入订阅详细信息来订阅它。

要使用 AWS CLI 创建新的 SNS 主题，您可以使用以下命令：

```
aws sns create-topic --name my-topic
```

要订阅主题，您可以使用以下命令：

```
aws sns subscribe --topic-arn arn:aws:sns:us-east-1:123456789012:my-topic --protocol email --notification-endpoint myemail@example.com
```

创建 SQS 队列是一个三步过程。首先需要创建队列，然后需要设置权限，最后需要订阅队列。要创建新的 SQS 队列，您可以使用 AWS 管理控制台，也可以使用 AWS CLI。

要使用 AWS 管理控制台创建新的 SQS 队列，请登录控制台并导航到 SQS 服务。单击“创建队列”按钮并输入队列的名称和描述。创建队列后，您可以通过单击“权限”选项卡并添加新权限来设置权限。最后，您可以通过单击“订阅主题”按钮并输入订阅的详细信息来订阅队列。

要使用 AWS CLI 创建新的 SQS 队列，您可以使用以下命令：

```
aws sqs create-queue --queue-name my-queue
```

要设置权限，您可以使用以下命令：

```
aws sqs set-queue-attributes --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue --attributes '{"Policy":"{\"Version\":\"2012-10-17\",\"Id\":\"MyQueuePolicy\",\"Statement\":[{\"Sid\":\"MyQueueSid\",\"Effect\":\"Allow\",\"Principal\":{\"AWS\":\"*\"},\"Action\":\"sqs:SendMessage\",\"Resource\":\"arn:aws:sqs:us-east-1:123456789012:my-queue\",\"Condition\":{\"ArnLike\":{\"aws:SourceArn\":\"arn:aws:sns:us-east-1:123456789012:my-topic\"}}}]}"}'
```

要订阅队列，您可以使用以下命令：

```
aws sqs subscribe-queue --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue --topic-arn arn:aws:sns:us-east-1:123456789012:my-topic
```

## 发送消息

现在您已经设置了 SNS 主题和 SQS 队列，您可以开始发送消息了。要发送消息，您可以使用 AWS 管理控制台，也可以使用 AWS CLI。

要使用 AWS 管理控制台发送消息，请登录控制台并导航至 SNS 服务。单击“创建消息”按钮并输入消息的详细信息。您还可以指定要发送的消息数和消息的生存时间。创建消息后，您可以单击“发布消息”按钮发送消息。

要使用 AWS CLI 发送消息，您可以使用以下命令：

```
aws sns publish --topic-arn arn:aws:sns:us-east-1:123456789012:my-topic --message "Hello, world!"
```

## 接收消息

发送消息后，它将存储在 SQS 队列中。要接收消息，您可以使用 AWS 管理控制台，也可以使用 AWS CLI。

要使用 AWS 管理控制台接收消息，请登录控制台并导航至 SQS 服务。单击“获取消息”按钮并选择要检索的消息数。您还可以指定消息的生存时间和可见性超时。检索到消息后，您可以单击“删除消息”按钮将其从队列中删除。

要使用 AWS CLI 接收消息，您可以使用以下命令：

```
aws sqs receive-message --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue
```

## 结论

在本文中，我们了解了如何使用 AWS SNS 和 SQS 在云中构建消息代理系统。我们已经看到了消息代理如何提供许多好处，以及如何使用 SNS 和 SQS 来发送和接收消息。我们还查看了一些代码示例，以展示如何在您自己的应用程序中设置和使用 SNS 和 SQS。