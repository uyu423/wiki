---
title: AWS 上的 Spring Boot 部署
description: 
published: true
date: 2023-02-07T13:32:41.229Z
tags: 
editor: markdown
dateCreated: 2023-02-07T13:32:39.550Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot Deployment on AWS***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-deployment-on-aws)
{.links-list}



# AWS 上的 Spring Boot 部署

希望在 AWS 上部署 Spring Boot 应用程序的开发人员可以使用不同的选项，具体取决于他们的用例。在本文中，我们将探索其中的一些选项，并提供有关何时使用每个选项的提示。

## 弹性豆茎

AWS Elastic Beanstalk 对于需要托管服务来部署和扩展其 Spring Boot 应用程序的开发人员来说是一个不错的选择。 Elastic Beanstalk 处理应用程序的容量配置、负载平衡和自动缩放。它还与其他 AWS 服务集成，例如 Amazon Relational Database Service (RDS) 和 Amazon Simple Notification Service (SNS)。

要使用 Elastic Beanstalk，开发人员只需将他们的 Spring Boot 应用程序上传为 ZIP 或 WAR 文件。 Elastic Beanstalk 随后会自动为应用程序创建环境并将应用程序部署到该环境。

对于需要托管服务来部署和扩展 Spring Boot 应用程序的开发人员来说，Elastic Beanstalk 是一个不错的选择。

## 亚马逊弹性容器服务 (ECS)

对于想要容器化 Spring Boot 应用程序的开发人员来说，Amazon ECS 是一个不错的选择。 ECS 是一种托管容器服务，可让您在 AWS 上轻松运行和扩展容器化应用程序。

要使用 Amazon ECS，开发人员首先需要使用 Docker 将其 Spring Boot 应用程序容器化。然后他们可以创建 ECS 任务定义，这是运行容器化应用程序的蓝图。创建任务定义后，开发人员便可以在 ECS 集群上运行任务。然后，Amazon ECS 将在集群上启动任务并将其提供给用户。

对于想要容器化 Spring Boot 应用程序的开发人员来说，Amazon ECS 是一个不错的选择。

## 亚马逊弹性容器注册表 (ECR)

对于想要为其 Spring Boot 应用程序存储和管理 Docker 映像的开发人员而言，Amazon ECR 是一个不错的选择。 ECR 是一种托管的 Docker 容器注册表服务，可让您轻松地在 AWS 上存储、管理和部署 Docker 映像。

要使用 Amazon ECR，开发人员首先需要为其 Spring Boot 应用程序创建一个存储库。然后他们可以将他们的 Docker 镜像推送到存储库。一旦映像被推送，开发人员就可以在 Amazon ECS 或 Amazon Elastic Container Service for Kubernetes (EKS) 上部署他们的应用程序。

对于想要为其 Spring Boot 应用程序存储和管理 Docker 映像的开发人员而言，Amazon ECR 是一个不错的选择。

## 亚马逊简单存储服务 (S3)

对于希望将 Spring Boot 应用程序存储为 ZIP 或 WAR 文件的开发人员来说，Amazon S3 是一个不错的选择。 S3 是一种托管存储服务，可以轻松地在 AWS 上存储和检索文件。

要使用 Amazon S3，开发人员只需将他们的 Spring Boot 应用程序上传为 ZIP 或 WAR 文件。然后他们可以创建一个 Amazon S3 存储桶，这是一个用于在 S3 上存储文件的容器。创建存储桶后，开发人员便可以在 Amazon Elastic Beanstalk 或 Amazon ECS 上部署他们的应用程序。

对于希望将 Spring Boot 应用程序存储为 ZIP 或 WAR 文件的开发人员来说，Amazon S3 是一个不错的选择。

## 亚马逊关系数据库服务 (RDS)

对于想要为其 Spring Boot 应用程序使用关系数据库的开发人员来说，Amazon RDS 是一个不错的选择。 RDS 是一种托管数据库服务，可以轻松地在 AWS 上设置、操作和扩展关系数据库。

要使用 Amazon RDS，开发人员首先需要创建一个 Amazon RDS 实例。然后他们可以为他们的 Spring Boot 应用程序创建一个数据库。创建数据库后，开发人员便可以在 Amazon Elastic Beanstalk 或 Amazon ECS 上部署他们的应用程序。

对于想要为其 Spring Boot 应用程序使用关系数据库的开发人员来说，Amazon RDS 是一个不错的选择。

## 亚马逊简单通知服务 (SNS)

对于想要从 Spring Boot 应用程序发送通知的开发人员来说，Amazon SNS 是一个不错的选择。 SNS 是一种托管通知服务，可以轻松地通过电子邮件、短信或推送通知向用户发送通知。

要使用 Amazon SNS，开发人员首先需要创建一个 Amazon SNS 主题。然后他们可以为用户订阅该主题。用户订阅后，开发人员便可以向该主题发布消息。然后消息将被传递给订阅者。

对于想要从 Spring Boot 应用程序发送通知的开发人员来说，Amazon SNS 是一个不错的选择。