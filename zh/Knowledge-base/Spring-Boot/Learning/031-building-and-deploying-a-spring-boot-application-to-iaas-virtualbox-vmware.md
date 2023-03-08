---
title: 031：构建 Spring Boot 应用程序并将其部署到 IaaS（Virtualbox、VMware）
description: 
published: true
date: 2023-02-03T23:32:11.914Z
tags: 
editor: markdown
dateCreated: 2023-02-03T23:32:10.307Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [031: Building and deploying a Spring Boot application to IaaS (Virtualbox, VMware)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/031-building-and-deploying-a-spring-boot-application-to-iaas-virtualbox-vmware)
{.links-list}


# 031：构建 Spring Boot 应用程序并将其部署到 IaaS（Virtualbox、VMware）

在本文中，我们将学习如何构建 Spring Boot 应用程序并将其部署到 IaaS（Virtualbox、VMware）。

我们将从使用 Spring Initializr 创建一个新的 Spring Boot 项目开始。对于我们的项目，我们需要选择 Web 和 Thymeleaf 依赖项。

创建项目后，我们将添加一个简单的控制器来呈现 Thymeleaf 模板。

@Controller public class HomeController { @RequestMapping("/") public String home(Model model) { model.addAttribute("message", "Hello, World!");回家”; } }

我们的模板将只显示我们从控制器传递的消息。

<html> <head> <title>你好，世界！</title> </head> <body> <p th:text="${message}"></p> </body> </html>

现在我们的应用程序已完成，我们需要将其打包为 JAR 文件。我们可以通过从项目的根目录运行以下命令来完成此操作：

./mvnw 包

这将在 target/ 目录中创建一个 JAR 文件。

我们现在可以将此 JAR 文件部署到我们的 IaaS 提供商。我们需要创建一个新的 VM 并安装 Java Runtime Environment (JRE)。

一旦我们的 VM 启动并运行，我们可以将 JAR 文件通过 SCP 传输到 VM 并使用以下命令运行它：

java -jar spring-boot-app.jar

现在可以通过 http://{vm-ip-address}:8080 访问我们的应用程序。

这里的所有都是它的！在本文中，我们学习了如何构建 Spring Boot 应用程序并将其部署到 IaaS（Virtualbox、VMware）。