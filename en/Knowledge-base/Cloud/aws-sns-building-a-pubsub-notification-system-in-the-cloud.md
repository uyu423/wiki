---
title: AWS SNS: Building a Pub/Sub Notification System in the Cloud
description: 
published: true
date: 2023-02-11T08:55:18.973Z
tags: 
editor: markdown
dateCreated: 2023-02-11T08:55:12.296Z
---

- [AWS SNS: creación de un sistema de notificación de Pub/Sub en la nube***Spanish** document is available*](/es/Knowledge-base/Cloud/aws-sns-building-a-pubsub-notification-system-in-the-cloud)
{.links-list}
- [AWS SNS：在云中构建发布/订阅通知系统***Chinese Simplified** document is available*](/zh/Knowledge-base/Cloud/aws-sns-building-a-pubsub-notification-system-in-the-cloud)
{.links-list}
- [AWS SNS: 클라우드에서 Pub/Sub 알림 시스템 구축***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-sns-building-a-pubsub-notification-system-in-the-cloud)
{.links-list}


# AWS SNS: Building a Pub/Sub Notification System in the Cloud

In this article, we're going to take a look at how to set up a simple pub/sub notification system using AWS SNS (Simple Notification Service). We'll cover everything from setting up an SNS topic to creating a subscription and sending a notification.

## Setting up an SNS Topic

The first step is to create an SNS topic. This can be done through the AWS Management Console, AWS CLI, or SDK.

Creating a topic is a simple process:

1. Go to the SNS console and click **Create topic**.
2. Enter a **Topic name** and **Display name**.
3. Click **Create topic**.

You should now see your new topic in the list of topics.

## Creating a Subscription

Now that we have a topic, we need to create a subscription. This will allow us to specify the endpoint that our notifications will be delivered to.

1. Go to the **Subscriptions** tab and click **Create subscription**.
2. Select the topic you created in the **Topic ARN** drop-down.
3. In the **Protocol** drop-down, select the protocol you want to use for delivery. AWS SNS supports a variety of protocols, including HTTP, HTTPS, email, and more.
4. Enter the **Endpoint** for your subscription. This will be the URL or email address that notifications will be delivered to.
5. Click **Create subscription**.

You should now see your new subscription in the list of subscriptions.

## Sending a Notification

Now that we have a topic and subscription set up, we're ready to send our first notification.

1. Go to the **Topics** tab and select the topic you want to send a notification to.
2. Click **Publish to topic**.
3. Enter a **Subject** and **Message** for your notification.
4. Click **Publish message**.

Your notification will now be delivered to the endpoint specified in your subscription.

## Conclusion

In this article, we've seen how to set up a simple pub/sub notification system using AWS SNS. We've covered everything from creating a topic to creating a subscription and sending a notification. With AWS SNS, it's easy to set up a notification system that can be used to send notifications to a variety of endpoints.