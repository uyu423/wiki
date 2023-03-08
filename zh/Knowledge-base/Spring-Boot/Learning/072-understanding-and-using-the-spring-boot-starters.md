---
title: 072：了解和使用 Spring Boot Starters
description: 
published: true
date: 2023-02-05T05:32:15.436Z
tags: 
editor: markdown
dateCreated: 2023-02-05T05:32:13.922Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [072: Understanding and Using the Spring Boot Starters***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/072-understanding-and-using-the-spring-boot-starters)
{.links-list}


# 072：了解和使用 Spring Boot Starters

Spring Boot Starters 是一组方便的依赖描述符，可以包含在您的应用程序中。通过在您的项目中包含其中一个，您将获得一组配置良好、随时可用的依赖项，您可以使用它们快速轻松地启动和运行您的项目。

在本文中，我们将了解 Spring Boot Starters 是什么、它们如何工作以及如何在您自己的项目中使用它们。

## 什么是 Spring Boot 启动器？

Spring Boot Starters 是一组依赖描述符，可以包含在您的项目中。这些描述符定义了一组配置良好、随时可用的依赖项，可用于快速轻松地启动和运行您的项目。

Spring Boot Starters 分为两组：Core Starters 和 Web Starters。 Core Starters 是任何 Spring Boot 应用程序所需的依赖项。 Web Starters 是任何将公开 Web 界面的 Spring Boot 应用程序所需的依赖项。

## Spring Boot Starters 是如何工作的？

Spring Boot Starters 通过提供一组配置良好、随时可用的依赖项来工作。这些依赖项可用于快速轻松地启动和运行您的项目。

在项目中包含 Spring Boot Starter 将自动包含该 Starter 所需的任何依赖项。例如，在您的项目中包含`spring-boot-starter-web` Starter 将自动包含`spring-boot-starter-tomcat` Starter，因为`spring-boot-starter-web` Starter 依赖于`spring -boot-starter-tomcat` 启动器。

## 如何在自己的项目中使用 Spring Boot Starters？

在您自己的项目中包含一个 Spring Boot Starter 很容易。只需将适当的依赖项添加到项目的“pom.xml”文件中即可。

例如，要在您的项目中包含 `spring-boot-starter-web` Starter，您需要将以下依赖项添加到您的 `pom.xml` 文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

## 结论

在本文中，我们了解了 Spring Boot Starters 是什么、它们如何工作以及如何在您自己的项目中使用它们。