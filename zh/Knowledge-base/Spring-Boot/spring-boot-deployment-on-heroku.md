---
title: Heroku 上的 Spring Boot 部署
description: 
published: true
date: 2023-02-07T12:32:31.834Z
tags: 
editor: markdown
dateCreated: 2023-02-07T12:32:29.645Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot Deployment on Heroku***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-deployment-on-heroku)
{.links-list}


# Heroku 上的 Spring Boot 部署

Heroku 是一个支持多种编程语言的云平台即服务 (PaaS)。其中一种语言是 Java。在本文中，我们将讨论如何在 Heroku 上部署 Spring Boot 应用程序。

## 什么是 Spring Boot？

Spring Boot 是一个基于 Java 的框架，用于创建微服务。它由 Pivotal Team 开发，是一个免费的开源项目。

## 什么是 Heroku？

Heroku 是一个支持多种编程语言的云平台即服务 (PaaS)。

Heroku 是一个平台即服务 (PaaS)，允许开发人员部署、管理和扩展他们的应用程序。 Heroku 简单易用，并为小型应用程序提供免费计划。

## 先决条件

在开始之前，您需要具备以下条件：

- 一个 Heroku 帐户
- 文本编辑器
- JDK 8 或以上
- Maven 3.3.9 或以上版本

## 创建一个 Spring Boot 应用程序

首先，您需要创建一个 Spring Boot 应用程序。您可以使用 Spring Initializr 执行此操作。

Spring Initializr 是一个 Web 应用程序，允许您创建 Spring Boot 应用程序。它将为您生成项目结构并添加所需的依赖项。

要创建 Spring Boot 应用程序，请转到 https://start.spring.io/，然后选择以下内容：

- 语言：Java
- 春季启动版本：2.4.4
- 项目：Maven 项目
- 包装：罐
- Java 版本：8
- 组：com.heroku
- 神器：演示

单击“生成项目”以下载项目。

## 创建一个 Procfile

Procfile 是一个文本文件，其中包含应用程序在启动时执行的命令。 Procfile 必须放在应用程序的根目录中。

创建一个名为 Procfile 的文件（没有任何扩展名）并向其中添加以下行。

    网络：java -jar target/demo-0.0.1-SNAPSHOT.jar

## 创建一个 Heroku 应用程序

创建 Procfile 后，您可以创建 Heroku 应用程序。

登录到您的 Heroku 帐户并单击新建 -> 创建新应用。

输入以下信息：

- 应用程序名称：演示
- 地区：欧洲

单击创建应用程序。

## 将应用程序部署到 Heroku

创建应用程序后，您可以将 Spring Boot 应用程序部署到 Heroku。

Heroku 使用 Git 进行部署，因此您需要将代码推送到 Heroku Git 存储库。

首先，您需要将 Heroku Git 存储库作为远程存储库添加到您的本地存储库。为此，请运行以下命令：

    $ heroku git:remote -a 演示

然后，您可以使用以下命令将您的代码推送到 Heroku Git 存储库：

    $ git 推送 heroku 大师

推送代码后，Heroku 将构建和部署应用程序。

您可以使用以下命令查看日志：

    $ heroku 日志 --tail

## 结论

在本文中，我们讨论了如何在 Heroku 上部署 Spring Boot 应用程序。