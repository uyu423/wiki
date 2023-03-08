---
title: 使用远程调试进行 Spring Boot 调试
description: 
published: true
date: 2023-02-02T20:57:31.800Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:57:27.230Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot Debugging with Remote Debugging***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-debugging-with-remote-debugging)
{.links-list}


# 介绍

开发人员经常需要调试他们的代码以查找和修复错误。可以通过多种方式调试 Spring Boot 应用程序，包括使用远程调试器。在本文中，我们将探讨如何使用远程调试器调试 Spring Boot 应用程序。

# 什么是远程调试？

远程调试是允许开发人员调试在远程计算机上运行的程序的过程。为此，开发人员需要能够访问远程机器并能够使用调试器连接到它。

# 如何使用远程调试器调试 Spring Boot 应用程序

要使用远程调试器调试 Spring Boot 应用程序，需要遵循几个步骤。我们将详细介绍这些步骤中的每一个。

## 1.确保应用程序在调试模式下运行

第一步是确保 Spring Boot 应用程序在调试模式下运行。这可以通过将以下行添加到 application.properties 文件来完成：

```
spring.boot.devtools.remote.debug=true
```

## 2.启动远程调试器

下一步是启动远程调试器。这可以通过运行以下命令来完成：

```
java -Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=8000,suspend=n -jar myapp.jar
```

将 myapp.jar 替换为您的 Spring Boot 应用程序的名称。

## 3.连接到远程调试器

最后一步是连接到远程调试器。这可以使用 Eclipse 或 IntelliJ 等调试器来完成。在 Eclipse 中，转到 Debug 透视图并选择 Remote Java Application。在“连接”选项卡中，选择包含 Spring Boot 应用程序的项目。在“连接”选项卡中，选择包含 Spring Boot 应用程序的项目。在“连接”选项卡中，选择包含 Spring Boot 应用程序的项目。在“连接”选项卡中，选择包含 Spring Boot 应用程序的项目。在“连接”选项卡中，选择包含 Spring Boot 应用程序的项目。

在 IntelliJ 中，转到运行 > 编辑配置。在远程选项卡中，选择包含 Spring Boot 应用程序的项目。在“连接”选项卡中，选择包含 Spring Boot 应用程序的项目。

# 结论

在本文中，我们探讨了如何使用远程调试器调试 Spring Boot 应用程序。我们还完成了执行此操作所需遵循的步骤。