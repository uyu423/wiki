---
title: Spring Boot CLI 命令行界面
description: 
published: true
date: 2023-02-17T18:15:04.368Z
tags: 
editor: markdown
dateCreated: 2023-01-30T22:23:38.612Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Spring Boot CLI Command Line Interface***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-cli-command-line-interface)
{.links-list}



# Spring Boot CLI 命令行界面

Spring Boot CLI 是一个命令行界面，用于快速构建基于 Spring 的应用程序。它提供了一种快速生成 Spring 项目的方法，其中包含所有必要的依赖项。

对于希望快速启动和运行 Spring 的开发人员来说，Spring Boot CLI 是一个重要的工具。在本文中，我们将了解如何使用 Spring Boot CLI 快速创建 Spring 项目。我们还将讨论 Spring Boot CLI 提供的一些功能。

## 入门

为了使用 Spring Boot CLI，您需要安装以下内容：

* Java 8 或更高版本
* Apache Maven 3.3.9 或更高版本

您可以通过运行以下命令检查是否安装了这些：

```
java -version
mvn -version
```

如果您没有安装这些，您可以按照[此处](https://spring.io/guides/gs/getting-started-maven/) 的说明进行操作。

安装这些后，您可以通过访问[此链接](https://repo.spring.io/release/org/springframework/boot/spring-boot-cli/2.3.1.RELEASE/ 下载 Spring Boot CLI spring-boot-cli-2.3.1.RELEASE-bin.zip）。

下载 Spring Boot CLI 后，您需要将其解压缩并将 `bin` 目录添加到您的 `PATH`。这将允许您从任何目录运行 `spring` 命令。

## 创建一个 Spring 项目

现在您已经安装了 Spring Boot CLI，让我们使用它来创建一个 Spring 项目。我们将创建一个使用 [Web](https://start.spring.io/#dependencies=web) 和 [JPA](https://start.spring.io/#dependencies=data-jpa) 的项目依赖项。

为此，我们将使用 `spring init` 命令。此命令将创建一个具有指定依赖项的 Spring 项目。 `-d` 标志用于指定我们要包含在项目中的依赖项。在我们的例子中，我们想要包括 Web 和 JPA 依赖项。我们还将指定 `-b` 标志以指示我们要使用 [bootstrap](https://getbootstrap.com/) 依赖项。

```
spring init -d=web,data-jpa -b
```

这将创建一个名为“my-project”的目录，其结构如下：

```
my-project
├── pom.xml
└── src
    ├── main
    │   ├── java
    │   │   └── com
    │   │       └── example
    │   │           └── myproject
    │   │               └── MyprojectApplication.java
    │   └── resources
    │       └── application.properties
    └── test
        └── java
            └── com
                └── example
                    └── myproject
                        └── MyprojectApplicationTests.java
```

`pom.xml` 文件包含项目的依赖项。 `src/main/java` 目录包含项目的 Java 源代码。 `src/test/java` 目录包含项目的测试。 `src/main/resources` 目录包含项目资源，例如属性文件。

## 运行应用程序

现在我们有了一个 Spring 项目，让我们运行它看看它做了什么。为此，我们将使用 `spring run` 命令。此命令将编译并运行应用程序。

```
spring run src/main/java/com/example/myproject/MyprojectApplication.java
```

这将在端口 8080 上启动应用程序。您可以通过访问 [http://localhost:8080](http://localhost:8080) 查看该应用程序。

## SpringBoot CLI 命令

虽然 `spring run` 命令对于快速运行应用程序很有用，但 Spring Boot CLI 提供了许多其他可用于不同任务的命令。我们将在下面简要讨论一些最有用的命令。

###`弹簧启动`

`spring boot` 命令可用于创建新的 Spring Boot 应用程序。此命令将生成一个具有指定依赖项的新项目。这与我们在上一节中用于创建项目的命令相同。

###`春季大扫除`

`spring clean` 命令可用于清理项目的构建目录。如果您想删除任何编译文件或其他不需要的工件，这将很有用。

###`春季运行`

`spring run` 命令可用于编译和运行应用程序。这与我们在上一节中用于运行应用程序的命令相同。

###`春季测试`

`spring test` 命令可用于运行项目的测试。这对于验证应用程序是否正常运行很有用。

### `弹簧罐`

`spring jar` 命令可用于将应用程序打包成 JAR 文件。这对于将应用程序部署到服务器很有用。

###`春季战争`

`spring war` 命令可用于将应用程序打包成 WAR 文件。这对于将应用程序部署到服务器很有用。

### `spring 帮助`

`spring help` 命令可用于显示所有可用命令的列表。这对于快速概览所有可用命令很有用。

## 结论

在本文中，我们讨论了如何使用 Spring Boot CLI 快速创建基于 Spring 的应用程序。我们还介绍了 Spring Boot CLI 提供的一些最有用的命令。