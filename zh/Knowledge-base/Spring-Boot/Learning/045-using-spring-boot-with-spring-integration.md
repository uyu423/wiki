---
title: 045：将 Spring Boot 与 Spring Integration 结合使用
description: 
published: true
date: 2023-02-04T11:32:17.052Z
tags: 
editor: markdown
dateCreated: 2023-02-04T11:32:15.441Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [045: Using Spring Boot with Spring Integration***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/045-using-spring-boot-with-spring-integration)
{.links-list}


# 将 Spring Boot 与 Spring Integration 结合使用

在本文中，我们将了解如何将 Spring Boot 与 Spring Integration 结合使用。我们将回顾 Spring Integration 的基础知识，并展示如何将其与 Spring Boot 结合使用。

## 什么是 Spring 集成？

Spring Integration 是一个扩展 Spring Framework 以提供对企业集成模式的支持的框架。这些模式用于促进不同应用程序和系统之间的通信。

Spring Integration 为各种不同的技术提供适配器，例如 JMS、HTTP 和 FTP。它还提供对消息通道、消息路由器和消息转换器的支持。

## 为什么要使用 Spring Integration？

Spring Integration 使您能够构建具有弹性和可扩展性的企业级应用程序。它通过提供跨不同技术的一致编程模型来帮助您避免供应商锁定。

## 入门

在本节中，我们将向您展示如何开始使用 Spring Integration。我们将介绍您需要的不同依赖项，并向您展示如何配置 Spring Integration。

### 依赖项

首先，您需要将以下依赖项添加到您的项目中：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-integration</artifactId>
    </dependency>
</dependencies>
```

这些依赖项将为 Spring Integration 引入必要的 jar。

### 配置

接下来，您需要配置 Spring Integration。您可以通过将以下内容添加到您的“application.properties”文件来执行此操作：

```properties
spring.integration.dsl.enabled=true
```

这将启用 Spring Integration Java DSL。

## 结论

在本文中，我们了解了如何将 Spring Boot 与 Spring Integration 结合使用。我们已经了解了 Spring Integration 的基础知识，并展示了如何开始使用它。