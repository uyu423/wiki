---
title: 028：构建 Spring Boot 应用程序并将其部署到 PaaS（Heroku、OpenShift）
description: 
published: true
date: 2023-02-03T20:32:44.244Z
tags: 
editor: markdown
dateCreated: 2023-02-03T20:32:39.163Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [028: Building and deploying a Spring Boot application to PaaS (Heroku, OpenShift)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/028-building-and-deploying-a-spring-boot-application-to-paas-heroku-openshift)
{.links-list}


# 028：构建 Spring Boot 应用程序并将其部署到 PaaS（Heroku、OpenShift）

在本文中，我们将学习如何构建 Spring Boot 应用程序并将其部署到平台即服务 (PaaS) 提供商。我们将特别关注两个流行的 PaaS 提供商 Heroku 和 OpenShift。

构建 Spring Boot 应用程序并将其部署到 PaaS 提供商是让您的应用程序快速启动和运行的好方法。 PaaS 提供商为您处理所有基础架构和部署配置，因此您可以专注于开发应用程序。

## 先决条件

在我们开始之前，您需要做一些事情：

* 一个 PaaS 帐户。您可以在 [heroku.com](https://www.heroku.com/) 上注册一个免费的 Heroku 帐户。对于 OpenShift，您可以在 [openshift.com](https://www.openshift.com/) 注册一个免费帐户。
* 文本编辑器或 IDE。我们将在本文中使用 [Visual Studio Code](https://code.visualstudio.com/)，但您可以使用任何您喜欢的编辑器。
* [JDK 8](https://adoptopenjdk.net/) 或更高版本。
* [Maven](https://maven.apache.org/) 3.3.9 或更高版本。

## 创建一个 Spring Boot 应用程序

让我们从创建一个简单的 Spring Boot 应用程序开始。我们将使用 [Spring Initializr](https://start.spring.io/) 来生成项目。

转到 [Spring Initializr](https://start.spring.io/) 并选择以下选项：

* 生成一个`Maven 项目`
* 使用`Java 8`
* 使用 `Spring Boot 2.2.2`
* 包装：`Jar`
* 类型：`Web`
* 神器：`demo`

单击“生成项目”，将下载一个“demo.zip”文件。将 zip 文件的内容解压缩到计算机上的一个目录中。

在 Visual Studio Code 中打开项目，您应该会看到以下项目结构：

```
demo
├── pom.xml
└── src
    └── main
        ├── java
        │   └── com
        │       └── example
        │           └── demo
        │               └── DemoApplication.java
        └── resources
            └── application.properties
```

`pom.xml` 文件是 Maven 项目配置文件。 `src/main/java` 目录包含应用程序的 Java 源代码。 `src/main/resources` 目录包含应用程序配置文件。

打开“DemoApplication.java”文件并添加以下“@RestController”：

```java
package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class DemoApplication {

    @GetMapping("/")
    public String home() {
        return "Hello, world!";
    }

}
```

这个 `@RestController` 公开了一个 `/` 端点，它返回 `Hello, world!` 字符串。

## 在本地运行应用程序

让我们在本地运行该应用程序以确保其正常工作。在终端中，导航到“demo”目录并运行以下命令：

```
mvn spring-boot:run
```

这将在您的本地计算机上启动应用程序。您可以在 [http://localhost:8080](http://localhost:8080) 访问该应用程序。您应该会看到“Hello, world!”字符串。

## 将应用程序部署到 Heroku

现在我们有了一个可以工作的应用程序，让我们将它部署到 Heroku。

Heroku 使用 [Git](https://git-scm.com/) 进行部署，因此我们需要做的第一件事是在 `demo` 目录中初始化一个 Git 存储库。在终端中，运行以下命令：

```
git init
git add .
git commit -m "Initial commit"
```

这将初始化 Git 存储库并进行初始提交。

接下来，我们需要创建一个 Heroku 应用程序。在终端中，运行以下命令：

```
heroku create
```

这将创建一个新的 Heroku 应用程序并将远程添加到您的 Git 存储库。

现在我们可以将应用程序部署到 Heroku。在终端中，运行以下命令：

```
git push heroku master
```

这会将代码推送到 Heroku 远程并触发部署。

部署完成后，您可以在 Heroku 提供的 URL 中查看应用程序。您应该会看到“Hello, world!”字符串。

## 将应用程序部署到 OpenShift

OpenShift 使用 [Git](https://git-scm.com/) 进行部署，因此我们需要做的第一件事是在 `demo` 目录中初始化一个 Git 存储库。在终端中，运行以下命令：

```
git init
git add .
git commit -m "Initial commit"
```

这将初始化 Git 存储库并进行初始提交。

接下来，我们需要创建一个新的 OpenShift 项目。 OpenShift 项目是资源的逻辑分组。我们将使用 OpenShift Web 控制台来创建项目。

登录到 [OpenShift Web 控制台](https://console.openshift.com/)，然后单击“创建项目”。输入 `demo` 作为项目名称，然后单击 `Create`。

创建项目后，我们可以将应用程序部署到 OpenShift。在终端中，运行以下命令：

```
git push openshift master
```

这会将代码推送到 OpenShift 远程并触发部署。

部署完成后，您可以在 OpenShift 提供的 URL 中查看应用程序。您应该会看到“Hello, world!”字符串。