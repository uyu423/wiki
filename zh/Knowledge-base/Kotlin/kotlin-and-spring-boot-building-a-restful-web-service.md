---
title: Kotlin 和 Spring Boot：构建 RESTful Web 服务
description: 
published: true
date: 2023-02-01T08:36:41.337Z
tags: 
editor: markdown
dateCreated: 2023-02-01T08:36:39.899Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Kotlin and Spring Boot: Building a RESTful Web Service***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-spring-boot-building-a-restful-web-service)
{.links-list}


  Kotlin 是一种运行在 Java 虚拟机上的现代编程语言，可用于构建广泛领域的应用程序。 Spring Boot 是一个框架，可以轻松创建独立的、生产级的基于 Spring 的应用程序。

在本文中，我们将了解如何使用 Kotlin 和 Spring Boot 构建简单的 RESTful Web 服务。我们将从使用 Spring Initializr 创建一个 Kotlin 项目开始。然后，我们将向构建文件中添加一些依赖项。接下来，我们将编写一个简单的控制器来处理 HTTP 请求。最后，我们将运行我们的应用程序并测试我们的 Web 服务。

创建 Kotlin 项目

我们将从使用 Spring Initializr 创建一个 Kotlin 项目开始。转到 Spring Initializr 网站并填写表单以创建一个新项目。确保选择 Kotlin 作为语言，并选择 Web 和 Lombok 依赖项。 Lombok 是一个可用于减少样板代码的库。

![弹簧初始化器](https://spring.io/images/spring-initializr.png)

填写表格后，单击“生成项目”以下载包含该项目的 zip 文件。解压缩 zip 文件并在您喜欢的 IDE 中打开项目。

添加依赖

接下来，我们将向构建文件中添加一些依赖项。首先，我们需要 Kotlin 标准库。将以下依赖项添加到 build.gradle 文件的依赖项部分：

```kotlin
implementation("org.jetbrains.kotlin:kotlin-stdlib-jdk8")
```

接下来，我们将添加 Spring Boot Web 启动器。这个 starter 将为我们提供使用 Spring Boot 构建 Web 应用程序所需的一切。将以下依赖项添加到 build.gradle 文件的依赖项部分：

```kotlin
implementation("org.springframework.boot:spring-boot-starter-web")
```

最后，我们将添加 Lombok 库。这个库将帮助我们减少样板代码。将以下依赖项添加到 build.gradle 文件的依赖项部分：

```kotlin
implementation("org.projectlombok:lombok")
```

编写控制器

接下来，我们将编写一个简单的控制器来处理 HTTP 请求。我们首先在 src/main/kotlin/com/example/helloworld 目录中创建一个名为 HelloController.kt 的 Kotlin 文件。

在这个文件中，我们将定义一个名为 HelloController 的控制器类。这个类将有一个名为 hello() 的方法。此方法将接受一个 HTTP 请求并返回一个字符串。将以下代码添加到 HelloController.kt 文件中：

```kotlin
package com.example.helloworld

import org.springframework.web.bind.annotation.GetMapping
import org.springframework.web.bind.annotation.RestController

@RestController
class HelloController {

    @GetMapping("/hello")
    fun hello(): String {
        return "Hello, World!"
    }

}
```

在此代码中，我们使用 @RestController 注释对我们的 HelloController 类进行了注释。这个注解告诉 Spring 这个类是一个控制器。我们还使用 @GetMapping 注释对我们的 hello() 方法进行了注释。此注释将 hello() 方法映射到 /hello URL。

运行应用程序

现在我们已经编写了我们的控制器，我们已经准备好运行我们的应用程序了。我们可以通过运行以下命令来完成此操作：

```kotlin
./gradlew bootRun
```

此命令将在端口 8080 上启动 Web 服务器。我们可以通过在 Web 浏览器中转到 http://localhost:8080/hello 来访问我们的 Web 服务。我们应该看到以下输出：

你好世界！

测试网络服务

我们还可以使用 curl 命令测试我们的 Web 服务。运行以下命令向我们的 Web 服务发送 GET 请求：

```kotlin
curl -i http://localhost:8080/hello
```

此命令应返回以下输出：

你好世界！

结论

在本文中，我们了解了如何使用 Kotlin 和 Spring Boot 构建简单的 RESTful Web 服务。我们首先使用 Spring Initializr 创建了一个 Kotlin 项目。然后，我们在构建文件中添加了一些依赖项。接下来，我们编写了一个简单的控制器来处理 HTTP 请求。最后，我们运行了我们的应用程序并测试了我们的 Web 服务。