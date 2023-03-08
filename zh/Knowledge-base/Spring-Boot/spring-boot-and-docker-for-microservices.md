---
title: 用于微服务的 Spring Boot 和 Docker
description: 
published: true
date: 2023-02-08T01:32:41.708Z
tags: 
editor: markdown
dateCreated: 2023-02-08T01:32:40.080Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot and Docker for Microservices***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-docker-for-microservices)
{.links-list}


# 介绍

开发人员正在转向微服务作为构建可扩展应用程序的一种方式。微服务是一种软件架构，其中大型应用程序构建为小型独立服务的集合。这种方法有很多好处，包括独立更新和部署服务的能力，以及水平扩展服务的能力。

虽然微服务提供了许多好处，但它们的管理也可能很复杂。这就是 Docker 的用武之地。Docker 是一个容器化平台，可以轻松打包、部署和管理微服务。

在本文中，我们将了解如何使用 Docker 和 Spring Boot 来开发和部署微服务。我们将从一个简单的示例开始，然后探索 Spring Boot 和 Docker 为开发微服务提供的一些更高级的功能。

# 什么是 Spring Boot？

Spring Boot 是一个基于 Java 的框架，可以轻松创建独立的、生产级的基于 Spring 的应用程序。它提供了许多使开发和部署微服务变得容易的特性，包括：

- 嵌入式 Tomcat：Spring Boot 带有嵌入式 Tomcat 服务器，这使您可以轻松地将应用程序作为独立的 Java 应用程序运行。
- 依赖管理：Spring Boot 自动为你管理依赖。当您开发微服务时，这可以节省大量时间，因为您不必担心手动管理依赖项。
- 配置：Spring Boot 提供了多种方式来配置您的应用程序。您可以使用标准的 Java 属性文件、YAML 文件或环境变量。这使得为不同环境（开发、生产等）配置应用程序变得容易。

# 什么是 Docker？

Docker 是一个容器化平台，可以轻松打包、部署和管理应用程序。 Docker 容器是独立的、隔离的环境，可以轻松打包和部署应用程序。

Docker 容器轻巧便携，是微服务的理想选择。它们还具有与平台无关的额外优势，因此它们可以部署在任何支持 Docker 的平台上。

# 使用 Spring Boot 和 Docker 开发微服务

在本节中，我们将了解如何使用 Spring Boot 和 Docker 开发和部署简单的微服务。

# 创建项目

首先，我们需要创建一个新的 Spring Boot 项目。我们可以使用 Spring Initializr 来做到这一点。 Initializr 是一个基于 Web 的工具，可以轻松创建 Spring Boot 项目。

我们将从创建一个简单的 Maven 项目开始。我们将我们的项目命名为“hello-world”，我们将使用最新版本的 Spring Boot（撰写本文时为 2.0.4）。我们还将添加“Web”和“Actuator”依赖项，因为我们的示例需要这两者。

创建项目后，我们需要向 `pom.xml` 文件添加一些依赖项：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

# 创建服务

现在我们已经设置了项目，可以创建微服务了。我们将从创建一个简单的“HelloController”开始：

```java
@RestController
public class HelloController {

    @RequestMapping("/")
    public String index() {
        return "Hello, world!";
    }
}
```

这个控制器将映射到 `/` 路径，它会返回字符串“Hello, world!”被调用时。

# 添加一个 Dockerfile

现在我们已经创建了微服务，我们需要向我们的项目添加一个 `Dockerfile`。 `Dockerfile` 是一个文本文件，其中包含构建 Docker 映像的说明。

我们的 `Dockerfile` 将非常简单。我们将从指定要使用的基本图像开始。对于我们的示例，我们将使用 `openjdk:8-jdk-alpine` 图像。此映像包含最小版本的 Alpine Linux 和 OpenJDK 8 JDK。

接下来，我们将添加几行来安装我们的应用程序需要的依赖项：

```dockerfile
FROM openjdk:8-jdk-alpine

RUN apk add --no-cache curl
```

我们正在使用 `apk` 命令来安装 `curl` 命令行工具。 `curl` 稍后将用于向我们的应用程序发出请求以测试它是否正在运行。

现在，我们将添加几行以将我们的应用程序 jar 文件复制到图像中，并指定在容器启动时应运行的命令：

```dockerfile
FROM openjdk:8-jdk-alpine

RUN apk add --no-cache curl

COPY target/hello-world-0.0.1-SNAPSHOT.jar /hello-world.jar

ENTRYPOINT ["java", "-jar", "/hello-world.jar"]
```

# 构建 Docker 镜像

现在我们有了 `Dockerfile`，我们可以构建我们的 Docker 镜像了。我们将使用 `docker build` 命令来构建镜像。我们将给我们的图像命名为“hello-world”：

```
$ docker build -t hello-world .
```

# 运行容器

现在我们有了 Docker 镜像，我们可以运行我们的容器了。我们将使用 `docker run` 命令来运行我们的容器。我们还将指定我们希望容器运行的端口。在我们的示例中，我们将使用端口 8080：

```
$ docker run -p 8080:8080 hello-world
```

# 测试应用程序

现在我们的容器正在运行，我们可以测试我们的应用程序。我们将使用 `curl` 命令向我们的应用程序发出请求：

```
$ curl http://localhost:8080

Hello, world!
```

# 结论

在本文中，我们了解了如何使用 Spring Boot 和 Docker 来开发和部署微服务。我们已经了解了如何创建一个简单的微服务，如何为我们的服务构建 Docker 镜像，以及如何在 Docker 容器中运行我们的服务。