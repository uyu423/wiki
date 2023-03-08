---
title: 077：使用 Docker 部署 Spring Boot 应用程序
description: 
published: true
date: 2023-02-05T08:32:53.801Z
tags: 
editor: markdown
dateCreated: 2023-02-05T08:32:52.064Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [077: Deploying a Spring Boot Application with Docker***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/077-deploying-a-spring-boot-application-with-docker)
{.links-list}


## 介绍

Docker 是一种容器化技术，它使您能够将应用程序及其所有依赖项打包并将其作为一个单元发送。这使得在任何支持 Docker 的主机上部署和运行您的应用程序变得容易。

在本文中，我们将学习如何使用 Docker 部署 Spring Boot 应用程序。我们将从构建一个简单的 Spring Boot 应用程序并将其打包为 Docker 映像开始。然后我们将在本地 Docker 主机上运行 Docker 映像。最后，我们会将 Docker 映像推送到 Docker 注册表，以便可以将其部署到生产服务器上。

## 先决条件

要继续阅读这篇文章，您需要具备以下条件：

- 文本编辑器
- JDK 8 或更高版本
- Maven 3.0 或更高版本
- Docker CE 18.03 或更高版本

## 构建 Spring Boot 应用程序

我们将从构建一个简单的 Spring Boot 应用程序开始。该应用程序将有一个返回国家列表的 REST 端点。

首先，为项目创建一个新目录并进入该目录。然后创建一个名为 `pom.xml` 的文件，内容如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>spring-boot-docker-example</artifactId>
    <version>1.0-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.4.RELEASE</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```

这是项目的 Maven `pom.xml` 文件。我们正在使用 Spring Boot starter parent，它提供了一种管理依赖项和配置构建的便捷方法。我们还使用了 Spring Boot 启动器 Web 依赖项，其中包括用于构建 Web 应用程序的依赖项。

接下来，创建一个名为 `src/main/java/com/example/springboot/Application.java` 的文件，内容如下：

```java
package com.example.springboot;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

这是主要的应用程序类。它使用“@SpringBootApplication”注释来启用自动配置和组件扫描。

接下来，创建一个名为 `src/main/java/com/example/springboot/controller/CountryController.java` 的文件，内容如下：

```java
package com.example.springboot.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Arrays;
import java.util.List;

@RestController
public class CountryController {

    @GetMapping("/countries")
    public List<String> getCountries() {
        return Arrays.asList("Australia", "Canada", "France", "Germany", "India", "Japan", "United Kingdom", "United States");
    }

}
```

这是“/countries”端点的控制器。它返回国家列表。

现在应用程序已完成，我们可以将其打包为 Docker 镜像。

## 将应用程序打包为 Docker 镜像

我们将使用 Maven 将应用程序打包为 Docker 映像。首先，我们需要添加一个 `<plugin>` 到 `pom.xml` 文件：

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
        <plugin>
            <groupId>com.spotify</groupId>
            <artifactId>dockerfile-maven-plugin</artifactId>
            <version>1.3.6</version>
            <configuration>
                <repository>${docker.repository}</repository>
                <tag>${project.version}</tag>
                <buildArgs>
                    <JAR_FILE>target/${project.build.finalName}.jar</JAR_FILE>
                </buildArgs>
            </configuration>
        </plugin>
    </plugins>
</build>
```

这将添加 Spotify Dockerfile Maven 插件，它将应用程序打包为 Docker 映像。我们还将插件配置为使用“${project.version}”作为 Docker 镜像标签，并将“${project.build.finalName}.jar”文件作为构建参数传递。

接下来，创建一个名为 `src/main/docker/Dockerfile` 的文件，内容如下：

```dockerfile
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG JAR_FILE
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
```

这是图像的 Dockerfile。它使用 OpenJDK 8 Alpine Docker 镜像作为基础镜像。它还将 `${JAR_FILE}` 复制到 `app.jar` 文件并将其设置为图像的入口点。

现在我们可以通过运行以下命令将应用程序打包为 Docker 镜像：

```
$ mvn package docker:build
```

这会将应用程序打包为 JAR 文件并构建 Docker 映像。 Docker 镜像将被标记为“${project.version}”，在本例中为“1.0-SNAPSHOT”。

## 运行 Docker 镜像

现在我们有了 Docker 镜像，我们可以在本地 Docker 主机上运行它。首先，我们需要启动一个 Docker 主机。如果您使用的是 Docker Machine，则可以使用以下命令启动 Docker 主机：

```
$ docker-machine create --driver virtualbox default
```

这将创建一个名为“default”的 Docker 主机。

接下来，我们需要设置一些环境变量，以便我们可以访问 Docker 主机：

```
$ eval $(docker-machine env default)
```

现在我们可以使用以下命令运行 Docker 镜像：

```
$ docker run -d -p 8080:8080 spring-boot-docker-example:1.0-SNAPSHOT
```

这将以分离模式运行 Docker 映像，并将 Docker 主机上的端口“8080”映射到容器上的端口“8080”。

您可以使用以下命令验证容器是否正在运行：

```
$ docker ps
```

你应该看到这样的输出：

```
CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
e9c4b7a4d4f4        spring-boot-docker-example:1.0   "java -Djava.securit…"   3 seconds ago       Up 2 seconds        0.0.0.0:8080->8080/tcp   stoic_ardinghelli
```

现在我们可以通过在 Web 浏览器中打开 http://localhost:8080 来访问该应用程序。你应该看到这样的页面：

![Spring Boot Docker 示例](https://i.imgur.com/hm4Tv0b.png)

## 将 Docker 镜像推送到注册表

现在我们有了一个可用的 Docker 镜像，我们可以将它推送到 Docker 注册表，以便将它部署到生产服务器上。

首先，我们需要创建一个 Docker 注册表。我们将在此示例中使用 Docker Hub。注册一个 Docker Hub 帐户，然后创建一个新的存储库。我们将我们的存储库称为“spring-boot-docker-example”。

创建存储库后，我们可以使用以下命令将 Docker 镜像推送到它：

```
$ docker push spring-boot-docker-example:1.0-SNAPSHOT
```

这会将“spring-boot-docker-example:1.0-SNAPSHOT”图像推送到 Docker Hub 上的“spring-boot-docker-example”存储库。

## 结论

在本文中，我们学习了如何使用 Docker 部署 Spring Boot 应用程序。我们首先构建一个简单的 Spring Boot 应用程序并将其打包为 Docker 映像。然后我们在本地 Docker 主机上运行 Docker 镜像。最后，我们将 Docker 映像推送到 Docker 注册表，以便可以将其部署到生产服务器上。