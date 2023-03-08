---
title: 095：Kotlin 中的 Web 开发：使用 Kotlin 和 Spring 构建 Web 应用程序
description: 
published: true
date: 2023-02-07T01:17:30.333Z
tags: 
editor: markdown
dateCreated: 2023-02-07T01:17:28.754Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [095: Web Development in Kotlin: Building Web Applications with Kotlin and Spring***English** document is available*](/en/Knowledge-base/Kotlin/Learning/095-web-development-in-kotlin-building-web-applications-with-kotlin-and-spring)
{.links-list}


# 095：Kotlin 中的 Web 开发：使用 Kotlin 和 Spring 构建 Web 应用程序

使用 Kotlin 和 Spring 进行 Web 开发是构建现代 Web 应用程序的绝佳方式。 Kotlin 是一种运行在 Java 虚拟机上的静态类型编程语言，可用于开发服务器端和客户端应用程序。 Spring 是一种流行的 Java 应用程序框架，可以轻松创建 Web 应用程序。

在本文中，我们将了解如何使用 Kotlin 和 Spring 构建 Web 应用程序。我们将从了解使用 Kotlin 进行 Web 开发的一些好处开始。然后，我们将了解如何设置 Kotlin 和 Spring 开发环境。最后，我们将介绍一个使用 Kotlin 和 Spring 的简单示例 Web 应用程序。

## 为什么使用 Kotlin 进行 Web 开发？

考虑使用 Kotlin 进行 Web 开发的原因有很多。 Kotlin 是一种简洁而富有表现力的编程语言，可以帮助您编写更少的代码并完成更多的工作。 Kotlin 还可以与 Java 互操作，这意味着您可以在 Kotlin 代码中使用现有的 Java 库。 Kotlin 还得到 JetBrains 的支持，JetBrains 是流行的 IntelliJ IDEA Java IDE 背后的公司，因此您可以相信 Kotlin 将继续得到开发和支持。

## 设置 Kotlin 和 Spring 开发环境

在我们开始使用 Kotlin 和 Spring 开发 Web 应用程序之前，我们需要设置一个开发环境。我们需要安装 Kotlin 编译器和运行时，以及 Java 开发工具包 (JDK)。我们还需要安装 Spring Framework。

有几种不同的方式来安装 Kotlin。我们可以从 Kotlin 网站下载 Kotlin 编译器，也可以使用 Gradle 或 Maven 等构建工具。我们将在此示例中使用 Gradle。

首先，我们需要在项目的根目录中创建一个名为 `build.gradle` 的文件。我们将向文件中添加以下行：

```groovy
plugins {
    id 'org.jetbrains.kotlin.jvm' version '1.3.72'
}

repositories {
    jcenter()
}

dependencies {
    implementation 'org.jetbrains.kotlin:kotlin-stdlib-jdk8'
    implementation 'org.springframework.boot:spring-boot-starter-webflux'
}
```

该文件告诉 Gradle 下载 Kotlin 编译器和运行时，以及 Spring 框架。

接下来，我们需要在项目的根目录中创建一个名为 settings.gradle 的文件。我们将在文件中添加以下行：

```groovy
include ':kotlin-web-example'
```

该文件告诉 Gradle 将我们的项目包含在构建中。

最后，我们需要在项目的根目录中创建一个名为“kotlin-web-example.gradle”的文件。我们将向文件中添加以下行：

```groovy
group 'com.example'
version '0.0.1-SNAPSHOT'

apply plugin: 'org.jetbrains.kotlin.jvm'

repositories {
    jcenter()
}

dependencies {
    implementation 'org.jetbrains.kotlin:kotlin-stdlib-jdk8'
    implementation 'org.springframework.boot:spring-boot-starter-webflux'
}

```

这个文件告诉 Gradle 我们项目的组和版本，以及我们需要的依赖项。

现在我们已经设置了构建文件，我们可以运行 `gradle build` 命令来构建我们的项目。这将下载 Kotlin 编译器和运行时，以及 Spring 框架。

## 一个简单的 Kotlin 和 Spring Web 应用程序

现在我们已经设置了开发环境，可以开始编写一些代码了。我们将首先在我们项目的 `src/main/kotlin` 目录中创建一个名为 `HelloController.kt` 的文件。我们将向文件中添加以下代码行：

```kotlin
package com.example.helloworld

import org.springframework.web.bind.annotation.GetMapping
import org.springframework.web.bind.annotation.RestController

@RestController
class HelloController {

    @GetMapping("/hello")
    fun hello(): String {
        return "Hello, world!"
    }

}
```

这段代码定义了一个简单的 `HelloController` 类，它有一个 `hello` 方法。此方法使用“@GetMapping”注释进行注释，它告诉 Spring 在对“/hello”路径发出“GET”请求时应调用此方法。 `@RestController` 注解告诉 Spring 这个类是一个处理 web 请求的控制器。

接下来，我们需要在项目的 src/main/kotlin 目录中创建一个名为 Application.kt 的文件。我们将向文件中添加以下代码行：

```kotlin
package com.example.helloworld

import org.springframework.boot.SpringApplication
import org.springframework.boot.autoconfigure.SpringBootApplication

@SpringBootApplication
class Application

fun main(args: Array<String>) {
    SpringApplication.run(Application::class.java, *args)
}
```

此代码定义了一个简单的“Application”类，该类使用“@SpringBootApplication”注释进行注释。这个注释告诉 Spring 这是一个 Spring Boot 应用程序。 `main` 方法是我们应用程序的入口点。此方法调用启动我们的应用程序的 `SpringApplication.run` 方法。

现在我们已经编写了代码，我们可以运行 `gradle build` 命令来构建我们的项目。这将编译我们的 Kotlin 代码并将其打包到一个 JAR 文件中。

然后我们可以运行 `java -jar build/libs/kotlin-web-example-0.0.1-SNAPSHOT.jar` 命令来启动我们的应用程序。然后我们可以在 http://localhost:8080/hello 访问我们的应用程序。

## 结论

在本文中，我们了解了如何使用 Kotlin 和 Spring 构建 Web 应用程序。我们已经看到 Kotlin 如何帮助我们编写更少的代码，以及 Spring 如何使创建 Web 应用程序变得容易。我们还了解了如何设置 Kotlin 和 Spring 开发环境以及如何编写简单的 Web 应用程序。