---
title: 在 Spring Boot 中调试和分析
description: 
published: true
date: 2023-02-17T18:02:53.215Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:24:04.985Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Debugging and Profiling in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/debugging-and-profiling-in-spring-boot)
{.links-list}


# 在 Spring Boot 中调试和分析

开发软件可能既困难又耗时。重要的是拥有可以帮助使过程尽可能顺利的工具。在本文中，我们将了解两个这样的工具：调试和分析。

调试是查找和修复软件错误的过程。它可用于查找代码和数据中的错误。分析是一种可用于优化软件的技术。它可用于查找瓶颈并提高性能。

Spring Boot 是用于开发 Web 应用程序的流行框架。它使创建独立的、生产级的基于 Spring 的应用程序变得容易，您可以“直接运行”。它还提供了多种工具来帮助调试和分析。

## 调试 Spring Boot 应用程序

有几种不同的方法可以调试 Spring Boot 应用程序。在本节中，我们将了解两个最流行的方法：使用 spring-boot-devtools 模块和使用远程调试。

### 使用 spring-boot-devtools 模块

spring-boot-devtools模块可用于提升调试体验。它提供了自动重启、实时重新加载和远程调试等功能。

要使用 spring-boot-devtools 模块，请将其作为依赖项添加到您的项目中：

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
  </dependency>
</dependencies>
```

完成后，您可以通过将以下属性添加到 application.properties 文件来启用模块的功能：

```
spring.devtools.restart.enabled=true
spring.devtools.livereload.enabled=true
spring.devtools.remote.debug.local=false
```

第一个属性 spring.devtools.restart.enabled 启用自动重启功能。当类路径中的文件更改时，此功能将自动重新启动应用程序。第二个属性 spring.devtools.livereload.enabled 启用实时重新加载功能。此功能将重新加载已更改的资源，而无需重新启动应用程序。

第三个属性 spring.devtools.remote.debug.local 启用远程调试。此功能将允许您从远程 IDE 调试应用程序。要使用此功能，您需要将属性的值设置为 true 并添加以下属性：

```
spring.devtools.remote.debug.port=8000
```

此属性设置将用于远程调试的端口。完成后，您可以在调试模式下启动应用程序。在 IntelliJ IDEA 中，您可以通过运行 -> 编辑配置来完成此操作。在 Edit Configurations 对话框中，单击 + 按钮并选择 Remote。在 Remote Configuration 对话框中，将端口设置为 8000 并单击 Apply。

您现在可以从 IntelliJ IDEA 调试应用程序。为此，请打开调试工具窗口并单击 + 按钮。在“添加配置”对话框中，选择“远程”并单击“确定”。在 Remote Configuration 对话框中，将端口设置为 8000 并单击 Debug。

### 使用远程调试

如果您使用的是不同的 IDE，您仍然可以使用远程调试。为此，您需要以调试模式启动应用程序并指定将用于调试的端口。在 IntelliJ IDEA 中，您可以通过运行 -> 编辑配置来完成此操作。在 Edit Configurations 对话框中，单击 + 按钮并选择 Remote。在 Remote Configuration 对话框中，将端口设置为 8000 并单击 Apply。

您现在可以从 IntelliJ IDEA 调试应用程序。为此，请打开调试工具窗口并单击 + 按钮。在“添加配置”对话框中，选择“远程”并单击“确定”。在 Remote Configuration 对话框中，将端口设置为 8000 并单击 Debug。

## 分析 Spring Boot 应用程序

分析是一种可用于优化软件的技术。它可用于查找瓶颈并提高性能。有几种不同的方法来分析 Spring Boot 应用程序。在本节中，我们将介绍两种最流行的方法：使用 Spring Boot Actuator 和使用 JProfiler。

### 使用 Spring Boot 执行器

Spring Boot Actuator 是一组可用于监控和管理 Spring Boot 应用程序的工具。它提供了许多功能，包括 Web 界面、用于监视和管理应用程序的端点，以及一组用于收集分析信息的工具。

要使用 Spring Boot Actuator，请将其作为依赖项添加到您的项目中：

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
  </dependency>
</dependencies>
```

完成后，您可以通过访问 http://localhost:8080/actuator 来访问 Web 界面。 Web 界面提供了许多不同的工具来监视和管理应用程序。它还提供了一组用于收集分析信息的工具。

要使用分析工具，您需要将以下属性添加到您的 application.properties 文件中：

```
management.endpoints.web.exposure.include=*
```

此属性将公开执行器的所有端点。完成后，您可以访问 /profiler 端点。此端点将允许您收集和查看分析信息。

### 使用 JProfiler

JProfiler 是一个 Java 分析工具。它可以用来收集各种不同类型的信息，包括线程信息、内存信息和SQL信息。它还提供了许多不同的视图，包括调用树视图、热点视图和实时内存视图。

要使用 JProfiler，您需要安装它并将其作为依赖项添加到您的项目中。您可以通过访问 JProfiler 网站并下载最新版本来执行此操作。完成后，您可以将其作为依赖项添加到您的项目中：

```xml
<dependencies>
  <dependency>
    <groupId>org.jprofiler</groupId>
    <artifactId>jprofiler</artifactId>
    <version>11.0.2</version>
  </dependency>
</dependencies>
```

完成后，您可以在配置文件模式下启动应用程序。在 IntelliJ IDEA 中，您可以通过运行 -> 编辑配置来完成此操作。在 Edit Configurations 对话框中，单击 + 按钮并选择 Profile。在 Profile Configuration 对话框中，选择 JProfiler 选项并单击 Apply。

您现在可以从 IntelliJ IDEA 分析应用程序。为此，请打开分析工具窗口并选择您要使用的分析会话。在会话中，您可以选择要收集的数据和要使用的视图。