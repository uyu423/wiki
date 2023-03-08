---
title: 部署 Spring Boot 应用程序：最佳实践
description: 
published: true
date: 2023-02-17T18:02:42.326Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:59:25.893Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Deploying Spring Boot Applications: Best Practices***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/deploying-spring-boot-applications-best-practices)
{.links-list}
 


# 部署 Spring Boot 应用程序：最佳实践

Spring Boot 是一种流行的 Java Web 框架，可以轻松创建生产级、独立的基于 Spring 的应用程序。在本文中，我们将讨论部署 Spring Boot 应用程序的一些最佳实践。

＃＃ 目录

1. [创建Spring Boot应用](#creating-a-spring-boot-application)
2. [部署一个Spring Boot应用](#deploying-a-spring-boot-application)
    1. [架构](#architecture)
    2. [网络服务器](#web-servers)
3. [结论](#conclusion)

## 创建一个 Spring Boot 应用程序

创建 Spring Boot 应用程序很简单。您只需要 Java 和一个文本编辑器。 Spring Boot 应用程序通常打包为 jar 文件，可以使用 java -jar 命令运行。例如，以下命令将启动一个在端口 8080 上运行的 Spring Boot 应用程序：

```java
java -jar my-spring-boot-app.jar
```

如果您使用 Maven，您还可以使用 `spring-boot:run` 目标：

```
mvn spring-boot:run
```

您还可以使用 Spring Initializr 创建 Spring Boot 应用程序。 Spring Initializr 是一个 Web 应用程序，可以根据您的选择生成 Spring Boot 应用程序。只需选择您想要的依赖项，Initializr 就会生成一个包含这些依赖项的项目。

## 部署 Spring Boot 应用程序

部署 Spring Boot 应用程序很容易。与传统的 Java Web 应用程序不同，无需配置 servlet 容器或应用程序服务器。但是，在部署 Spring Boot 应用程序时需要牢记一些事项。

＃＃＃ 建筑学

Spring Boot 应用程序通常部署为独立的 jar 文件。这使得在任何支持 Java 的平台上部署和运行 Spring Boot 应用程序变得容易。

Spring Boot 应用程序也可以部署为 war 文件。但是，这不是推荐的部署方法，因为它需要 servlet 容器或应用程序服务器来运行应用程序。

### 网络服务器

Spring Boot 应用程序可以部署到各种 Web 服务器。最受欢迎的选项是 Apache Tomcat 和 Jetty。

Tomcat 是 Java 应用程序使用最广泛的 Web 服务器。 Tomcat 是一个servlet 容器，可以运行War 文件。 Tomcat 既可以作为独立服务器使用，也可以作为可嵌入的 servlet 容器使用。

Jetty 是一种广泛使用的开源 Web 服务器。 Jetty 是一个servlet 容器，可以运行War 文件。 Jetty 可用作独立服务器和可嵌入的 servlet 容器。

＃＃ 结论

部署 Spring Boot 应用程序很容易。 Spring Boot 应用程序可以部署到各种 Web 服务器，并且不需要 servlet 容器或应用程序服务器。