---
title: Kotlin 和 Docker：打包和运行您的应用程序
description: 
published: true
date: 2023-02-12T00:17:31.021Z
tags: 
editor: markdown
dateCreated: 2023-02-12T00:17:29.381Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kotlin and Docker: Packaging and Running Your Applications***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-docker-packaging-and-running-your-applications)
{.links-list}


# Kotlin 和 Docker：打包和运行您的应用程序

Kotlin 是一种兼容 JVM 的语言，近年来因其简洁的语法和与 Java 的互操作性而受到欢迎。 Docker 是一个容器化平台，使开发人员能够在隔离环境中打包和运行应用程序。

在本文中，我们将展示如何将 Kotlin 应用程序打包到 Docker 容器中并在服务器上运行。我们还将简要讨论结合使用 Kotlin 和 Docker 的一些好处。

## 在 Docker 容器中打包 Kotlin 应用程序

要将 Kotlin 应用程序打包到 Docker 容器中，我们需要创建一个 Dockerfile 来指定基础映像和必要的依赖项。我们将使用 `openjdk:8-jdk-alpine` 图像作为我们的基础图像。此映像包含 OpenJDK 8 JVM 和 Alpine Linux 发行版。 Alpine Linux 是一个轻量级的 Linux 发行版，非常适合 Docker 容器。

我们还需要指定 `kotlin-stdlib` 依赖项。此依赖项包含 Kotlin 标准库，所有 Kotlin 应用程序都需要它。

```Dockerfile
FROM openjdk:8-jdk-alpine

# Add the Kotlin standard library as a dependency
RUN apk add --no-cache kotlin-stdlib
```

接下来，我们需要将 Kotlin 代码复制到容器中。我们将把我们的代码放在 `/app` 目录中。

```Dockerfile
# Copy our Kotlin code into the container
COPY src/ /app/src/
```

最后，我们需要指定 `ENTRYPOINT` 和 `CMD` 值。 `ENTRYPOINT` 值指定容器启动时将运行的命令。 `CMD` 值指定将传递给 `ENTRYPOINT` 命令的参数。在我们的例子中，我们将使用 `kotlinc` 命令编译代码，使用 `java` 命令运行编译后的代码。

```Dockerfile
# Specify the entrypoint and command
ENTRYPOINT ["kotlinc", "-include-runtime", "/app/src/main.kt", "-d", "/app/app.jar"]
CMD ["java", "-jar", "/app/app.jar"]
```

`-include-runtime` 参数告诉 `kotlinc` 编译器在编译代码中包含 Kotlin 运行时。这是必要的，因为 Kotlin 运行时不包含在“kotlin-stdlib”依赖项中。

## 在 Docker 容器中运行 Kotlin 应用程序

现在我们有了 `Dockerfile`，我们可以构建我们的 Docker 镜像并在 Docker 容器中运行我们的 Kotlin 应用程序。

首先，我们需要构建我们的 Docker 镜像。我们将使用 `docker build` 命令来构建我们的镜像。我们将我们的图像命名为“kotlin-app”并使用“latest”标签对其进行标记。

```console
$ docker build -t kotlin-app:latest .
```

接下来，我们需要运行我们的 Docker 镜像。我们将使用 `docker run` 命令来运行我们的图像。我们还将指定“-p 8080:8080”参数，它将主机上的端口“8080”映射到容器中的端口“8080”。

```console
$ docker run -p 8080:8080 kotlin-app:latest
```

我们的 Kotlin 应用程序现在在 Docker 容器中运行，可以通过“http://localhost:8080”访问。

## 一起使用 Kotlin 和 Docker 的好处

结合使用 Kotlin 和 Docker 有几个好处。

首先，Kotlin 是一种非常简洁的语言。这意味着我们的 Kotlin 代码将比等效的 Java 代码小得多。这在 Docker 容器中打包应用程序时很重要，因为较小的图像可以更快地构建和部署。

其次，Kotlin 与 Java 完全互操作。这意味着我们可以在 Kotlin 代码中轻松使用现有的 Java 库。这在使用 Docker 容器化现有 Java 应用程序时很重要。

第三，Kotlin 是一种 JVM 兼容的语言。这意味着我们可以在任何支持 JVM 的平台上运行我们的 Kotlin 代码。这在 Docker 容器中部署应用程序时很重要，因为我们可以在任何支持 Docker 的平台上运行我们的容器，而不管底层操作系统是什么。

## 结论

在本文中，我们展示了如何将 Kotlin 应用程序打包到 Docker 容器中并在服务器上运行它。我们还简要讨论了结合使用 Kotlin 和 Docker 的一些好处。