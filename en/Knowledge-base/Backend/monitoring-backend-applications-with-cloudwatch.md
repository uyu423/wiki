---
title: Monitoring Backend Applications with CloudWatch
description: 
published: true
date: 2023-02-10T01:55:40.550Z
tags: 
editor: markdown
dateCreated: 2023-02-10T01:55:33.777Z
---

- [Supervisión de aplicaciones back-end con CloudWatch***Spanish** document is available*](/es/Knowledge-base/Backend/monitoring-backend-applications-with-cloudwatch)
{.links-list}
- [使用 CloudWatch 监控后端应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Backend/monitoring-backend-applications-with-cloudwatch)
{.links-list}
- [CloudWatch로 백엔드 애플리케이션 모니터링***Korean** document is available*](/ko/Knowledge-base/Backend/monitoring-backend-applications-with-cloudwatch)
{.links-list}


#Monitoring Backend Applications with CloudWatch

CloudWatch is a monitoring service for AWS cloud resources and the applications running on AWS. CloudWatch collects monitoring and operational data in the form of logs, metrics, and events, which can be used to troubleshoot and optimize your applications.

In this article, we will focus on how to use CloudWatch to monitor backend applications. We will cover the following topics:

- What is CloudWatch?
- Setting up CloudWatch
- Creating a CloudWatch alarm
- Viewing CloudWatch logs

##What is CloudWatch?

As mentioned earlier, CloudWatch is a monitoring service for AWS cloud resources and the applications running on AWS. With CloudWatch, you can collect and track metrics, set alarms, and automatically react to changes in your AWS resources.

CloudWatch provides you with data and actionable insights to monitor your applications, respond to system-wide performance changes, optimize resource utilization, and get a unified view of operational health.

##Setting up CloudWatch

In order to use CloudWatch, you first need to set up an AWS account and create an Amazon CloudWatch Logs group.

1. To set up an AWS account, go to [https://aws.amazon.com/](https://aws.amazon.com/) and click **Create an AWS Account**.

2. Follow the instructions to create your account.

3. Once you have created your account, go to the Amazon CloudWatch console at [https://console.aws.amazon.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/).

4. In the left navigation panel, click **Logs**.

5. Click **Create log group**.

6. Enter a name for your log group and click **Create log group**.

##Creating a CloudWatch Alarm

An alarm watches a metric over a time period that you specify, and performs one or more actions based on the value of the metric relative to a threshold that you set. The actions can be anything from sending an Amazon SNS notification to calling an AWS Lambda function.

In this section, we will create an alarm that sends an Amazon SNS notification when the average CPU utilization of an Amazon EC2 instance exceeds 50%.

1. Go to the Amazon CloudWatch console at [https://console.aws.amazon.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/).

2. In the left navigation panel, click **Alarms**.

3. Click **Create alarm**.

4. Select the metric **CPUUtilization** and click **Next**.

5. Configure the alarm as follows:

- For **Statistic**, select **Average**.
- For **Period**, enter **60**.
- For **Unit**, select **Seconds**.
- For **Threshold**, enter **50**.
- For **Evaluation period**, enter **2**.
- For **Treat missing data**, select **Missing data as breaching**.
- For **Actions**, select the action **Send a notification**.
- For **Send a notification to**, select the Amazon SNS topic that you want to receive the notification.

6. Click **Create alarm**.

##Viewing CloudWatch Logs

CloudWatch Logs allows you to monitor, store, and access your log files from Amazon EC2 instances, Amazon CloudTrail, or other sources.

In this section, we will show you how to view CloudWatch logs for an Amazon EC2 instance.

1. Go to the Amazon CloudWatch console at [https://console.aws.amazon.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/).

2. In the left navigation panel, click **Logs**.

3. Select the log group that you want to view the logs for.

4. Select the log stream that you want to view.

5. The log stream will be displayed in the right panel.

##References

- [https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
- [https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html)
- [https://aws.amazon.com/blogs/aws/new-cloudwatch-logs-agent/](https://aws.amazon.com/blogs/aws/new-cloudwatch-logs-agent/)
- [https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html)