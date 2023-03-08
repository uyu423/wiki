---
title: Cloud Foundry 上的 Spring Boot 部署
description: 
published: true
date: 2023-02-02T14:57:41.468Z
tags: 
editor: markdown
dateCreated: 2023-02-02T14:57:39.806Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot Deployment on Cloud Foundry***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-deployment-on-cloud-foundry)
{.links-list}


# Cloud Foundry 上的 Spring Boot 部署

希望在 Cloud Foundry 上部署基于 Spring Boot 的应用程序的开发人员有几种不同的选择。在本文中，我们将了解其中的几个选项，并讨论每个选项的优缺点。

## 打包成罐子

打包 Spring Boot 应用程序的一种选择是将其打包为 jar 文件。这是 Spring Boot 文档中推荐的方法。

要将 Spring Boot 应用程序打包为 jar，您需要使用 spring-boot-maven-plugin 插件。该插件会将您的应用程序打包为可执行的 jar 文件。然后，您可以使用“cf push”命令将此 jar 文件部署到 Cloud Foundry。

将应用程序打包为 jar 的一个优点是您可以使用 `java -jar` 命令轻松地在本地运行它。这有助于调试目的。

打包为 jar 的另一个优点是您可以在 `manifest.yml` 文件中指定您的应用程序需要的任何环境变量。如果您想避免在代码中硬编码任何特定于环境的值，这会很有帮助。

## 打包成一场战争

打包 Spring Boot 应用程序的另一种选择是将其打包为 war 文件。这不是 Spring Boot 文档中推荐的方法，但它是一个选项。

要将 Spring Boot 应用程序打包为 war，您需要使用 spring-boot-starter-web 依赖项。此依赖项将包括将应用程序打包为战争所需的所有库。

然后，您可以使用“cf push”命令将此 war 文件部署到 Cloud Foundry。打包为战争的一个优点是您可以在 `manifest.yml` 文件中指定您的应用程序需要的任何环境变量。如果您想避免在代码中硬编码任何特定于环境的值，这会很有帮助。

## 使用 Cloud Foundry Java 构建包

Cloud Foundry 提供了一个 Java 构建包，可用于部署 Spring Boot 应用程序。此 buildpack 将检测到您的应用程序是 Spring Boot 应用程序，并将对其进行相应配置。

要使用 Cloud Foundry Java buildpack，您需要在 manifest.yml 文件中将 java_buildpack 指定为应用程序的 buildpack。然后，您可以使用 `cf push` 命令部署您的应用程序。

使用 Cloud Foundry Java buildpack 的优势之一是您无需将应用程序打包到 jar 或 war 文件中。 buildpack 会为你做到这一点。

使用 Cloud Foundry Java buildpack 的另一个优势是您可以在“manifest.yml”文件中指定应用程序所需的任何环境变量。如果您想避免在代码中硬编码任何特定于环境的值，这会很有帮助。

## 使用 Spring Cloud 连接器

Spring Cloud 连接器提供了一个抽象层，允许您将任何 Cloud Foundry 服务与 Spring 应用程序一起使用。如果您想使用 Cloud Foundry Java 构建包当前不支持的服务，这会很有帮助。

要使用 Spring Cloud 连接器，您需要将 `spring-cloud-spring-service-connector` 依赖项添加到您的项目中。然后，您可以使用 `cf push` 命令部署您的应用程序。

使用 Spring Cloud 连接器的一个优点是您不需要将应用程序打包到 jar 或 war 文件中。 buildpack 会为你做到这一点。

使用 Spring Cloud 连接器的另一个优点是您可以在 `manifest.yml` 文件中指定应用程序所需的任何环境变量。如果您想避免在代码中硬编码任何特定于环境的值，这会很有帮助。

## 结论

在 Cloud Foundry 上部署 Spring Boot 应用程序有几个不同的选项。每个选项都有自己的优点和缺点。您可以自行决定哪个选项最适合您的应用。