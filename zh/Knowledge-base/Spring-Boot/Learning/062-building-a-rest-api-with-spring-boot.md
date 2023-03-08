---
title: 062：使用 Spring Boot 构建 REST API
description: 
published: true
date: 2023-02-03T02:57:29.997Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:57:28.427Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [062: Building a REST API with Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/062-building-a-rest-api-with-spring-boot)
{.links-list}


# 062：使用 Spring Boot 构建 REST API

在本文中，我们将学习如何使用 Spring Boot 构建 REST API。

我们将从创建一个新的 Spring Boot 项目开始。然后，我们将向我们的项目添加一个依赖项，以允许我们创建一个 REST API。

接下来，我们将创建一个控制器来处理对我们 API 的 HTTP 请求。最后，我们将使用 Postman 测试我们的 API。

## 创建一个 Spring Boot 项目

首先，我们需要创建一个新的 Spring Boot 项目。我们可以使用 Spring Initializr 来做到这一点。

我们需要指定以下信息：

- 组：com.example
- 神器：演示
- 名称：DemoApplication
- 描述：062 的演示项目
- 包名：com.example.demo
- 包装：罐
- Java 版本：8
- 语言：科特林
- 引导版本：2.1.5

![spring-initializr](https://i.imgur.com/eU0mhVv.png)

填写表格后，我们可以单击“生成项目”。这将下载包含我们项目的 ZIP 文件。

## 添加依赖

接下来，我们需要向我们的项目添加依赖项。这种依赖关系将允许我们创建一个 REST API。

我们可以通过将以下内容添加到我们的 build.gradle 文件中来做到这一点：

```groovy
dependencies {
    ...
    compile("org.springframework.boot:spring-boot-starter-web")
}
```

## 创建控制器

现在我们已经设置了项目，我们可以开始创建我们的 API。

我们将从创建一个控制器开始。该控制器将处理对我们 API 的 HTTP 请求。

我们可以通过在 com.example.demo 包中创建一个名为 DemoController.kt 的新 Kotlin 文件来做到这一点。

```kotlin
package com.example.demo

import org.springframework.web.bind.annotation.GetMapping
import org.springframework.web.bind.annotation.RestController

@RestController
class DemoController {

    @GetMapping("/")
    fun index(): String {
        return "Hello, world!"
    }
}
```

在此文件中，我们创建了一个具有单个端点的控制器。此端点将返回字符串“Hello, world!”访问时。

## 测试我们的 API

现在我们已经创建了我们的 API，我们可以测试它以确保它按预期工作。

我们可以使用 Postman 来做到这一点。 Postman 是一个允许我们向 API 发送 HTTP 请求的工具。

首先，我们需要启动我们的应用程序。我们可以通过运行以下命令来完成此操作：

```
./gradlew bootRun
```

一旦我们的应用程序启动，我们就可以向“/”端点发送 HTTP GET 请求。我们应该看到字符串“Hello, world!”在响应体中。

![邮递员](https://i.imgur.com/zgWVLCg.png)

## 结论

在本文中，我们学习了如何使用 Spring Boot 构建 REST API。我们创建了一个新项目，添加了一个依赖项，创建了一个控制器，并测试了我们的 API。