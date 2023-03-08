---
title: 041：将 Spring Boot 与 Apache Storm 结合使用
description: 
published: true
date: 2023-02-04T07:32:19.496Z
tags: 
editor: markdown
dateCreated: 2023-02-04T07:32:17.926Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [041: Using Spring Boot with Apache Storm***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/041-using-spring-boot-with-apache-storm)
{.links-list}


# 将 Spring Boot 与 Apache Storm 结合使用

在本文中，我们将学习如何将 Spring Boot 与 Apache Storm 结合使用。我们将涵盖以下主题：

* 什么是 Apache Storm？
* 什么是Spring Boot？
* 如何在 Apache Storm 中使用 Spring Boot

## 什么是 Apache 风暴？

Apache Storm 是一个免费开源的分布式实时计算系统。 Storm 使可靠地处理无限制的数据流变得容易，实时处理就像 Hadoop 批处理一样。

Storm 很简单，可以与任何编程语言一起使用，而且使用起来很有趣！

## 什么是 Spring Boot？

Spring Boot 是一个框架，用于轻松创建独立的、生产级的基于 Spring 的应用程序，您可以“直接运行”。我们对 Spring 平台和第三方库有自己的看法，因此您可以轻松上手。大多数 Spring Boot 应用程序需要很少的 Spring 配置。

## 如何在 Apache Storm 中使用 Spring Boot

现在我们知道了 Storm 和 Spring Boot 是什么，让我们看看如何一起使用它们。

我们首先需要的是 Storm 的 Maven 依赖项：

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>1.1.1</version>
    <scope>provided</scope>
</dependency>
```

我们还需要 Spring Boot 的依赖项：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

现在我们可以创建一个 Spring Boot 应用程序：

```java
@SpringBootApplication
public class StormApplication {

    public static void main(String[] args) {
        SpringApplication.run(StormApplication.class, args);
    }

}
```

我们现在可以在我们的应用程序中创建一个 Storm 拓扑：

```java
@Component
public class MyTopology {

    @Autowired
    private TopologyBuilder topologyBuilder;

    @PostConstruct
    public void init() {
        // ...
    }

}
```

就是这样！现在，我们的 Spring Boot 应用程序中有了一个可用的 Storm 拓扑。

## 附加信息

* 有关 Apache Storm 的更多信息，请参阅 [Apache Storm 网站](https://storm.apache.org/)。
* 有关 Spring Boot 的更多信息，请参阅 [Spring Boot 网站](https://projects.spring.io/spring-boot/)。