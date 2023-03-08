---
title: 030：使用 Gradle 开发和部署 Spring Boot 应用程序
description: 
published: true
date: 2023-02-03T22:32:28.729Z
tags: 
editor: markdown
dateCreated: 2023-02-03T22:32:27.164Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [030: Developing and deploying a Spring Boot application with Gradle***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/030-developing-and-deploying-a-spring-boot-application-with-gradle)
{.links-list}


# 030：使用 Gradle 开发和部署 Spring Boot 应用程序

Spring Boot 是一种流行的 Java 框架，用于开发 Web 应用程序。它使您可以轻松创建独立的、生产级的基于 Spring 的应用程序，您可以“直接运行”。

在本文中，我们将介绍如何使用 Gradle 开发和部署 Spring Boot 应用程序。我们将从设置我们的项目开始，然后我们将编写我们的代码并将其打包到一个 jar 文件中。最后，我们将把我们的应用程序部署到服务器上。

## 设置我们的项目

我们需要做的第一件事是设置我们的项目。我们将为我们的项目创建一个新目录并初始化 Gradle 构建脚本。

```
$ mkdir my-spring-boot-app
$ cd my-spring-boot-app
$ gradle init
```

接下来，我们需要将 Spring Boot 依赖项添加到我们的构建脚本中。我们将通过将以下行添加到我们的 `build.gradle` 文件来做到这一点：

```
dependencies {
    compile 'org.springframework.boot:spring-boot-starter-web'
}
```

## 编写我们的代码

现在我们的项目已经建立，我们可以开始编写代码了。我们将创建一个打印“Hello, world!”的简单 Spring Boot 应用程序。

首先，我们将在我们的 `src/main/java` 目录中创建一个名为 `HelloWorldController.java` 的文件。该文件将包含我们的控制器：

```java
package com.example.myapp;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloWorldController {

    @RequestMapping("/")
    public String index() {
        return "Hello, world!";
    }

}
```

接下来，我们将在我们的 `src/main/java` 目录中创建一个名为 `Application.java` 的文件。该文件将包含我们的主要应用程序类：

```java
package com.example.myapp;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## 打包我们的应用

现在我们的代码已经写好了，我们需要把它打包成一个jar文件。我们可以通过运行“gradle build”命令来做到这一点。这将在我们的 build/libs 目录中创建一个 jar 文件。

## 部署我们的应用程序

现在我们的应用程序已打包，我们可以将其部署到服务器。我们将使用 `java -jar` 命令来运行我们的 jar 文件：

```
$ java -jar build/libs/my-spring-boot-app.jar
```

我们的应用程序将在端口 8080 上启动。我们可以通过在浏览器中访问 http://localhost:8080 来访问它。

## 结论

在本文中，我们介绍了如何使用 Gradle 开发和部署 Spring Boot 应用程序。我们已经建立了我们的项目，编写了我们的代码，将它打包成一个 jar 文件，并将它部署到一个服务器上。