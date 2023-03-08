---
title: 091：将 Spring Boot 与 Apache Zookeeper 集成以进行协调和同步
description: 
published: true
date: 2023-02-05T21:32:22.391Z
tags: 
editor: markdown
dateCreated: 2023-02-05T21:32:20.808Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [091: Integrating Spring Boot with Apache Zookeeper for Coordination and Synchronization***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/091-integrating-spring-boot-with-apache-zookeeper-for-coordination-and-synchronization)
{.links-list}


# 091：将 Spring Boot 与 Apache Zookeeper 集成以进行协调和同步

Apache Zookeeper 是分布式系统的分布式协调服务。它用于管理大型分布式系统。 Spring Boot 是用于开发微服务的流行 Java 框架。

在本文中，我们将学习如何将 Spring Boot 与 Apache Zookeeper 集成。我们将使用 Zookeeper 来协调和同步我们的 Spring Boot 微服务。

## 安装 Apache 动物园管理员

在开始使用 Zookeeper 之前，我们需要安装它。我们可以在 macOS 上使用 Homebrew 安装 Zookeeper：

```
$ brew install zookeeper
```

或者我们可以从 [Apache Zookeeper 网站](https://zookeeper.apache.org/) 下载 Zookeeper 二进制版本。

## 启动 Apache Zookeeper

安装 Zookeeper 后，我们可以使用以下命令启动它：

```
$ zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties
```

## 创建一个 Spring Boot 项目

我们可以使用 [Spring Initializr](https://start.spring.io/) 创建一个 Spring Boot 项目。我们将使用以下依赖项：

* 网络
* 执行器
*龙目岛

## 配置 Spring Boot

我们需要配置 Spring Boot 应用程序以使用 Zookeeper。我们可以通过将以下属性添加到我们的 application.properties 文件来做到这一点：

```properties
spring.cloud.zookeeper.connect-string=localhost:2181
spring.cloud.zookeeper.discovery.instance-id=${spring.application.name}
spring.cloud.zookeeper.discovery.root=/${spring.application.name}
spring.cloud.zookeeper.discovery.service-name=${spring.application.name}
spring.cloud.zookeeper.discovery.enabled=true
```

## 创建一个 Spring Boot 服务

我们可以使用“@SpringBootApplication”注解创建一个 Spring Boot 服务：

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## 添加一个休息控制器

我们可以使用 @RestController 注释向我们的服务添加一个 Rest 控制器：

```java
@RestController
public class GreetingController {

    @GetMapping("/greeting")
    public String greeting() {
        return "Hello, world!";
    }

}
```

## 测试服务

我们可以通过向 `/greeting` 端点发送 `GET` 请求来测试我们的服务：

```
$ curl localhost:8080/greeting
Hello, world!
```

## 向 Zookeeper 注册服务

一旦我们的服务启动并运行，我们需要向 Zookeeper 注册它。我们可以使用“@DiscoveryClient”注释来做到这一点：

```java
@SpringBootApplication
@DiscoveryClient
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## 从另一个服务访问服务

一旦我们的服务注册到 Zookeeper，我们就可以从另一个服务访问它。我们可以通过将“DiscoveryClient”注入我们的控制器来做到这一点：

```java
@RestController
public class GreetingController {

    @Autowired
    private DiscoveryClient discoveryClient;

    @GetMapping("/greeting")
    public String greeting() {
        List<ServiceInstance> instances = discoveryClient.getInstances("greeting-service");
        if (instances.isEmpty()) {
            return "Hello, world!";
        }
        String url = instances.get(0).getUri().toString();
        return "Hello, world! (from " + url + ")";
    }

}
```

## 结论

在本文中，我们学习了如何将 Spring Boot 与 Apache Zookeeper 集成。我们使用 Zookeeper 来协调和同步我们的 Spring Boot 微服务。