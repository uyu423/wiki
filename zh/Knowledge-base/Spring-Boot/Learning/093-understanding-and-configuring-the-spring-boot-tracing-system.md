---
title: 093：了解和配置 Spring Boot 跟踪系统
description: 
published: true
date: 2023-02-04T20:55:17.525Z
tags: 
editor: markdown
dateCreated: 2023-02-04T20:55:15.927Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [093: Understanding and Configuring the Spring Boot Tracing System***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/093-understanding-and-configuring-the-spring-boot-tracing-system)
{.links-list}


# 093：了解和配置 Spring Boot 跟踪系统

Spring Boot 提供了一个跟踪系统，可用于收集和查看有关流经系统的请求的信息。这对于调试目的或监视系统性能很有用。

在本文中，我们将了解如何配置 Spring Boot 跟踪系统，以及如何使用它来收集有关请求处理的信息。

## 配置 Spring Boot 跟踪系统

Spring Boot 跟踪系统是使用 application.properties 文件中的 spring.sleuth 属性配置的。以下属性可用于配置跟踪系统：

- `spring.sleuth.sampler.probability`：请求被采样的概率。默认值为 1.0，这意味着将对所有请求进行采样。

- `spring.sleuth.sampler.spans`：可以为单个请求创建的最大跨度数。默认值为 100。

- `spring.sleuth.trace-id128`：如果设置为 true，将生成 128 位跟踪 ID。默认值为假。

- `spring.sleuth.web.skip-pattern`：用于确定不应跟踪哪些请求的正则表达式。默认值为“/health”

有关这些属性的更多信息，请参阅 [Spring Boot 文档](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-tracing.html# boot-features-跟踪弹簧侦探）。

## 收集追踪信息

Spring Boot 跟踪系统可用于收集有关请求处理的信息。这些信息可以通过两种方式收集：

- 通过将信息记录到文件
- 通过将信息发送到 [Zipkin](https://zipkin.io/) 服务器

### 将跟踪信息记录到文件中

Spring Boot 跟踪系统可以配置为将跟踪信息记录到文件中。这可以通过在 application.properties 文件中设置 spring.sleuth.log.file 属性来完成。以下是如何配置跟踪系统以将信息记录到文件的示例：

```
spring.sleuth.log.file=traces.log
```

### 将跟踪信息发送到 Zipkin 服务器

Spring Boot 跟踪系统可以配置为将跟踪信息发送到 Zipkin 服务器。这可以通过在 application.properties 文件中设置 spring.sleuth.zipkin.baseUrl 属性来完成。以下是如何配置跟踪系统以将信息发送到 Zipkin 服务器的示例：

```
spring.sleuth.zipkin.baseUrl=http://localhost:9411
```

## 查看跟踪信息

### 将跟踪信息记录到文件中

如果跟踪系统配置为将信息记录到文件中，则可以通过在文本编辑器中打开文件来查看信息。信息将以 [JSON](https://www.json.org/) 格式记录。

### 将跟踪信息发送到 Zipkin 服务器

如果跟踪系统配置为向 Zipkin 服务器发送信息，则可以通过在 Web 浏览器中打开 Zipkin 服务器来查看信息。 Zipkin 服务器将提供一个图形界面来查看跟踪信息。

## 结论

在本文中，我们了解了如何配置 Spring Boot 跟踪系统，以及如何使用它来收集有关请求处理的信息。我们还了解了如何查看系统收集的跟踪信息。