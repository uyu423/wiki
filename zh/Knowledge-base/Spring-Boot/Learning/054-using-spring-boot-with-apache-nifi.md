---
title: 054：将 Spring Boot 与 Apache Nifi 结合使用
description: 
published: true
date: 2023-02-03T01:23:38.943Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:23:37.386Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [054: Using Spring Boot with Apache Nifi***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/054-using-spring-boot-with-apache-nifi)
{.links-list}


# 将 Spring Boot 与 Apache Nifi 结合使用

Spring Boot 是一种流行的基于 Java 的框架，用于创建微服务。 Apache NiFi 是一个强大的数据流工具，可用于处理和路由数据。

在本文中，我们将展示如何将 Spring Boot 与 Apache NiFi 结合使用。我们将涵盖以下主题：

* 设置 Spring Boot 项目
* 配置 Apache NiFi
* 创建 Spring Boot 服务
* 测试数据流

## 设置 Spring Boot 项目

我们需要做的第一件事是创建一个新的 Spring Boot 项目。我们可以使用 [Spring Initializr](https://start.spring.io/) 生成具有必要依赖项的项目。

对于此示例，我们需要以下依赖项：

* Web - 用于创建 Web 应用程序
* H2 - 用于内存数据库

一旦我们设置了项目，我们就可以开始配置 Apache NiFi。

## 配置 Apache NiFi

Apache NiFi 需要配置为使用我们将要创建的 Spring Boot 服务。我们需要将以下内容添加到 NiFi 配置中：

* 调用 Spring Boot 服务的 Processor
* 处理器的连接池
* 连接池的控制器服务

我们可以使用 NiFi GUI 来配置这些设置。首先，我们将添加处理器：

![添加处理器](https://i.imgur.com/Lb6qyFW.png)

接下来，我们将添加连接池：

![添加连接池](https://i.imgur.com/vH8X3zJ.png)

最后，我们将添加控制器服务：

![添加控制器服务](https://i.imgur.com/g4SVfyi.png)

## 创建 Spring Boot 服务

现在我们已经配置了 Apache NiFi，我们可以创建 Spring Boot 服务。该服务将是一个公开 REST 端点的简单 Web 应用程序。

端点将采用 JSON 负载并返回响应。响应将是具有生成的 ID 的相同 JSON 负载。

这是该服务的代码：

```java
@RestController
public class DataController {

    @PostMapping("/data")
    public ResponseEntity<String> data(@RequestBody String data) {
        // Generate ID
        String id = UUID.randomUUID().toString();
        // Return response
        return ResponseEntity.ok().body(id);
    }
}
```

## 测试数据流

现在我们已经启动并运行了服务，我们可以测试数据流了。我们将使用 NiFi GUI 将 JSON 负载发送到端点。

首先，我们将创建一个新的 FlowFile：

![创建流文件](https://i.imgur.com/TGiukC5.png)

接下来，我们将添加 JSON 负载：

![添加 JSON 负载](https://i.imgur.com/l0v4tqO.png)

最后，我们将触发处理器并检查响应：

![触发处理器](https://i.imgur.com/JY4fZUO.png)

![检查响应](https://i.imgur.com/5AFw8gG.png)

正如我们所见，响应包含生成的 ID。

## 结论

在本文中，我们展示了如何将 Spring Boot 与 Apache NiFi 结合使用。我们设置了一个简单的数据流来调用 Spring Boot 服务并返回响应。

如果您有兴趣了解有关 NiFi 的更多信息，请务必查看 [官方文档](https://nifi.apache.org/docs.html)。