---
title: AWS Fargate: Running Containers without Managing Infrastructure
description: 
published: true
date: 2023-02-19T04:32:24.695Z
tags: 
editor: markdown
dateCreated: 2023-02-19T04:32:17.703Z
---

- [AWS Fargate: 인프라 관리 없이 컨테이너 실행***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-fargate-running-containers-without-managing-infrastructure)
{.links-list}


# AWS Fargate: Running Containers without Managing Infrastructure

AWS Fargate is a serverless compute engine for containers that works with both Amazon Elastic Container Service (ECS) and Amazon Elastic Container Service for Kubernetes (EKS). Fargate makes it easy to run and manage containerized applications without having to worry about server infrastructure.

With Fargate, you no longer need to provision or manage servers, install and maintain operating systems, or patch and update software. Fargate removes the need to choose server types and sizes, decide when to scale your clusters, or optimize cluster utilization. This means you can focus on building and running your applications, and let AWS worry about the infrastructure.

Fargate is available now in all commercial AWS Regions.


## How Does Fargate Work?

Fargate runs containers on a purpose-built Elastic Network Interface (ENI) that is optimized for performance and security. Your containers run in isolated security groups and can communicate with each other using the ENI.

Fargate provides two launch types:

-   Fargate launch type – This launch type allows you to run containers without having to manage servers or clusters. You only need to specify the amount of CPU and memory resources required for your task.
-   EC2 launch type – This launch type allows you to launch containers on Amazon EC2 instances. You can launch Fargate tasks on existing Amazon EC2 instances that are part of an ECS or EKS cluster.

## What Are the Benefits of Using Fargate?

Fargate offers several benefits, including the following:

-   No need to manage servers or clusters – With Fargate, you no longer need to provision or manage servers. This means you can focus on building and running your applications, and let AWS worry about the infrastructure.
-   Easy to use – Fargate is easy to use. You simply specify the amount of CPU and memory resources required for your task, and Fargate will provision the underlying infrastructure and run your task.
-   Flexible – Fargate provides two launch types: Fargate and EC2. The Fargate launch type allows you to run containers without having to manage servers or clusters. The EC2 launch type allows you to launch Fargate tasks on existing Amazon EC2 instances that are part of an ECS or EKS cluster.
-   Secure – Fargate runs containers in isolated security groups and can communicate with each other using the ENI.
-   Scalable – Fargate makes it easy to scale your applications. You simply specify the desired number of tasks, and Fargate will scale your application up or down as needed.
-   Available in all commercial AWS Regions – Fargate is available in all commercial AWS Regions.