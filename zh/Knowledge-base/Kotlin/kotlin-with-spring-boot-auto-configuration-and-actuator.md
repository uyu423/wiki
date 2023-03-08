---
title: Kotlin with Spring Boot：自动配置和执行器
description: 
published: true
date: 2023-02-02T18:23:16.581Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:23:15.019Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kotlin with Spring Boot: Auto-configuration and Actuator***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-with-spring-boot-auto-configuration-and-actuator)
{.links-list}


# Kotlin with Spring Boot：自动配置和执行器

Kotlin 是一种运行在 JVM 上的静态类型编程语言，可用于开发 Android 应用程序。 Spring Boot 是一个框架，可以轻松创建独立的、生产级的基于 Spring 的应用程序，您可以“直接运行”。

Kotlin with Spring Boot 项目为 Kotlin 和 Spring Boot 应用程序提供自动配置和执行器支持。

## 自动配置

自动配置是 Spring Boot 的一项功能，它会根据类路径上的依赖项自动配置 Spring 应用程序。例如，如果您在类路径中包含 spring-boot-starter-data-jpa 依赖项，Spring Boot 将自动为您配置 DataSource 和 JPA EntityManagerFactory。

Kotlin with Spring Boot 项目为 Kotlin 和 Spring Boot 应用程序提供自动配置。这意味着，例如，如果您在类路径中包含 spring-boot-starter-data-jpa 依赖项，带有 Spring Boot 的 Kotlin 将自动为您配置 DataSource 和 JPA EntityManagerFactory。

要将 Kotlin 与 Spring Boot 自动配置一起使用，您需要将 kotlin-spring-boot-autoconfigure 模块添加到类路径中。

## 执行器

Actuator 是 Spring Boot 的一项功能，可让您监控和管理您的应用程序。例如，Actuator 提供了一个 HTTP 端点，您可以使用它来监控应用程序的运行状况。

Kotlin with Spring Boot 项目为 Kotlin 和 Spring Boot 应用程序提供执行器支持。这意味着，例如，您可以使用 Actuator 来监控 Kotlin 和 Spring Boot 应用程序的运行状况。

要将 Kotlin 与 Spring Boot Actuator 一起使用，您需要将 kotlin-spring-boot-actuator 模块添加到类路径中。

## 入门

要开始使用 Kotlin 和 Spring Boot，您可以使用 Spring Initializr 生成具有所需依赖项的项目。例如，要生成具有 kotlin-spring-boot-autoconfigure 和 kotlin-spring-boot-actuator 依赖项的项目，您可以执行以下操作：

1. 前往 https://start.spring.io/。
2. 从语言下拉列表中选择 Kotlin。
3. 从引导版本下拉列表中选择 Spring Boot 2.0.0。
4. 在工件字段中输入 kotlin-spring-boot-example。
5. 选择 kotlin-spring-boot-autoconfigure 和 kotlin-spring-boot-actuator 依赖项。
6. 单击生成项目。

然后您可以将生成的项目导入您最喜欢的 IDE 并开始编码！

## 结论

在本文中，我们研究了 Kotlin with Spring Boot 项目，它为 Kotlin 和 Spring Boot 应用程序提供自动配置和执行器支持。我们还了解了如何开始使用 Kotlin 和 Spring Boot，使用 Spring Initializr 生成具有必要依赖项的项目。