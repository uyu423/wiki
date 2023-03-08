---
title: 带有 Netflix OSS 的 Spring Boot 微服务
description: 
published: true
date: 2023-02-08T00:32:55.396Z
tags: 
editor: markdown
dateCreated: 2023-02-08T00:32:53.647Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot Microservices with Netflix OSS***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-microservices-with-netflix-oss)
{.links-list}


# 使用 Netflix OSS 的 Spring Boot 微服务

过去，大型单体应用程序是作为一个单元构建的。然而，随着应用程序规模和复杂性的增长，它们变得越来越难以维护。此外，这些应用程序的部署变得更加复杂，因为必须一次部署整个应用程序。

为了解决这些问题，微服务已成为构建应用程序的流行架构风格。微服务是小型、独立的服务，它们协同工作以形成更大的应用程序。这种架构有很多好处，包括：

- 易于部署和扩展：微服务可以独立部署和扩展，这使得部署新功能或根据需要扩展服务变得容易。

- 松散耦合：服务是独立的，可以在不影响其他服务的情况下进行更改或更新。

- 弹性：如果一项服务出现故障，其他服务可以继续运行。

Netflix OSS 是一组用于构建微服务的工具和库。在本文中，我们将学习如何使用 Netflix OSS 构建 Spring Boot 微服务。

## 先决条件

在我们开始之前，您需要做一些事情：

- Java 8
- Maven 3.3.9 或更高版本

## 创建一个 Spring Boot 项目

我们将从创建一个 Spring Boot 项目开始。对于这个例子，我们将使用 Spring Initializr 来生成我们的项目。

转到 https://start.spring.io/ 并选择以下选项：

- 项目：Maven 项目
- 语言：Java
- 春季启动版本：2.1.3

单击“生成项目”以下载项目。

## 添加依赖

接下来，我们需要向我们的项目添加一些依赖项。打开生成的 pom.xml 文件并添加以下依赖项：

```xml
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-actuator</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
	</dependency>
</dependencies>
```

`spring-boot-starter-actuator` 依赖项提供了监控和管理我们的应用程序的功能。 `spring-cloud-starter-netflix-eureka-client` 依赖项提供与 Eureka 服务发现工具的集成。

## 配置尤里卡

Eureka 是一个服务发现工具。它允许服务自行注册并被其他服务发现。我们将使用 Eureka 来发现我们的微服务。

首先，我们需要在 application.properties 文件中添加一些配置：

```properties
eureka.instance.hostname=localhost
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```

接下来，我们将创建一个“@Configuration”类并使用“@EnableEurekaClient”对其进行注释：

```java
@Configuration
@EnableEurekaClient
public class EurekaConfig {
}
```

## 创建微服务

现在我们已经设置了项目，可以开始创建微服务了。对于此示例，我们将创建一个返回问候语的简单服务。

首先，我们将创建一个 `GreetingController`：

```java
@RestController
public class GreetingController {

    @GetMapping("/greeting")
    public String greeting() {
        return "Hello, world!";
    }
}
```

接下来，我们将创建一个“@Configuration”类并使用“@EnableWebMvc”对其进行注释：

```java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {
}
```

最后，我们将创建一个“@SpringBootApplication”类：

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

## 构建并运行应用程序

现在我们已经创建了微服务，我们可以构建并运行它。在您的终端中，导航到项目目录并运行以下命令：

```
mvn spring-boot:run
```

您应该看到以下输出：

```
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.1.3.RELEASE)

2019-03-29 13:48:41.537  INFO 14073 --- [           main] c.e.a.Application                    : Starting Application on my-macbook-pro.local with PID 14073 (/Users/jdoe/projects/spring-boot-microservices/target/classes started by jdoe in /Users/jdoe/projects/spring-boot-microservices)
2019-03-29 13:48:41.541  INFO 14073 --- [           main] c.e.a.Application                    : No active profile set, falling back to default profiles: default
2019-03-29 13:48:42.591  INFO 14073 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2019-03-29 13:48:42.604  INFO 14073 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2019-03-29 13:48:42.604  INFO 14073 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.17]
2019-03-29 13:48:42.617  INFO 14073 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2019-03-29 13:48:42.618  INFO 14073 --- [           main] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 1735 ms
2019-03-29 13:48:42.791  INFO 14073 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2019-03-29 13:48:42.917  INFO 14073 --- [           main] c.n.eureka.cluster. PeersRefreshScheduler : Starting...
2019-03-29 13:48:42.932  INFO 14073 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2019-03-29 13:48:42.935  INFO 14073 --- [           main] c.e.a.Application                    : Started Application in 1.948 seconds (JVM running for 2.485)
```

您现在可以通过 http://localhost:8080/greeting 访问该服务。

## 配置微服务

现在我们的微服务已启动并运行，我们需要对其进行配置。我们将从向我们的 application.properties 文件添加一个 spring.application.name 属性开始：

```properties
spring.application.name=greeting-service
```

此属性设置我们服务的名称。 Eureka 将使用它来识别我们的服务。

接下来，我们将添加一个 `server.port` 属性：

```properties
server.port=8081
```

此属性设置我们的服务将在其上运行的端口。默认情况下，Spring Boot 将在端口 8080 上运行。但是，我们可以通过设置 `server.port` 属性来更改它。

## 向 Eureka 注册微服务

现在我们的微服务已经配置好了，我们需要向 Eureka 注册它。为此，我们将向我们的 Application 类添加一个 @EnableEurekaClient 注释：

```java
@SpringBootApplication
@EnableEurekaClient
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

这个注释告诉 Spring 向 Eureka 注册我们的微服务。

## 构建并运行应用程序

现在我们已经用 Eureka 注册了我们的微服务，我们可以构建并运行它。在您的终端中，导航到项目目录并运行以下命令：

```
mvn spring-boot:run
```

您应该看到以下输出：

```
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.1.3.RELEASE)

2019-03-29 13:54:45.264  INFO 29122 --- [           main] c.e.a.Application                    : Starting Application on my-macbook-pro.local with PID 29122 (/Users/jdoe/projects/spring-boot-microservices/target/classes started by jdoe in /Users/jdoe/projects/spring-boot-microservices)
2019-03-29 13:54:45.266  INFO 29122 --- [           main] c.e.a.Application                    : No active profile set, falling back to default profiles: default
2019-03-29 13:54:46.318  INFO 29122 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8081 (http)
2019-03-29 13:54:46.330  INFO 29122 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2019-03-29 13:54:46.331  INFO 29122 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.17]
2019-03-29 13:54:46.344  INFO 29122 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2019-03-29 13:54:46.345  INFO 29122 --- [           main] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 1773 ms
2019-03-29 13:54:46.522  INFO 29122 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2019-03-29 13:54:46.643  INFO 29122 --- [           main] c.n.eureka.cluster. PeersRefreshScheduler : Starting...
2019-03-29 13:54:46.657  INFO 29122 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8081 (http) with context path ''
2019-03-29 13:54:46.660  INFO 29122 --- [           main] c.e.a.Application                    : Started Application in 1.965 seconds (JVM running for 2.502)
```

您现在可以通过 http://localhost:8081/greeting 访问该服务。

## 测试微服务

现在我们的微服务已启动并运行，我们可以对其进行测试。在您的终端中，运行以下命令：

```
curl http://localhost:8081/greeting
```

您应该看到以下输出：

```
Hello, world!
```

## 结论

在本文中，我们学习了如何使用 Netflix OSS 构建 Spring Boot 微服务。我们还学习了如何向 Eureka 注册微服务以及如何测试它。