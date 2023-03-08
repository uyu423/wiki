---
title: 069：为高级开发定制 Spring Boot CLI
description: 
published: true
date: 2023-02-05T03:32:26.881Z
tags: 
editor: markdown
dateCreated: 2023-02-05T03:32:21.532Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [069: Customizing the Spring Boot CLI for Advanced Development***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/069-customizing-the-spring-boot-cli-for-advanced-development)
{.links-list}


# 为高级开发定制 Spring Boot CLI

Spring Boot CLI 是快速引导 Spring 应用程序的绝佳工具。它允许您创建独立的基于 Spring 的应用程序，这些应用程序可以从命令行运行而无需 Web 服务器。

在本文中，我们将了解如何为高级开发自定义 Spring Boot CLI。我们将介绍如何安装 CLI、如何创建和运行 Spring Boot 应用程序，以及如何根据您自己的开发需求自定义 CLI。

## 安装 Spring Boot CLI

Spring Boot CLI 是一个命令行工具，可用于快速创建和运行 Spring Boot 应用程序。它可以作为独立的可执行 JAR 文件或 Homebrew 包使用。

要安装 Spring Boot CLI，请先从 Spring Boot 网站下载最新版本的 CLI。然后，解压缩下载的文件并将 `spring-boot-cli/bin` 目录添加到您的 `PATH`。

或者，如果您使用的是 Homebrew，则可以通过运行以下命令来安装 Spring Boot CLI：

```
$ brew tap pivotal/tap
$ brew install springboot
```

## 创建一个 Spring Boot 应用程序

现在我们已经安装了 Spring Boot CLI，让我们创建一个简单的 Spring Boot 应用程序。我们将从为我们的项目创建一个新目录开始：

```
$ mkdir my-app
$ cd my-app
```

接下来，我们将在项目目录中创建一个名为“application.properties”的新文件。该文件将包含我们的 Spring Boot 应用程序的配置。我们将 `spring.main.banner-mode` 属性设置为 `off` 以便在我们的应用程序运行时不显示 Spring Boot 横幅：

```
spring.main.banner-mode=off
```

现在，我们可以创建我们的 Spring Boot 应用程序。我们将使用 `spring` 命令创建一个新的 `@SpringBootApplication` 类：

```
$ spring init -n com.example.myapp -d web my-app.jar
```

这将在我们的项目目录中创建一个新的“my-app.jar”文件。我们可以通过执行以下命令来运行我们的应用程序：

```
$ java -jar my-app.jar
```

我们的应用程序将启动并可通过“http://localhost:8080”访问。

## 自定义 Spring Boot CLI

Spring Boot CLI 提供了许多用于自定义其行为的选项。这些选项可以在命令行或 `spring` 配置文件中指定。

`spring` 配置文件是 Spring Boot CLI 启动时读取的 YAML 文件。该文件可用于指定 `spring` 命令的选项，例如默认项目目录和默认包名称。

要创建 `spring` 配置文件，请在您的主目录中创建一个名为 `.spring-configuration.yaml` 的新文件。该文件的内容将在启动时由 Spring Boot CLI 读取。

这是一个示例 `spring` 配置文件：

```yaml
spring:
  project:
    default-project-dir: ~/projects
  package:
    default-package-name: com.example
```

此文件将默认项目目录设置为“~/projects”，并将默认包名称设置为“com.example”。

现在，当我们创建一个新的 Spring Boot 应用程序时，`spring` 命令将使用这些默认值：

```
$ spring init my-app
```

这将在 ~/projects/my-app 目录中使用 com.example 包名称创建一个新的 Spring Boot 应用程序。

我们还可以在 `spring` 命令行上指定选项。例如，我们可以使用 `--project-dir` 选项来设置项目目录：

```
$ spring init --project-dir=~/my-app my-app
```

这将在 ~/my-app 目录中创建一个新的 Spring Boot 应用程序。

## 结论

在本文中，我们研究了如何为高级开发定制 Spring Boot CLI。我们介绍了如何安装 CLI、如何创建和运行 Spring Boot 应用程序以及如何根据您自己的开发需求自定义 CLI。