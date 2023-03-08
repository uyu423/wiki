---
title: 弹簧引导日志记录
description: 
published: true
date: 2023-02-01T02:17:22.373Z
tags: 
editor: markdown
dateCreated: 2023-02-01T02:17:20.844Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Spring Boot Logging***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-logging)
{.links-list}



# Spring Boot 日志记录

Spring Boot 使您可以轻松地为您的应用程序配置日志记录。默认情况下，Spring Boot 会将应用程序配置为使用 `java.util.logging` (JUL) 日志框架。这可以通过向项目添加适当的启动器依赖项来更改为使用 Log4j2、Logback 或 slf4j。

在本文中，我们将了解如何在 Spring Boot 中配置日志记录。我们将从一个基本示例开始，然后转向更高级的主题。

## 基本配置

在 Spring Boot 中配置日志记录的最简单方法是将 logging.level 属性添加到 application.properties 文件。可以为特定包或特定记录器设置日志记录级别。例如，以下配置会将 com.example 包的日志记录级别设置为 DEBUG：

```
logging.level.com.example=DEBUG
```

如果你想为所有包设置日志记录级别，你可以使用 `root` 记录器。例如，以下配置会将所有包的日志记录级别设置为“INFO”：

```
logging.level.root=INFO
```

## 记录器

除了设置日志级别，你还可以配置日志输出的格式。默认情况下，Spring Boot 将以 %d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n 格式输出日志消息。

您可以通过设置 logging.pattern.console 属性来更改格式。例如，以下配置将以 %d [%thread] %-5level %logger{36} - %msg%n 格式输出日志消息：

```
logging.pattern.console=%d [%thread] %-5level %logger{36} - %msg%n
```

## 附加程序

除了控制台之外，Spring Boot 还可以将日志记录到文件中。默认情况下，日志消息将输出到 `tmp` 目录中的 `spring.log` 文件。您可以通过设置 logging.file 属性来更改文件的位置。例如，以下配置会将日志消息输出到文件“/var/log/spring.log”：

```
logging.file=/var/log/spring.log
```

## 自定义记录器

如果要创建自定义记录器，可以使用 logging.config 属性指定 log4j2.xml 文件的位置。例如，以下配置会将日志消息输出到文件“/var/log/spring.log”：

```
logging.config=log4j2.xml
```

## 高级配置

除了基本配置外，Spring Boot 还提供了一些高级功能。例如，您可以将记录器配置为将日志消息输出到多个文件。您还可以为特定类设置日志级别。

## 记录到多个文件

您可以通过设置 logging.file.name 和 logging.file.max-size 属性将记录器配置为将日志消息输出到多个文件。例如，以下配置会将日志消息输出到 `tmp` 目录中的文件 `spring.log` 和 `spring.log.1`：

```
logging.file.name=spring.log
logging.file.max-size=10MB
```

## 类的日志级别

您可以通过设置 logging.level.{class} 属性来设置特定类的日志记录级别。例如，以下配置会将 com.example.MyClass 类的日志记录级别设置为 DEBUG：

```
logging.level.com.example.MyClass=DEBUG
```

## 结论

在本文中，我们了解了如何在 Spring Boot 中配置日志记录。我们已经了解了如何设置日志记录级别以及如何更改日志输出的格式。我们还了解了如何将日志消息输出到多个文件以及如何为特定类设置日志记录级别。