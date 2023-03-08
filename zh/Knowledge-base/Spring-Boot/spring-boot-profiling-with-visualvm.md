---
title: 使用 VisualVM 进行 Spring Boot 分析
description: 
published: true
date: 2023-01-31T20:57:39.329Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:57:35.631Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Spring Boot Profiling with VisualVM***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-profiling-with-visualvm)
{.links-list}



# 使用 VisualVM 进行 Spring Boot 分析

Spring Boot 是构建微服务和其他生产级应用程序的绝佳框架。使用 Spring Boot 的好处之一是它带有嵌入式 Tomcat 服务器，这使得将应用程序部署为独立 jar 变得容易。

但是，使用嵌入式服务器的缺点之一是很难解决性能问题。在本文中，我们将了解如何使用 VisualVM 来分析 Spring Boot 应用程序。

## 什么是 VisualVM？

VisualVM 是一个提供图形界面的工具，用于查看有关 Java 应用程序的详细信息。它可用于监控 JVM 上运行的应用程序并对其进行故障排除。

## 安装 VisualVM

VisualVM 包含在 Oracle JDK 中，因此如果您安装了 JDK，那么您已经拥有了 VisualVM。如果您没有安装 JDK，可以从 [Oracle 网站](https://www.oracle.com/java/technologies/visualvm.html) 下载 VisualVM。

## 分析 Spring Boot 应用程序

现在我们已经安装了 VisualVM，让我们来看看如何使用它来分析 Spring Boot 应用程序。

首先，我们需要启动我们的 Spring Boot 应用程序。我们将为此示例使用 [Spring PetClinic](https://github.com/spring-projects/spring-petclinic) 示例应用程序。

一旦应用程序启动并运行，我们就可以打开 VisualVM 并连接到正在运行的应用程序。为此，单击“文件”菜单并选择“添加 JMX 连接”。

![VisualVM 添加 JMX 连接](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-add-jmx-connection.png)

在“添加 JMX 连接”对话框中，输入正在运行的应用程序的主机和端口。默认主机是“localhost”，默认端口是“1099”。

![VisualVM 添加 JMX 连接对话框](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-add-jmx-connection-dialog.png)

单击“确定”以连接到正在运行的应用程序。

一旦 VisualVM 连接到正在运行的应用程序，您应该会在“应用程序”选项卡中看到该应用程序。

![VisualVM 应用程序选项卡](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-applications-tab.png)

要开始分析应用程序，请在“应用程序”选项卡中选择应用程序并单击“配置文件”按钮。

![VisualVM 配置文件按钮](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-profile-button.png)

在“Profile Application”对话框中，选择“CPU”分析类型并单击“Start”。

![VisualVM 配置文件应用对话框](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-profile-application-dialog.png)

分析会话启动后，您可以使用 VisualVM 查看线程活动、内存使用情况以及有关正在运行的应用程序的其他信息。

![VisualVM 监视器选项卡](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-monitor-tab.png)

当您完成对应用程序的分析后，您可以通过选择“文件”菜单并选择“退出”来停止分析会话。

## 结论

在本文中，我们了解了如何使用 VisualVM 来分析 Spring Boot 应用程序。 VisualVM 是一个强大的工具，可用于解决 Spring Boot 应用程序中的性能问题。