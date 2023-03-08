---
title: 034：将 Spring Boot 与 Spring Cloud Config 结合使用
description: 
published: true
date: 2023-02-04T02:32:36.860Z
tags: 
editor: markdown
dateCreated: 2023-02-04T02:32:31.602Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [034: Using Spring Boot with Spring Cloud Config***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/034-using-spring-boot-with-spring-cloud-config)
{.links-list}


# 使用 Spring Boot 和 Spring Cloud Config

Spring Cloud Config 为分布式系统中的外部化配置提供服务器端和客户端支持。通过 @EnableConfigServer 注释，Config Server 可以很容易地与 Spring Boot 应用程序一起使用。

在本文中，我们将了解如何在 Spring Boot 应用程序中使用配置服务器。我们还将了解如何使用 Config Client 连接到 Config Server 并获取配置。

## 设置配置服务器

我们需要做的第一件事是设置配置服务器。我们可以在我们的 Spring Boot 应用程序上使用 @EnableConfigServer 注释来做到这一点：

```java
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {

    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}
```

这将在我们的应用程序上启用配置服务器。默认情况下，配置服务器将从位于应用程序类路径中的文件提供配置。

我们还可以配置配置服务器以从 Git 存储库中获取配置。例如，我们可以将以下内容添加到我们的 application.properties 文件中：

```properties
spring.cloud.config.server.git.uri=https://github.com/spring-cloud/spring-cloud-config
spring.cloud.config.server.git.searchPaths=config-repo
```

这将告诉配置服务器从 config-repo 目录中的 spring-cloud-config GitHub 存储库获取配置。

## 设置配置客户端

现在我们已经设置了配置服务器，我们可以设置我们的配置客户端。 Config Client 是一个 Spring Boot 应用程序，它从 Config Server 获取配置。

我们可以使用@EnableConfigClient 注释设置配置客户端：

```java
@SpringBootApplication
@EnableConfigClient
public class ConfigClientApplication {

    public static void main(String[] args) {
        SpringApplication.run(ConfigClientApplication.class, args);
    }
}
```

这将在我们的应用程序上启用 Config Client。默认情况下，Config Client 将通过 http://localhost:8888 连接到 Config Server。

我们还可以配置 Config Client 以连接到不同的 Config Server。例如，我们可以将以下内容添加到我们的 application.properties 文件中：

```properties
spring.cloud.config.uri=http://config-server:8888
```

这将告诉配置客户端连接到位于 http://config-server:8888 的配置服务器。

## 获取配置

一旦我们设置了 Config Server 和 Config Client，我们就可以从 Config Server 获取配置。 Config Client 将获取配置并将其提供给我们的应用程序。

例如，我们可以将以下内容添加到我们的 application.properties 文件中：

```properties
spring.cloud.config.name=my-app
```

这将告诉配置客户端获取 my-app 应用程序的配置。该配置将通过 Spring 环境提供给我们的应用程序。

我们还可以获取特定配置文件的配置。例如，我们可以将以下内容添加到我们的 application.properties 文件中：

```properties
spring.cloud.config.name=my-app
spring.cloud.config.profile=dev
```

这将告诉 Config Client 使用 dev 配置文件获取 my-app 应用程序的配置。该配置将通过 Spring 环境提供给我们的应用程序。

## 结论

在这篇文章中，我们研究了如何将配置服务器与 Spring Boot 应用程序一起使用。我们还研究了如何使用 Config Client 连接到 Config Server 并获取配置。