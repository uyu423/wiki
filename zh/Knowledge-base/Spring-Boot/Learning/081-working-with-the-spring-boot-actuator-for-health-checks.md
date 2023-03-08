---
title: 081：使用 Spring Boot Actuator 进行健康检查
description: 
published: true
date: 2023-02-05T12:32:18.494Z
tags: 
editor: markdown
dateCreated: 2023-02-05T12:32:16.946Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [081: Working with the Spring Boot Actuator for Health Checks***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/081-working-with-the-spring-boot-actuator-for-health-checks)
{.links-list}


# 什么是用于健康检查的 Spring Boot Actuator？

Spring Boot Actuator for Health Checks 是一种允许开发人员轻松检查其应用程序健康状况的工具。它可用于监控应用程序性能、识别潜在问题并提供有关应用程序整体健康状况的信息。

Spring Boot Actuator for Health Checks 是一个内置工具，包含在 Spring Boot 框架中。它易于使用，并提供有关应用程序健康状况的大量信息。

# 为什么使用 Spring Boot Actuator 进行健康检查？

用于健康检查的 Spring Boot Actuator 是开发人员的宝贵工具。它可以帮助识别应用程序的潜在问题并提供有关应用程序整体健康状况的信息。

用于健康检查的 Spring Boot Actuator 易于使用，并提供了丰富的信息。对于想要监控其应用程序健康状况的开发人员来说，这是一个有价值的工具。

# 如何使用 Spring Boot Actuator 进行健康检查

使用 Spring Boot Actuator 进行健康检查很容易。只需将以下依赖项添加到您的项目中：

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

添加依赖项后，您可以通过将以下内容添加到 application.properties 文件来访问 Actuator 端点：

```properties
management.endpoints.web.exposure.include=health
```

然后，您可以在 http://localhost:8080/actuator/health 访问健康端点。

# 结论

用于健康检查的 Spring Boot Actuator 是开发人员的宝贵工具。它易于使用，并提供有关应用程序健康状况的大量信息。对于想要监控其应用程序健康状况的开发人员来说，这是一个有价值的工具。