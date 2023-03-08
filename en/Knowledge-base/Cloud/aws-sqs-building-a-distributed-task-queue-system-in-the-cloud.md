---
title: AWS SQS: Building a Distributed Task Queue System in the Cloud
description: 
published: true
date: 2023-02-17T18:16:26.782Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:05:23.342Z
---

- [AWS SQS: 클라우드에서 분산 작업 대기열 시스템 구축***Korean** version of this document is available*](/ko/Knowledge-base/Cloud/aws-sqs-building-a-distributed-task-queue-system-in-the-cloud)
{.links-list}
- [AWS SQS: クラウドでの分散タスク キュー システムの構築***Japanese** version of this document is available*](/ja/Knowledge-base/Cloud/aws-sqs-building-a-distributed-task-queue-system-in-the-cloud)
{.links-list}
- [AWS SQS：在云端构建分布式任务队列系统***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Cloud/aws-sqs-building-a-distributed-task-queue-system-in-the-cloud)
{.links-list}


# AWS SQS: Building a Distributed Task Queue System in the Cloud

In this article, we'll be looking at how to build a distributed task queue system using Amazon Simple Queue Service (SQS). We'll cover the following topics:

- What is a task queue?
- Why use a task queue?
- What is Amazon SQS?
- Getting started with Amazon SQS
- Building a distributed task queue with Amazon SQS

## What is a task queue?

A task queue is a system for managing and processing tasks. Tasks can be anything that needs to be done, such as sending an email, processing an image, or cleaning up data.

Task queues are used to process tasks asynchronously. This means that the task is added to the queue and then processed by a worker at a later time. This is different from synchronous processing, where the task is processed immediately.

Task queues have the following benefits:

- They can be used to process tasks in the background, without blocking the main application.
- They can be used to process tasks in parallel, by using multiple workers.
- They can be used to distribute work across multiple machines.

## Why use a task queue?

There are many reasons why you might want to use a task queue. Here are some examples:

- You want to process tasks in the background, without blocking the main application.
- You want to process tasks in parallel, by using multiple workers.
- You want to distribute work across multiple machines.

Task queues can be used for a variety of tasks. For example, you could use a task queue to:

- Send emails
- Process images
- Clean up data
- Generate reports

## What is Amazon SQS?

Amazon Simple Queue Service (SQS) is a managed message queue service. It can be used to build distributed task queue systems.

SQS is a reliable, scalable, and low-cost message queue service. It supports both standard and first-in-first-out (FIFO) queues.

## Getting started with Amazon SQS

To use SQS, you first need to create an Amazon SQS queue. This can be done using the AWS Management Console, AWS Command Line Interface (CLI), or AWS SDK.

Once you have created a queue, you can start adding messages to it. Messages can be added using the AWS Management Console, AWS CLI, or AWS SDK.

Once you have added messages to the queue, they can be processed by workers. Workers can be created using the AWS Management Console, AWS CLI, or AWS SDK.

## Building a distributed task queue with Amazon SQS

In this section, we'll show you how to use Amazon SQS to build a distributed task queue system. We'll use the following components:

- Amazon SQS
- Amazon Elastic Compute Cloud (EC2)
- Amazon Simple Notification Service (SNS)

We'll also use the following open-source software:

- Apache ActiveMQ
- Apache Camel

### Creating an Amazon SQS queue

The first step is to create an Amazon SQS queue. This can be done using the AWS Management Console, AWS CLI, or AWS SDK.

Once the queue has been created, you need to configure it. The following configuration settings are required:

- Message retention period: This is the time that a message will remain in the queue before it is deleted. The minimum is four seconds, and the maximum is 14 days.

- Delivery delay: This is the time that a message will remain in the queue before it is delivered to a worker. The minimum is zero seconds, and the maximum is 15 minutes.

- Receipt handle: This is a token that is used to delete a message from the queue.

- Visibility timeout: This is the time that a message will remain in the queue before it is visible to other workers. The minimum is zero seconds, and the maximum is 12 hours.

### Creating an Amazon EC2 instance

The next step is to create an Amazon EC2 instance. This can be done using the AWS Management Console, AWS CLI, or AWS SDK.

Once the instance has been created, you need to configure it. The following configuration settings are required:

- Security groups: You need to create a security group that allows inbound traffic on port 22 (SSH) and port 8080 (HTTP).

- Key pair: You need to create a key pair and store the private key in a safe place.

- IAM role: You need to create an IAM role that allows the EC2 instance to access SQS.

### Installing and configuring Apache ActiveMQ

The next step is to install and configure Apache ActiveMQ. Apache ActiveMQ is an open-source message broker.

First, you need to download Apache ActiveMQ. This can be done using the following command:

```
wget http://www.apache.org/dyn/closer.cgi?filename=/activemq/5.15.8/apache-activemq-5.15.8-bin.tar.gz&action=download
```

Next, you need to extract the downloaded file. This can be done using the following command:

```
tar -xzf apache-activemq-5.15.8-bin.tar.gz
```

Next, you need to change into the ActiveMQ directory. This can be done using the following command:

```
cd apache-activemq-5.15.8/
```

Next, you need to edit the ActiveMQ configuration file. This can be done using your favorite text editor. For example, you could use the following command:

```
nano conf/activemq.xml
```

The ActiveMQ configuration file is well-documented. Read the documentation and make the following changes:

- In the ```<broker>``` element, set the ```persistent="true"``` attribute.

- In the ```<transportConnectors>``` element, add the following ```<transportConnector>``` element:

```xml
<transportConnector name="sqs" uri="sqs://ACCESS_KEY_ID:SECRET_ACCESS_KEY@sqs.us-east-1.amazonaws.com:9324?queuePrefix=act" />
```

- In the ```<destinations>``` element, add the following ```<queue>``` element:

```xml
<queue physicalName="TASK_QUEUE_NAME" />
```

Replace ```TASK_QUEUE_NAME``` with the name of the Amazon SQS queue that you created earlier.

- In the ```<systemUsage>``` element, set the ```storeUsage>``` and ```tempUsage>``` elements to the following values:

```xml
<storeUsage limit="20 gb"/>
<tempUsage limit="10 gb"/>
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
bin/activemq start
```

You can check that the broker is running by executing the following command:

```
bin/activemq status
```

You should see the following output:

```
ACTIVEMQ_HOME: /home/ec2-user/apache-activemq-5.15.8
ACTIVEMQ_DATA: /home/ec2-user/apache-activemq-5.15.8/data
Connecting to broker URL: sqs://ACCESS_KEY_ID:SECRET_ACCESS_KEY@sqs.us-east-1.amazonaws.com:9324?queuePrefix=act
including: queue://TASK_QUEUE_NAME
LOG: Apache ActiveMQ 5.15.8 (localhost, ID:ip-10-0-1-32.ec2.internal-39767-1588389434974-0:1) is starting
up
INFO: For help or more information please see: http://activemq.apache.org
INFO: ActiveMQ WebConsole available at http://0.0.0.0:8161/
INFO: Closing Spring application context.
INFO: Apache ActiveMQ 5.15.8 (localhost, ID:ip-10-0-1-32.ec2.internal-39767-1588389434974-0:1) uptime
37.528 seconds
INFO: Apache ActiveMQ 5.15.8 (localhost, ID:ip-10-0-1-32.ec2.internal-39767-1588389434974-0:1) is
shutting down
```

If the broker is not running, you can start it using the following command:

```
bin/activemq start
```

### Installing and configuring Apache Camel

The next step is to install and configure Apache Camel. Apache Camel is an open-source integration framework.

First, you need to download Apache Camel. This can be done using the following command:

```
wget http://www.apache.org/dyn/closer.cgi?filename=/camel/2.23.1/apache-camel-2.23.1.tar.gz&action=download
```

Next, you need to extract the downloaded file. This can be done using the following command:

```
tar -xzf apache-camel-2.23.1.tar.gz
```

Next, you need to change into the Camel directory. This can be done using the following command:

```
cd apache-camel-2.23.1/
```

Next, you need to create a configuration file. This can be done using your favorite text editor. For example, you could use the following command:

```
nano conf/camel.xml
```

Add the following content to the file:

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="
  http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
  http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">
 
  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">
    <route>
      <from uri="sqs://ACCESS_KEY_ID:SECRET_ACCESS_KEY@sqs.us-east-1.amazonaws.com:9324?queuePrefix=act&amp;delay=5000&concurrentConsumers=5&maxMessagesPerPoll=10"/>
      <to uri="activemq:TASK_QUEUE_NAME"/>
    </route>
  </camelContext>
</beans>
```

Replace ```ACCESS_KEY_ID``` and ```SECRET_ACCESS_KEY``` with your Amazon SQS access key id and secret access key. Replace ```TASK_QUEUE_NAME``` with the name of the Amazon SQS queue that you created earlier.

- Save your changes and exit the text editor.

### Running Apache Camel

The next step is to start Apache Camel. This can be done using the following command:

```
bin/camel
```

You can check that Apache Camel is running by executing the following command:

```
bin/camel status
```

You should see the following output:

```
 Camel is not running.
```

If Apache Camel is not running, you can start it using the following command:

```
bin/camel start
```

### Sending messages to the queue

The next step is to send messages to the Amazon SQS queue. This can be done using the AWS Management Console, AWS CLI, or AWS SDK.

Messages can be any JSON-formatted data. The following is an example message:

```json
{
  "task": "send_email",
  "to": "john@example.com",
  "from": "noreply@example.com",
  "subject": "Hello John",
  "body": "Hello John,\n\nThis is a message from the task queue."
}
```

### Processing messages

Messages in the Amazon SQS queue can be processed by workers. Workers can be created using the AWS Management Console, AWS CLI, or AWS SDK.

Workers can be any type of program, such as a web application, a command-line program, or a script. The following is an example worker written in PHP:

```php
<?php

// Check if a message has been received.
if (!empty($_GET['message'])) {
  // Decode the message.
  $message = json_decode($_GET['message']);
 
  // Process the message.
  switch ($message->task) {
    case 'send_email':
      // Send the email.
      mail($message->to, $message->subject, $message->body, 'From: ' . $message->from);
      break;
 
    case 'process_image':
      // Process the image.
      // ...
      break;
 
    case 'cleanup_data':
      // Clean up the data.
      // ...
      break;
 
    case 'generate_report':
      // Generate the report.
      // ...
      break;
  }
}
```

## Conclusion

In this article, we've looked at how to build a distributed task queue system using Amazon Simple Queue Service (SQS). We've covered the following topics:

- What is a task queue?
- Why use a task queue?
- What is Amazon SQS?
- Getting started with Amazon SQS
- Building a distributed task queue with Amazon SQS

If you have any questions, feel free to post them in the comments.