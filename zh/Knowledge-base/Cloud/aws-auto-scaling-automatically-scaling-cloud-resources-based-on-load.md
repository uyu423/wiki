---
title: AWS Auto Scaling：根据负载自动扩展云资源
description: 
published: true
date: 2023-01-31T20:23:51.850Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:23:50.280Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [AWS Auto Scaling: Automatically Scaling Cloud Resources Based on Load***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-auto-scaling-automatically-scaling-cloud-resources-based-on-load)
{.links-list}


# AWS Auto Scaling：根据负载自动扩展云资源

Auto Scaling 是一种云计算功能，使组织能够根据需求自动扩展或缩减其 Amazon Web Services (AWS) 资源，从而节省资金并确保资源在需要时可用。

AWS Auto Scaling 是一种经济高效的方式，可确保您的 AWS 资源在您需要时可用，并且您不会为闲置的资源付费。通过确保应用程序拥有处理流量高峰所需的资源，这也是提高应用程序性能的好方法。

Auto Scaling 是 Amazon Elastic Compute Cloud (EC2)、Amazon Elastic Container Service (ECS)、Amazon Relational Database Service (RDS) 和其他 AWS 服务的一项功能。

配置 Auto Scaling 时，您可以指定希望 AWS 为您维护的最小和最大实例数。然后，AWS 将根据需要添加或删除实例，以确保您不超出这些限制。您还可以指定扩展策略，以确定 AWS 应该如何扩展或缩减您的资源。例如，您可以指定希望 AWS 在您的 CPU 使用率超过 80% 时添加更多实例。

AWS Auto Scaling 是节省 AWS 账单费用和提高应用程序性能的好方法。但是，了解自动缩放的工作原理并正确配置它很重要，因为如果使用不当，它可能会产生意想不到的后果。

## AWS Auto Scaling 的工作原理

AWS Auto Scaling 通过维护一组称为“队列”的 EC2 实例来工作。该队列由“自动缩放组”(ASG) 管理，它是一组设置，用于确定应如何扩大或缩小队列。

ASG 包含许多可配置的设置，包括最小和最大实例数、所需容量和扩展策略。

创建 ASG 时，您必须指定希望它维护的最小和最大实例数。然后，ASG 将根据需要扩大或缩小机队规模，以使您保持在这些限制范围内。

您还可以指定所需容量，即您希望 ASG 在任何给定时间维护的实例数。 ASG 将根据需要扩大或缩小机队规模，以达到所需容量。

ASG 还包含许多扩展策略。这些政策决定了 ASG 应如何扩大或缩小机队规模以响应需求变化。

例如，您可以指定一个扩展策略，在 CPU 使用率超过 80% 时添加更多实例。当 CPU 使用率超过 80% 时，此策略会导致 ASG 向队列中添加更多实例。

您还可以指定扩展策略，以确定 ASG 应如何扩展队列以响应每秒请求数 (RPS) 或每秒字节数 (BPS) 的变化。

Auto Scaling 是节省 AWS 账单费用和提高应用程序性能的好方法。但是，了解自动缩放的工作原理并正确配置它很重要，因为如果使用不当，它可能会产生意想不到的后果。

## 配置 AWS 自动缩放

AWS 自动缩放是 Amazon EC2、Amazon ECS、Amazon RDS 和其他 AWS 服务的一项功能。

配置 Auto Scaling 时，您可以指定希望 AWS 为您维护的最小和最大实例数。然后，AWS 将根据需要添加或删除实例，以确保您不超出这些限制。您还可以指定扩展策略，以确定 AWS 应该如何扩展或缩减您的资源。例如，您可以指定希望 AWS 在您的 CPU 使用率超过 80% 时添加更多实例。

但是，了解自动缩放的工作原理并正确配置它很重要，因为如果使用不当，它可能会产生意想不到的后果。

例如，如果您指定了一个扩展策略，要求在 CPU 使用率超过 80% 时添加更多实例，但您没有办法限制可以添加的实例数量，那么 AWS 将继续添加实例，直到它达到您指定的最大实例数。这可能会导致意外高额的 AWS 账单。

为避免这种情况，您可以使用“缩放计划”。扩展计划是一组设置，用于确定 ASG 应如何扩大或缩小队列。

扩展计划包含许多可配置的设置，包括最小和最大实例数、所需容量和扩展策略。

您可以使用扩展计划通过指定在给定时间段内可以添加的最大实例数来限制可以添加的实例数。例如，您可以指定在 24 小时内最多可以添加 10 个实例。

您还可以使用扩展计划通过指定必须维护的最小实例数来限制可以删除的实例数。例如，您可以指定必须始终维护至少 2 个实例。

## 结论

AWS Auto Scaling 是一种经济高效的方式，可确保您的 AWS 资源在您需要时可用，并且您不会为闲置的资源付费。通过确保应用程序拥有处理流量高峰所需的资源，这也是提高应用程序性能的好方法。

Auto Scaling 是 Amazon EC2、Amazon ECS、Amazon RDS 和其他 AWS 服务的一项功能。

配置 Auto Scaling 时，您可以指定希望 AWS 为您维护的最小和最大实例数。然后，AWS 将根据需要添加或删除实例，以确保您不超出这些限制。您还可以指定扩展策略，以确定 AWS 应该如何扩展或缩减您的资源。

但是，了解自动缩放的工作原理并正确配置它很重要，因为如果使用不当，它可能会产生意想不到的后果。

有关 AWS 自动扩展的更多信息，请参阅以下资源：

- [AWS Auto Scaling 文档](https://docs.aws.amazon.com/autoscaling/latest/userguide/WhatIsAutoScaling.html)
- [自动缩放组](https://docs.aws.amazon.com/autoscaling/latest/userguide/AutoScalingGroups.html)
- [扩展计划](https://docs.aws.amazon.com/autoscaling/latest/userguide/ScalingPlans.html)