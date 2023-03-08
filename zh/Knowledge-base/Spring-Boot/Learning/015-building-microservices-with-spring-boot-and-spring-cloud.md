---
title: 015：使用 Spring Boot 和 Spring Cloud 构建微服务
description: 
published: true
date: 2023-02-03T09:36:34.580Z
tags: 
editor: markdown
dateCreated: 2023-02-03T09:36:32.947Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [015: Building microservices with Spring Boot and Spring Cloud***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/015-building-microservices-with-spring-boot-and-spring-cloud)
{.links-list}


# 介绍

微服务是一种用于构建云原生应用程序的流行架构风格。它们是小型的独立单元，可以独立部署并组合成复杂的应用程序。

Spring Boot 是用于构建微服务的流行框架。它使创建可以“直接运行”的独立的、生产级的基于 Spring 的应用程序变得容易。

Spring Cloud 是一个用于构建微服务的开源工具生态系统。它为分布式系统中使用的常见模式提供库，例如服务发现、断路器和分布式跟踪。

在本文中，我们将学习如何使用 Spring Boot 和 Spring Cloud 构建微服务。我们将从一个简单的“hello world”微服务示例开始，然后我们将使用 Spring Cloud Netflix Eureka 和 Ribbon 添加服务发现和负载平衡。最后，我们将使用 Spring Cloud Sleuth 添加分布式跟踪。

# 构建一个“Hello World”微服务

让我们从创建一个简单的“hello world”微服务开始。我们将使用 Spring Initializr 生成具有以下依赖项的项目：

- 网络
- 执行器

Web 依赖项添加了对使用 Spring MVC 构建 Web 应用程序的支持。 Actuator 依赖项增加了对监视和管理我们的应用程序的支持。

生成项目后，我们可以在我们的 IDE 中打开它并添加一个简单的控制器：

```java
@RestController
public class HelloController {

    @RequestMapping("/")
    public String hello() {
        return "Hello, world!";
    }

}
```

这个控制器有一个返回“Hello, world!”的端点。信息。

要运行我们的应用程序，我们可以使用 Spring Boot Maven 插件：

```
./mvnw spring-boot:run
```

应用程序启动并运行后，我们可以在 http://localhost:8080/ 访问“hello world”端点。

# 添加服务发现

在微服务架构中，服务通常部署在节点集群上。部署服务时，需要向服务发现服务器注册，以便其他服务可以找到它。

Spring Cloud Netflix Eureka 是一个流行的服务发现服务器。要将 Eureka 添加到我们的项目中，我们可以添加以下依赖项：

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

添加依赖项后，我们可以通过将 @EnableEurekaServer 注释添加到我们的主应用程序类来启用 Eureka 服务器：

```java
@SpringBootApplication
@EnableEurekaServer
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

我们现在可以启动我们的应用程序并访问 http://localhost:8761/ 上的 Eureka 仪表板。

# 添加负载均衡

在微服务架构中，一个服务部署在多个节点上是很常见的。调用服务时，负载平衡器用于将请求路由到其中一个节点。

Spring Cloud Netflix Ribbon 是一个流行的负载均衡器。要将 Ribbon 添加到我们的项目中，我们可以添加以下依赖项：

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-ribbon</artifactId>
</dependency>
```

添加依赖项后，我们可以通过将 @RibbonClient 注释添加到我们的主应用程序类来配置 Ribbon：

```java
@SpringBootApplication
@EnableEurekaServer
@RibbonClient(name = "hello-service")
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

此注解为“hello-service”服务配置了一个 Ribbon 客户端。

# 添加分布式跟踪

在微服务架构中，可能很难解决问题，因为请求可以通过多个服务进行路由。分布式跟踪可以通过跟踪流经系统的请求来提供帮助。

Spring Cloud Sleuth 是一个流行的分布式跟踪框架。要将 Sleuth 添加到我们的项目中，我们可以添加以下依赖项：

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-sleuth</artifactId>
</dependency>
```

添加依赖项后，Sleuth 将自动配置为跟踪请求。

# 结论

在本文中，我们学习了如何使用 Spring Boot 和 Spring Cloud 构建微服务。我们从一个简单的“hello world”微服务开始，并添加了服务发现、负载平衡和分布式跟踪。