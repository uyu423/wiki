---
title: Spring Tool Suite：终极开发环境
description: 
published: true
date: 2023-02-06T05:32:27.807Z
tags: 
editor: markdown
dateCreated: 2023-02-06T05:32:26.239Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Tool Suite: The Ultimate Development Environment***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-tool-suite-the-ultimate-development-environment)
{.links-list}

      

# Spring 工具套件：终极开发环境

有这么多不同的选项和配置可用，设置开发环境可能是一项艰巨的任务，尤其是对于那些刚接触 IT 世界的人来说。但是，有一个工具可以使这个过程变得更加容易：Spring Tool Suite (STS)。

STS是一个基于Eclipse的IDE，专为开发Spring应用而设计。它具有广泛的功能，可以大大改善开发人员的体验，包括：

- 用于创建新的 Spring Boot、MVC 和 Batch 项目的项目模板。
- 自动生成项目元数据（例如 pom.xml 文件）。
- 内置支持动态重新加载 Java 类和资源。
- 与流行的构建工具集成，例如 Maven 和 Gradle。
- 用于查看应用程序日志输出的控制台视图。

此外，STS 提供了丰富的插件，可以添加更多功能，例如：

- Spring Cloud CLI：允许您在本地计算机上开发、测试和部署 Spring Cloud 应用程序。
- Spring Cloud Data Flow：使用 Spring Cloud Streams 构建数据管道的工具。
- Spring Cloud Security：为 Spring Cloud 应用程序添加安全功能。

凭借所有这些功能，STS 可以成为任何开发人员的强大资产，无论他们的经验水平如何。在本文中，我们将仔细研究如何开始使用 STS 及其一些最有用的功能。

## 安装 STS

STS可以从[Spring Tools网站](https://spring.io/tools)下载。有两个版本可用：

- **标准**版，其中包括核心 STS 功能。
- **终极**版，包括标准版的所有功能，以及用于开发云原生应用程序的附加插件。

对于本文，我们将使用终极版。下载 ZIP 文件后，将其解压缩到您选择的位置并启动 STS 可执行文件。

## 创建一个新项目

当您首次启动 STS 时，您将看到欢迎屏幕。从这里，您可以选择创建新项目、导入现有项目或从目录中打开项目。

我们将创建一个新项目，因此选择“Create a new Spring Starter Project”选项。

![STS 欢迎屏幕](https://i.imgur.com/l7qE4Vx.png)

在下一个屏幕上，系统会要求您提供有关项目的一些信息，例如名称和位置。您还可以选择要使用的构建工具（Maven 或 Gradle）以及要创建的项目类型。

对于此示例，我们将创建一个基于 Maven 的 Spring Boot 项目。输入必要的信息后，单击“完成”按钮。

![新项目屏幕](https://i.imgur.com/DY6rNcu.png)

 STS 现在将创建项目并在 IDE 中打开它。

## 探索 IDE

STS IDE 基于 Eclipse，因此如果您熟悉该 IDE，您应该会感到很熟悉。但是，有一些 STS 特有的功能值得一提。

### Spring Boot 仪表板

STS 最有用的功能之一是 Spring Boot 仪表板。这是一个特殊的视图，可以快速访问最常用的 Spring Boot 功能。

![Spring Boot 仪表板](https://i.imgur.com/uY0A8tV.png)

从仪表板中，您可以查看和管理应用程序的依赖项、启动和停止应用程序、查看应用程序日志等等。

### Spring Boot Bean

STS 的另一个有用特性是 Spring Boot Beans 视图。该视图显示了应用程序中定义的所有 bean 及其依赖项。

![Spring Boot Beans](https://i.imgur.com/Lzq3G8I.png)

这是调试应用程序的有用工具，因为它可以帮助您了解应用程序的不同部分如何组合在一起。

### Spring Boot 应用程序

Spring Boot Apps 视图是另一个特定于 STS 的功能，在开发 Spring Boot 应用程序时非常有用。

![Spring Boot 应用程序](https://i.imgur.com/DxvkVrA.png)

此视图显示了在本地计算机上运行的所有 Spring Boot 应用程序，以及它们的调试和 JMX 端口。当您需要连接到远程应用程序以进行调试或监视时，这会非常有用。

## 结论

在本文中，我们了解了 Spring Tool Suite IDE 的一些最有用的特性。我们还看到了如何安装 STS 和创建一个新的 Spring Boot 项目。

虽然这只是对 STS 必须提供的功能的简要介绍，但它应该让您很好地了解这个强大的工具如何帮助您更有效地开发 Spring 应用程序。