---
title: Debugging Cloud Services: Best Practices for AWS and Azure
description: 
published: true
date: 2023-02-19T05:06:31.103Z
tags: 
editor: markdown
dateCreated: 2023-02-19T05:06:24.206Z
---

- [클라우드 서비스 디버깅: AWS 및 Azure 모범 사례***Korean** document is available*](/ko/Knowledge-base/Cloud/debugging-cloud-services-best-practices-for-aws-and-azure)
{.links-list}


# Debugging Cloud Services: Best Practices for AWS and Azure

The cloud is a great place to run your applications. However, when things go wrong, it can be difficult to debug your cloud-based applications. In this article, we'll share some best practices for debugging cloud services on AWS and Azure.

## Logging

One of the most important things you can do when debugging your cloud-based applications is to enable logging. AWS and Azure both provide great logging capabilities.

### AWS CloudTrail

AWS CloudTrail is a service that provides visibility into your AWS account. It enables you to log, monitor, and retain account activity and API calls. CloudTrail provides event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command line tools, and other AWS services. This event history simplifies security analysis, resource change tracking, and compliance auditing.

To enable CloudTrail logging in your AWS account, visit the [CloudTrail console](https://console.aws.amazon.com/cloudtrail/home). Click the **Create Trail** button and enter a name for your trail. Then, select the **All events** checkbox and click **Create Trail**.

### Azure Activity Log

The Azure Activity Log provides information about actions that were taken on your Azure resources. It can be used to answer the question: "What happened to my Azure resources?" The Azure Activity Log is written to a storage account, and you can use the Log Analytics service to query the activity log.

To enable the Azure Activity Log, visit the [Activity Log](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) blade in the Azure portal. Click the **Turn on diagnostics logging** button and select the **Send to Log Analytics** option.

## Monitoring

In addition to logging, it's important to monitor your cloud-based applications. AWS and Azure both provide great monitoring capabilities.

### AWS CloudWatch

AWS CloudWatch is a service that provides monitoring for AWS resources and applications. CloudWatch collects monitoring and operational data in the form of logs, metrics, and events. You can use CloudWatch to set alarms, and respond to changes in your AWS resources.

To create a CloudWatch alarm, visit the [CloudWatch console](https://console.aws.amazon.com/cloudwatch/home). Click the **Create Alarm** button and select the **Metric** you want to monitor. Then, select the **Statistic**, **Period**, and **Unit**. Finally, enter the **Threshold** and click **Create Alarm**.

### Azure Monitor

Azure Monitor is a service that provides monitoring for Azure resources and applications. Azure Monitor collects monitoring and diagnostic data in the form of logs, metrics, and events. You can use Azure Monitor to set alerts, and respond to changes in your Azure resources.

To create an Azure Monitor alert, visit the [Azure Monitor](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview) blade in the Azure portal. Click the **Add alert rule** button and select the **Metric** you want to monitor. Then, select the **Operator**, **Threshold**, and **Period**. Finally, click the **Add alert rule** button.

## Conclusion

In this article, we've shared some best practices for debugging cloud services on AWS and Azure. Logging and monitoring are both important tools that can help you debug your cloud-based applications.