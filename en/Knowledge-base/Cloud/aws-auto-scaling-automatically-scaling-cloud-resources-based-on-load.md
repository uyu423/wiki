---
title: AWS Auto Scaling: Automatically Scaling Cloud Resources Based on Load
description: 
published: true
date: 2023-01-31T20:23:54.089Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:23:50.278Z
---

- [AWS Auto Scaling: 로드에 따라 자동으로 클라우드 리소스 확장***Korean** version of this document is available*](/ko/Knowledge-base/Cloud/aws-auto-scaling-automatically-scaling-cloud-resources-based-on-load)
{.links-list}
- [AWS Auto Scaling: 負荷に基づいてクラウド リソースを自動的にスケーリングする***Japanese** version of this document is available*](/ja/Knowledge-base/Cloud/aws-auto-scaling-automatically-scaling-cloud-resources-based-on-load)
{.links-list}
- [AWS Auto Scaling：根据负载自动扩展云资源***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Cloud/aws-auto-scaling-automatically-scaling-cloud-resources-based-on-load)
{.links-list}


# AWS Auto Scaling: Automatically Scaling Cloud Resources Based on Load

Auto scaling is a cloud computing feature that enables organizations to scale their Amazon Web Services (AWS) resources up or down automatically according to demand, thereby saving money and ensuring that resources are available when needed.

AWS auto scaling is a cost-effective way to ensure that your AWS resources are available when you need them and that you are not paying for resources that are idle. It is also a good way to improve the performance of your applications by ensuring that they have the resources they need to handle spikes in traffic.

Auto scaling is a feature of Amazon Elastic Compute Cloud (EC2), Amazon Elastic Container Service (ECS), Amazon Relational Database Service (RDS), and other AWS services.

When configuring auto scaling, you specify the minimum and maximum number of instances that you want AWS to maintain for you. AWS will then add or remove instances as needed to keep you within these limits. You can also specify scaling policies that determine how AWS should scale your resources up or down. For example, you can specify that you want AWS to add more instances when your CPU utilization is above 80%.

AWS auto scaling is a good way to save money on your AWS bill and to improve the performance of your applications. It is important to understand how auto scaling works and to configure it properly, however, as it can have unintended consequences if not used correctly.

## How AWS Auto Scaling Works

AWS auto scaling works by maintaining a group of EC2 instances that are known as a "fleet." This fleet is managed by an "auto scaling group" (ASG), which is a collection of settings that determine how the fleet should be scaled up or down.

The ASG contains a number of configurable settings, including the minimum and maximum number of instances, the desired capacity, and the scaling policies.

When you create an ASG, you must specify the minimum and maximum number of instances that you want it to maintain. The ASG will then scale the fleet up or down as needed to keep you within these limits.

You can also specify the desired capacity, which is the number of instances that you want the ASG to maintain at any given time. The ASG will scale the fleet up or down as needed to reach this desired capacity.

The ASG also contains a number of scaling policies. These policies determine how the ASG should scale the fleet up or down in response to changes in demand.

For example, you can specify a scaling policy that says to add more instances when the CPU utilization is above 80%. This policy would cause the ASG to add more instances to the fleet when the CPU utilization is above 80%.

You can also specify scaling policies that determine how the ASG should scale the fleet in response to changes in the number of requests per second (RPS) or the number of bytes per second (BPS).

Auto scaling is a good way to save money on your AWS bill and to improve the performance of your applications. It is important to understand how auto scaling works and to configure it properly, however, as it can have unintended consequences if not used correctly.

## Configuring AWS Auto Scaling

AWS auto scaling is a feature of Amazon EC2, Amazon ECS, Amazon RDS, and other AWS services.

When configuring auto scaling, you specify the minimum and maximum number of instances that you want AWS to maintain for you. AWS will then add or remove instances as needed to keep you within these limits. You can also specify scaling policies that determine how AWS should scale your resources up or down. For example, you can specify that you want AWS to add more instances when your CPU utilization is above 80%.

It is important to understand how auto scaling works and to configure it properly, however, as it can have unintended consequences if not used correctly.

For example, if you specify a scaling policy that says to add more instances when the CPU utilization is above 80%, but you do not have a way to limit the number of instances that can be added, then AWS will keep adding instances until it reaches the maximum number of instances that you have specified. This could result in an unexpectedly high AWS bill.

To avoid this, you can use a "scaling plan." A scaling plan is a collection of settings that determine how the ASG should scale the fleet up or down.

The scaling plan contains a number of configurable settings, including the minimum and maximum number of instances, the desired capacity, and the scaling policies.

You can use a scaling plan to limit the number of instances that can be added by specifying a maximum number of instances that can be added in a given time period. For example, you could specify that no more than 10 instances can be added in a 24-hour period.

You can also use a scaling plan to limit the number of instances that can be removed by specifying a minimum number of instances that must be maintained. For example, you could specify that at least 2 instances must be maintained at all times.

## Conclusion

AWS auto scaling is a cost-effective way to ensure that your AWS resources are available when you need them and that you are not paying for resources that are idle. It is also a good way to improve the performance of your applications by ensuring that they have the resources they need to handle spikes in traffic.

Auto scaling is a feature of Amazon EC2, Amazon ECS, Amazon RDS, and other AWS services.

When configuring auto scaling, you specify the minimum and maximum number of instances that you want AWS to maintain for you. AWS will then add or remove instances as needed to keep you within these limits. You can also specify scaling policies that determine how AWS should scale your resources up or down.

It is important to understand how auto scaling works and to configure it properly, however, as it can have unintended consequences if not used correctly.

For more information on AWS auto scaling, see the following resources:

- [AWS Auto Scaling Documentation](https://docs.aws.amazon.com/autoscaling/latest/userguide/WhatIsAutoScaling.html)
- [Auto Scaling Groups](https://docs.aws.amazon.com/autoscaling/latest/userguide/AutoScalingGroups.html)
- [Scaling Plans](https://docs.aws.amazon.com/autoscaling/latest/userguide/ScalingPlans.html)