---
title: AWS SNS & SQS: Building a Message Broker System in the Cloud
description: 
published: true
date: 2023-02-02T03:23:58.103Z
tags: 
editor: markdown
dateCreated: 2023-02-02T03:23:53.881Z
---

- [AWS SNS y SQS: creación de un sistema de intermediario de mensajes en la nube***Spanish** document is available*](/es/Knowledge-base/Cloud/aws-sns--sqs-building-a-message-broker-system-in-the-cloud)
{.links-list}
- [AWS SNS 和 SQS：在云中构建消息代理系统***Chinese Simplified** document is available*](/zh/Knowledge-base/Cloud/aws-sns--sqs-building-a-message-broker-system-in-the-cloud)
{.links-list}
- [AWS SNS 및 SQS: 클라우드에서 메시지 브로커 시스템 구축***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-sns--sqs-building-a-message-broker-system-in-the-cloud)
{.links-list}


# AWS SNS & SQS: Building a Message Broker System in the Cloud

In this article, we'll look at how to use AWS SNS and SQS to build a message broker system in the cloud. We'll explore the benefits of using a message broker and how it can help with processing and routing messages between different services. We'll also look at some code examples to show how to set up and use SNS and SQS in your own applications.

## What is a message broker?

A message broker is a system that helps to process and route messages between different software applications. It can provide a number of benefits, such as:

- improved performance by decoupling message-sending and message-processing
- greater flexibility in how messages are routed
- the ability to handle a large number of messages
- easier management of message queues

Message brokers are often used in applications that need to process a large number of messages, or where messages need to be routed between different services. For example, a message broker could be used to process orders from a website and route them to the correct fulfilment service.

## What are SNS and SQS?

SNS and SQS are two services from Amazon Web Services (AWS) that can be used to build a message broker system.

SNS is a pub/sub messaging service that can be used to send messages to a number of different subscribers. It can be used to fan out messages to multiple subscribers, or to send messages to a specific subscriber.

SQS is a message queue service that can be used to store messages until they can be processed. It can be used to decouple message-sending and message-processing, or to process messages in batches.

## Setting up SNS and SQS

In order to use SNS and SQS, you'll need to set up an AWS account and create a new SNS topic and SQS queue.

Creating an SNS topic is a two-step process. First, you need to create the topic, and then you need to subscribe to the topic. To create a new SNS topic, you can use the AWS Management Console, or you can use the AWS CLI.

To create a new SNS topic using the AWS Management Console, log in to the console and navigate to the SNS service. Click on the "Create topic" button and enter a name and description for your topic. Once the topic has been created, you can subscribe to it by clicking on the "Subscribe to topic" button and entering the details of the subscription.

To create a new SNS topic using the AWS CLI, you can use the following command:

```
aws sns create-topic --name my-topic
```

To subscribe to the topic, you can use the following command:

```
aws sns subscribe --topic-arn arn:aws:sns:us-east-1:123456789012:my-topic --protocol email --notification-endpoint myemail@example.com
```

Creating an SQS queue is a three-step process. First, you need to create the queue, then you need to set up the permissions, and finally you need to subscribe to the queue. To create a new SQS queue, you can use the AWS Management Console, or you can use the AWS CLI.

To create a new SQS queue using the AWS Management Console, log in to the console and navigate to the SQS service. Click on the "Create queue" button and enter a name and description for your queue. Once the queue has been created, you can set the permissions by clicking on the "Permissions" tab and adding a new permission. Finally, you can subscribe to the queue by clicking on the "Subscribe to topic" button and entering the details of the subscription.

To create a new SQS queue using the AWS CLI, you can use the following command:

```
aws sqs create-queue --queue-name my-queue
```

To set the permissions, you can use the following command:

```
aws sqs set-queue-attributes --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue --attributes '{"Policy":"{\"Version\":\"2012-10-17\",\"Id\":\"MyQueuePolicy\",\"Statement\":[{\"Sid\":\"MyQueueSid\",\"Effect\":\"Allow\",\"Principal\":{\"AWS\":\"*\"},\"Action\":\"sqs:SendMessage\",\"Resource\":\"arn:aws:sqs:us-east-1:123456789012:my-queue\",\"Condition\":{\"ArnLike\":{\"aws:SourceArn\":\"arn:aws:sns:us-east-1:123456789012:my-topic\"}}}]}"}'
```

To subscribe to the queue, you can use the following command:

```
aws sqs subscribe-queue --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue --topic-arn arn:aws:sns:us-east-1:123456789012:my-topic
```

## Sending messages

Now that you have set up your SNS topic and SQS queue, you can start sending messages. To send a message, you can use the AWS Management Console, or you can use the AWS CLI.

To send a message using the AWS Management Console, log in to the console and navigate to the SNS service. Click on the "Create message" button and enter the details of the message. You can also specify the number of messages to send and the time to live for the message. Once the message has been created, you can click on the "Publish message" button to send the message.

To send a message using the AWS CLI, you can use the following command:

```
aws sns publish --topic-arn arn:aws:sns:us-east-1:123456789012:my-topic --message "Hello, world!"
```

## Receiving messages

Once you have sent a message, it will be stored in the SQS queue. To receive the message, you can use the AWS Management Console, or you can use the AWS CLI.

To receive a message using the AWS Management Console, log in to the console and navigate to the SQS service. Click on the "Get messages" button and select the number of messages to retrieve. You can also specify the time to live for the message and the visibility timeout. Once the message has been retrieved, you can click on the "Delete message" button to delete it from the queue.

To receive a message using the AWS CLI, you can use the following command:

```
aws sqs receive-message --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue
```

## Conclusion

In this article, we've looked at how to use AWS SNS and SQS to build a message broker system in the cloud. We've seen how a message broker can provide a number of benefits, and how SNS and SQS can be used to send and receive messages. We've also looked at some code examples to show how to set up and use SNS and SQS in your own applications.