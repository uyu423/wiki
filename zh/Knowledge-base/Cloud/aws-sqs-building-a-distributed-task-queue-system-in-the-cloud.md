---
title: AWS SQS：在云端构建分布式任务队列系统
description: 
published: true
date: 2023-02-17T18:16:29.730Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:05:23.343Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [AWS SQS: Building a Distributed Task Queue System in the Cloud***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-sqs-building-a-distributed-task-queue-system-in-the-cloud)
{.links-list}


# AWS SQS：在云端构建分布式任务队列系统

在本文中，我们将研究如何使用 Amazon Simple Queue Service (SQS) 构建分布式任务队列系统。我们将涵盖以下主题：

- 什么是任务队列？
- 为什么要使用任务队列？
- 什么是亚马逊 SQS？
- 开始使用 Amazon SQS
- 使用 Amazon SQS 构建分布式任务队列

## 什么是任务队列？

任务队列是用于管理和处理任务的系统。任务可以是任何需要完成的事情，例如发送电子邮件、处理图像或清理数据。

任务队列用于异步处理任务。这意味着任务被添加到队列中，稍后由工作人员处理。这与同步处理不同，同步处理是立即处理任务。

任务队列有以下好处：

- 它们可用于在后台处理任务，而不会阻塞主应用程序。
- 它们可用于通过使用多个 worker 来并行处理任务。
- 它们可用于在多台机器上分配工作。

## 为什么要使用任务队列？

您可能想要使用任务队列的原因有很多。这里有些例子：

- 您想在后台处理任务，而不阻塞主应用程序。
- 您想通过使用多个工作人员并行处理任务。
- 你想在多台机器上分配工作。

任务队列可用于各种任务。例如，您可以使用任务队列来：

- 发电子邮件
- 过程图像
- 清理数据
- 生成报告

## 什么是亚马逊 SQS？

Amazon Simple Queue Service (SQS) 是一种托管消息队列服务。它可用于构建分布式任务队列系统。

SQS 是一种可靠、可扩展且低成本的消息队列服务。它支持标准队列和先进先出 (FIFO) 队列。

## 开始使用 Amazon SQS

要使用 SQS，您首先需要创建一个 Amazon SQS 队列。这可以使用 AWS 管理控制台、AWS 命令行界面 (CLI) 或 AWS 开发工具包来完成。

创建队列后，您可以开始向其中添加消息。可以使用 AWS 管理控制台、AWS CLI 或 AWS SDK 添加消息。

一旦您将消息添加到队列中，它们就可以由工作人员处理。可以使用 AWS 管理控制台、AWS CLI 或 AWS 开发工具包创建工作人员。

## 使用 Amazon SQS 构建分布式任务队列

在本节中，我们将向您展示如何使用 Amazon SQS 构建分布式任务队列系统。我们将使用以下组件：

- 亚马逊 SQS
- 亚马逊弹性计算云 (EC2)
- 亚马逊简单通知服务 (SNS)

我们还将使用以下开源软件：

- 阿帕奇ActiveMQ
- 阿帕奇骆驼

### 创建一个 Amazon SQS 队列

第一步是创建一个 Amazon SQS 队列。这可以使用 AWS 管理控制台、AWS CLI 或 AWS 开发工具包来完成。

创建队列后，您需要对其进行配置。需要以下配置设置：

- 消息保留期：这是消息在被删除之前保留在队列中的时间。最短为四秒，最长为 14 天。

- 传递延迟：这是消息在传递给工作人员之前保留在队列中的时间。最短为零秒，最长为 15 分钟。

- 接收句柄：这是用于从队列中删除消息的标记。

- 可见性超时：这是消息在其他工作人员可见之前保留在队列中的时间。最小值为零秒，最大值为 12 小时。

### 创建一个 Amazon EC2 实例

下一步是创建一个 Amazon EC2 实例。这可以使用 AWS 管理控制台、AWS CLI 或 AWS 开发工具包来完成。

创建实例后，您需要对其进行配置。需要以下配置设置：

- 安全组：您需要创建一个安全组，允许端口 22 (SSH) 和端口 8080 (HTTP) 上的入站流量。

- 密钥对：您需要创建一个密钥对并将私钥存储在安全的地方。

- IAM角色：您需要创建一个允许EC2实例访问SQS的IAM角色。

### 安装和配置 Apache ActiveMQ

下一步是安装和配置 Apache ActiveMQ。 Apache ActiveMQ 是一个开源消息代理。

首先，您需要下载 Apache ActiveMQ。这可以使用以下命令完成：

```
wget http://www.apache.org/dyn/closer.cgi?filename=/activemq/5.15.8/apache-activemq-5.15.8-bin.tar.gz&action=download
```

Next, you need to extract the downloaded file. This can be done using the following command:

```
tar -xzf apache-activemq-5.15.8-bin.tar.gz
```

接下来，您需要切换到 ActiveMQ 目录。这可以使用以下命令完成：

```
cd apache-activemq-5.15.8/
```

接下来，您需要编辑 ActiveMQ 配置文件。这可以使用您最喜欢的文本编辑器来完成。例如，您可以使用以下命令：

```
nano conf/activemq.xml
```

ActiveMQ 配置文件有详细的文档记录。阅读文档并进行以下更改：

- 在```<broker>``` element, set the ```persistent="true"``` attribute.

- In the ```<transportConnectors>``` element, add the following ```<transportConnector>``` element:

```xml
<transportConnector name="sqs" uri="sqs://ACCESS_KEY_ID:SECRET_ACCESS_KEY@sqs.us-east-1.amazonaws.com:9324?queuePrefix=act" />
```

- In the ```<destinations>``` element, add the following ```<queue>``` element:

```xml
<队列物理名称="TASK_QUEUE_NAME" />
```

Replace ```TASK_QUEUE_NAME``` with the name of the Amazon SQS queue that you created earlier.

- In the ```<systemUsage>``` element, set the ```storeUsage>``` and ```tempUsage>``` elements to the following values:

```xml
<storeUsage limit="20 GB"/>
<tempUsage limit="10 GB"/>
```

This will ensure that the ActiveMQ broker does not run out of storage space.

- In the ```<plugins>``` element, add the following ```<statisticsBrokerPlugin>``` element:

```xml
<statisticsBrokerPlugin/>
```

This will enable ActiveMQ broker statistics.

- Save your changes and exit the text editor.

### Starting Apache ActiveMQ

The next step is to start the Apache ActiveMQ broker. This can be done using the following command:

```
bin/activemq 启动
```

You can check that the broker is running by executing the following command:

```
bin/activemq 状态
```

You should see the following output:

```
ACTIVEMQ_HOME: /home/ec2-user/apache-activemq-5.15.8
ACTIVEMQ_DATA: /home/ec2-user/apache-activemq-5.15.8/data
连接到代理 URL：sqs://ACCESS_KEY_ID:SECRET_ACCESS_KEY@sqs.us-east-1.amazonaws.com:9324?queuePrefix=act
包括：queue://TASK_QUEUE_NAME
日志：Apache ActiveMQ 5.15.8（本地主机，ID：ip-10-0-1-32.ec2.internal-39767-1588389434974-0:1）正在启动
向上
信息：如需帮助或更多信息，请参阅：http://activemq.apache.org
信息：ActiveMQ WebConsole 位于 http://0.0.0.0:8161/
信息：关闭 Spring 应用程序上下文。
信息：Apache ActiveMQ 5.15.8（本地主机，ID：ip-10-0-1-32.ec2.internal-39767-1588389434974-0:1）正常运行时间
37.528 秒
信息：Apache ActiveMQ 5.15.8（本地主机，ID：ip-10-0-1-32.ec2.internal-39767-1588389434974-0:1）是
关闭
```

If the broker is not running, you can start it using the following command:

```
bin/activemq 启动
```

### Installing and configuring Apache Camel

The next step is to install and configure Apache Camel. Apache Camel is an open-source integration framework.

First, you need to download Apache Camel. This can be done using the following command:

```
wget http://www.apache.org/dyn/closer.cgi?filename=/camel/2.23.1/apache-camel-2.23.1.tar.gz&action=download
```

接下来，您需要解压缩下载的文件。这可以使用以下命令完成：

```
tar -xzf apache-camel-2.23.1.tar.gz
```

Next, you need to change into the Camel directory. This can be done using the following command:

```
cd apache-camel-2.23.1/
```

Next, you need to create a configuration file. This can be done using your favorite text editor. For example, you could use the following command:

```
纳米会议/骆驼.xml
```

Add the following content to the file:

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="
  http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
  http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">
 
  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">
    <路线>
      <from uri="sqs://ACCESS_KEY_ID:SECRET_ACCESS_KEY@sqs.us-east-1.amazonaws.com:9324?queuePrefix=act&amp;delay=5000&concurrentConsumers=5&maxMessagesPerPoll=10"/>
      <to uri="activemq:TASK_QUEUE_NAME"/>
    </路线>
  </camelContext>
</豆子>
```

Replace ```ACCESS_KEY_ID``` and ```SECRET_ACCESS_KEY``` with your Amazon SQS access key id and secret access key. Replace ```TASK_QUEUE_NAME``` with the name of the Amazon SQS queue that you created earlier.

- Save your changes and exit the text editor.

### Running Apache Camel

The next step is to start Apache Camel. This can be done using the following command:

```
垃圾箱/骆驼
```

You can check that Apache Camel is running by executing the following command:

```
垃圾箱/骆驼状态
```

You should see the following output:

```
 骆驼没有跑。
```

If Apache Camel is not running, you can start it using the following command:

```
垃圾箱/骆驼开始
```

### Sending messages to the queue

The next step is to send messages to the Amazon SQS queue. This can be done using the AWS Management Console, AWS CLI, or AWS SDK.

Messages can be any JSON-formatted data. The following is an example message:

```json
{
  “任务”：“发送电子邮件”，
  “至”：“john@example.com”，
  “来自”：“noreply@example.com”，
  "subject": "你好约翰",
  "body": "你好约翰，\n\n这是一条来自任务队列的消息。"
}
```

### Processing messages

Messages in the Amazon SQS queue can be processed by workers. Workers can be created using the AWS Management Console, AWS CLI, or AWS SDK.

Workers can be any type of program, such as a web application, a command-line program, or a script. The following is an example worker written in PHP:

```PHP
<?php

// 检查是否收到消息。
如果 (!empty($_GET['message'])) {
  //解码消息。
  $message = json_decode($_GET['message']);
 
  // 处理消息。
  切换（$消息->任务）{
    案例“发送电子邮件”：
      // 发送邮件。
      邮件($message->to, $message->subject, $message->body, 'From: '. $message->from);
      休息;
 
    案例'process_image'：
      // 处理图像。
      // ...
      休息;
 
    案例“cleanup_data”：
      // 清理数据。
      // ...
      休息;
 
    案例“generate_report”：
      // 生成报告。
      // ...
      休息;
  }
}
```

## 结论

在本文中，我们了解了如何使用 Amazon Simple Queue Service (SQS) 构建分布式任务队列系统。我们涵盖了以下主题：

- 什么是任务队列？
- 为什么要使用任务队列？
- 什么是亚马逊 SQS？
- 开始使用 Amazon SQS
- 使用 Amazon SQS 构建分布式任务队列

如果您有任何问题，请随时在评论中发表。