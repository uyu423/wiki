---
title: 用于分布式系统的 Spring Boot 和 Spring Cloud
description: 
published: true
date: 2023-02-03T19:17:27.803Z
tags: 
editor: markdown
dateCreated: 2023-02-03T19:17:22.854Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot and Spring Cloud for Distributed Systems***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-spring-cloud-for-distributed-systems)
{.links-list}


# 用于分布式系统的 Spring Boot 和 Spring Cloud

云已成为许多企业和组织的新常态。它具有成本效益、可扩展性，并提供许多其他好处。但它也可能很复杂，有很多活动部件。

使在云上开发分布式系统更容易的一种方法是使用 Spring Boot 和 Spring Cloud。在本文中，我们将了解这两个框架是什么以及它们如何一起使用。

## 什么是 Spring Boot？

Spring Boot 是一个框架，可帮助您创建独立的、生产级的基于 Spring 的应用程序。它旨在让您以最少的配置尽快启动和运行。

Spring Boot 具有许多特性，包括：

- 嵌入式服务器，可以轻松部署您的应用程序
- 支持许多不同的数据源
- 大量starter依赖，可以用最少的配置为你的项目添加常用依赖
- Spring bean的自动配置
- 自以为是但灵活的配置

Spring Boot 使创建 Spring 驱动的应用程序和服务变得容易。它采用 Spring 平台的自以为是的观点，让您以最少的配置启动和运行。

## 什么是Spring Cloud？

Spring Cloud 是一组用于构建云原生应用程序的工具。它提供了许多功能，包括：

- 服务发现：一种注册和发现服务的机制
- 配置管理：分布式配置服务
- 路由：一种反向代理服务，用于将请求路由到后端服务
- 负载均衡：客户端负载均衡库
- 断路器：用于管理分布式系统故障的库

Spring Cloud 帮助您构建可扩展、有弹性和自我管理的云原生应用程序。

## 一起使用 Spring Boot 和 Spring Cloud

Spring Boot 和 Spring Cloud 可以很好地协同工作。 Spring Boot 可以轻松创建独立的、生产级的基于 Spring 的应用程序，而 Spring Cloud 可以轻松构建和部署微服务。

这是一个使用 Spring Boot 和 Spring Cloud 构建的微服务的简单示例。

```java
@SpringBootApplication
@EnableDiscoveryClient
public class MyService {
    
    @Autowired
    private DiscoveryClient discoveryClient;
    
    @RequestMapping("/")
    public String home() {
        return "Hello from MyService";
    }
    
    @RequestMapping("/service-instances/{applicationName}")
    public List<ServiceInstance> serviceInstancesByApplicationName(
        @PathVariable String applicationName) {
        return this.discoveryClient.getInstances(applicationName);
    }
}
```

这个微服务向 Spring Cloud DiscoveryClient 注册自己，这允许它被其他服务发现。它还公开了两个 REST 端点：一个用于返回简单的问候语，另一个用于返回给定应用程序名称的 ServiceInstances 列表。

要运行此微服务，您可以使用 Spring Boot Maven 插件：

```
$ mvn spring-boot:run
```

然后，您可以通过 http://localhost:8080 访问该微服务。

## 结论

在本文中，我们了解了 Spring Boot 和 Spring Cloud 是什么以及它们如何一起使用。我们还看到了一个使用这两个框架构建的微服务的简单示例。

如果您正在寻找一种方法来简化在云上开发分布式系统，那么 Spring Boot 和 Spring Cloud 值得一试。