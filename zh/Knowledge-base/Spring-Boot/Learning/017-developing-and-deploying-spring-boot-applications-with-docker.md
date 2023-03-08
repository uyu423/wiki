---
title: 017：使用 Docker 开发和部署 Spring Boot 应用程序
description: 
published: true
date: 2023-02-03T10:04:55.465Z
tags: 
editor: markdown
dateCreated: 2023-02-03T10:04:53.792Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [017: Developing and deploying Spring Boot applications with Docker***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/017-developing-and-deploying-spring-boot-applications-with-docker)
{.links-list}


# 使用 Docker 开发和部署 Spring Boot 应用程序

Docker 是一个可以大大简化开发和部署 Spring Boot 应用程序的过程的工具。在本文中，我们将了解如何使用 Docker 开发和部署 Spring Boot 应用程序。

## 使用 Docker 开发 Spring Boot 应用程序

使用 Docker 开发 Spring Boot 应用程序非常简单。您只需要一个文本编辑器和一个 Dockerfile。

Dockerfile 是一个文本文件，其中包含构建 Docker 映像所需的所有命令。 Docker 镜像是一个文件，其中包含应用程序运行所需的所有文件和依赖项。

要创建 Dockerfile，请在项目的根目录中创建一个名为“Dockerfile”的新文件。然后，将以下行添加到文件中：

```
FROM java:8

ADD . /app

WORKDIR /app

RUN ./gradlew build

EXPOSE 8080

CMD ["java", "-jar", "build/libs/spring-boot-app-0.0.1-SNAPSHOT.jar"]
```

第一行“FROM java:8”告诉 Docker 使用“java:8”Docker 镜像作为我们应用程序的基础镜像。 `java:8` Docker 镜像包含 Java 8 应用程序所需的所有文件和依赖项。

第二行，`ADD。 /app`，告诉 Docker 将当前目录（`./`）中的所有文件添加到 Docker 镜像中的`/app` 目录中。

第三行，“WORKDIR /app”，告诉 Docker 使用“/app”目录作为我们应用程序的工作目录。

第四行，`RUN ./gradlew build`，告诉 Docker 运行 `./gradlew build` 命令来构建我们的应用程序。此命令将编译我们的代码并在 build/libs 目录中创建一个 .jar 文件。

第五行“EXPOSE 8080”告诉 Docker 为我们的应用程序公开端口“8080”。

第六行也是最后一行，`CMD ["java", "-jar", "build/libs/spring-boot-app-0.0.1-SNAPSHOT.jar"]`，告诉 Docker 运行 `java` 命令`-jar` 选项和 `spring-boot-app-0.0.1-SNAPSHOT.jar` 文件作为参数。这将在端口“8080”上启动我们的应用程序。

现在我们有了一个 Dockerfile，我们可以为我们的应用程序构建一个 Docker 镜像。为此，打开终端并导航到项目的根目录。然后，运行以下命令：

```
$ docker build -t spring-boot-app .
```

此命令将为我们的应用程序构建一个 Docker 映像，并使用“spring-boot-app”名称对其进行标记。

构建镜像后，我们可以使用以下命令运行它：

```
$ docker run -p 8080:8080 spring-boot-app
```

此命令将为我们的图像启动一个 Docker 容器，并将主机上的端口“8080”映射到容器上的端口“8080”。

现在，我们可以通过“http://localhost:8080”访问我们的应用程序。

## 使用 Docker 部署 Spring Boot 应用程序

使用 Docker 部署 Spring Boot 应用程序与开发应用程序一样简单。我们只需要一个 Dockerfile 和一个 docker-compose.yml 文件。

docker-compose.yml 文件是一个 YAML 文件，其中包含 docker-compose 的所有必要配置，docker-compose 是一种可用于管理多容器应用程序的工具。

要创建 docker-compose.yml 文件，请在项目的根目录中创建一个名为“docker-compose.yml”的新文件。然后，将以下行添加到文件中：

```
version: '2'

services:
  app:
    build: .
    ports:
      - "8080:8080"
```

第一行，`version: '2'`，告诉 docker-compose 使用 docker-compose 文件格式的版本 2。

第二行，`services:`，告诉 docker-compose 我们要定义一个服务。服务是一个容器，它是多容器应用程序的一部分。

第三行，`app:`，是我们服务的名称。

第四行，`build: .`，告诉 docker-compose 使用当前目录 (`./`) 中的 `Dockerfile` 构建我们的服务。

第五行也是最后一行，`ports: - "8080:8080"`，告诉 docker-compose 将主机上的端口 `8080` 映射到容器上的端口 `8080`。

现在我们有了一个 docker-compose.yml 文件，我们可以使用以下命令部署我们的应用程序：

```
$ docker-compose up
```

此命令将在端口 8080 上启动我们的应用程序。

## 结论

在本文中，我们了解了如何使用 Docker 开发和部署 Spring Boot 应用程序。 Docker 可以大大简化开发和部署 Spring Boot 应用程序的过程。