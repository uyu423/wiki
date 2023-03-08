---
title: 用于项目创建的 Spring Boot 初始化程序
description: 
published: true
date: 2023-02-07T21:32:33.444Z
tags: 
editor: markdown
dateCreated: 2023-02-07T21:32:31.785Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot Initializer for Project Creation***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-initializer-for-project-creation)
{.links-list}


# 用于项目创建的 Spring Boot 初始化程序

开发新项目可能非常耗时，尤其是从头开始时。 Spring Boot 可以更轻松地创建独立的、生产级的基于 Spring 的应用程序，您可以“直接运行”。它提供了一个灵活的构建系统和可以轻松配置的应用程序服务器。

在本文中，我们将向您展示如何使用 Spring Boot Initializr 来创建一个新的 Spring Boot 项目。 Spring Boot Initializr 是一个可以生成 Spring Boot 项目的 Web 应用程序。它提供选项来选择项目所需的依赖项。

## 什么是 Spring Boot Initializr？

Spring Boot Initializr 是一个可以生成 Spring Boot 项目的 Web 应用程序。它提供选项来选择项目所需的依赖项。

生成的项目包括选定的依赖项，可以使用 Gradle 或 Maven 构建工具构建。它还包括应用程序服务器（如果有）和构建工具的必要配置文件。

## 如何使用Spring Boot Initializr？

要使用 Spring Boot Initializr，您需要访问 Initializr Web 应用程序。您可以通过访问 Spring Boot Initializr 网站来执行此操作：https://start.spring.io/

![Spring Boot Initializr](https://i.imgur.com/HLgHZzg.png)

在 Initializr 网站上，您可以选择项目所需的依赖项。比如需要使用JPA访问数据库，可以选择“JPA”依赖。

![Spring Boot Initializr 依赖项](https://i.imgur.com/pz4UHfz.png)

选择好依赖后，就可以生成工程了。该项目将生成为 ZIP 文件。

## 如何创建Spring Boot 项目？

现在我们已经了解了如何使用 Spring Boot Initializr，让我们创建一个 Spring Boot 项目。

我们将使用 Initializr 网站生成具有以下依赖项的 Spring Boot 项目：

- 网络
- JPA
- MySQL

![Spring Boot Initializr 依赖项](https://i.imgur.com/pz4UHfz.png)

选择好依赖后，我们就可以生成工程了。该项目将生成为 ZIP 文件。

## 如何将项目导入Eclipse？

现在我们已经生成了项目，让我们将它导入到 Eclipse 中。

在 Eclipse 中，选择文件 -> 导入 -> 现有 Maven 项目。

![将 Maven 项目导入 Eclipse](https://i.imgur.com/Vywzo8I.png)

在“Import Maven Project”对话框中，选择我们刚刚生成的“spring-boot-mysql-example”项目。

![导入 Maven 项目](https://i.imgur.com/pz4UHfz.png)

单击“完成”导入项目。

该项目将导入到 Eclipse 中。

## 如何运行项目？

现在我们已经导入了项目，让我们运行它。

右键单击该项目并选择“运行方式 -> Java 应用程序”。

![运行 Java 应用程序](https://i.imgur.com/7lFWoqo.png)

在“Java 应用程序”对话框中，选择“应用程序”类并单击“确定”。

![Java 应用程序](https://i.imgur.com/pz4UHfz.png)

该项目将在嵌入式 Tomcat 服务器上运行。

您可以在 http://localhost:8080/ 访问该应用程序。

## 结论

在本文中，我们向您展示了如何使用 Spring Boot Initializr 创建一个新的 Spring Boot 项目。 Spring Boot Initializr 是一个可以生成 Spring Boot 项目的 Web 应用程序。它提供选项来选择项目所需的依赖项。