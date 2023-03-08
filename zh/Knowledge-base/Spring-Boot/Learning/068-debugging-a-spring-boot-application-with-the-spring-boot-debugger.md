---
title: 068：使用 Spring Boot 调试器调试 Spring Boot 应用程序
description: 
published: true
date: 2023-02-05T02:17:26.809Z
tags: 
editor: markdown
dateCreated: 2023-02-05T02:17:25.183Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [068: Debugging a Spring Boot Application with the Spring Boot Debugger***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/068-debugging-a-spring-boot-application-with-the-spring-boot-debugger)
{.links-list}


# 068：使用 Spring Boot 调试器调试 Spring Boot 应用程序

开发人员在尝试调试 Spring Boot 应用程序时面临许多挑战。 Spring Boot Debugger 是一个强大的工具，可以帮助开发人员克服这些挑战并快速找到问题的根本原因。

在本文中，我们将了解如何使用 Spring Boot Debugger 调试 Spring Boot 应用程序。我们还将了解可用于解决常见 Spring Boot 问题的调试器的一些功能。

## 设置 Spring Boot 调试器

使用 Spring Boot Debugger 的第一步是确保其配置正确。在大多数情况下，调试器将在应用程序以调试模式启动时自动配置。但是，在某些情况下可能需要手动配置调试器。

配置调试器的最简单方法是为您的 IDE 使用 Spring Boot Debugger 插件。该插件会自动将必要的配置添加到您的应用程序中。

或者，您可以将以下配置添加到您的 application.properties 文件中：

```
spring.jpa.show-sql=true
spring.h2.console.enabled=true
```

## 使用 Spring Boot 调试器

一旦正确配置了调试器，您就可以开始使用它来调试您的应用程序。调试器可用于调试 Web 应用程序和非 Web 应用程序。

要调试 Web 应用程序，您可以使用以下步骤：

1. 以调试模式启动您的应用程序。
2. 使用调试器客户端连接到应用程序。
3. 在代码中设置断点。
4. 检查变量并分析调用堆栈。

要调试非 Web 应用程序，您可以使用以下步骤：

1. 以调试模式启动您的应用程序。
2. 使用调试器客户端连接到应用程序。
3. 在代码中设置断点。
4. 检查变量并分析调用堆栈。
5.附加到正在运行的应用程序。

## Spring Boot 调试器的特性

Spring Boot Debugger 具有许多可用于解决常见 Spring Boot 问题的功能。

### 热插拔

热交换是调试器的一项功能，它允许开发人员更改他们的代码并使这些更改立即生效。这对于修复实时应用程序中的错误特别有用。

要使用热交换，只需对您的代码进行所需的更改并保存文件。更改将立即生效。

### 断点

断点是调试器的另一个有用的特性。断点可用于在特定行暂停代码的执行。这使您可以检查变量和调用堆栈以查看代码中发生的情况。

通过单击 IDE 中的行号，可以在代码中添加断点。或者，您可以使用以下命令添加断点：

```
debug: breakpoint MyClass.java:12
```

### 检查变量

当您的代码在断点处暂停时，您可以检查变量的值。这可以在您的 IDE 中完成，也可以使用以下命令完成：

```
debug: inspect myVariable
```

### 分析调用堆栈

调用堆栈可用于查看导致代码当前状态的方法调用序列。这有助于理解您的代码为何未按预期运行。

可以在您的 IDE 中或使用以下命令查看调用堆栈：

```
debug: trace
```

## 结论

在本文中，我们了解了如何使用 Spring Boot Debugger 来调试 Spring Boot 应用程序。我们还了解了可用于解决常见 Spring Boot 问题的调试器的一些功能。