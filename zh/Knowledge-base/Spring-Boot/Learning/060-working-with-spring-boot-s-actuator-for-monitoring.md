---
title: 060：使用 Spring Boot 的执行器进行监控
description: 
published: true
date: 2023-02-04T23:32:25.075Z
tags: 
editor: markdown
dateCreated: 2023-02-04T23:32:23.530Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [060: Working with Spring Boot's Actuator for Monitoring***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/060-working-with-spring-boot-s-actuator-for-monitoring)
{.links-list}


# 用于监控的 Spring Boot 执行器

Spring Boot 的 Actuator 是监控和管理 Spring Boot 应用程序的绝佳工具。在这篇文章中，我们将了解如何使用 Actuator 来监控应用程序的运行状况和性能。

## 什么是执行器？

Actuator 是一个 Spring Boot 模块，它提供生产就绪的功能来帮助您监控和管理您的应用程序。使用 Actuator，您可以监控应用程序的运行状况、性能，甚至可以创建自定义端点以获取有关应用程序状态的信息。

## 如何使用执行器？

要在您的 Spring Boot 应用程序中使用 Actuator，您需要将以下依赖项添加到您的 `pom.xml`：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

添加依赖项后，您可以开始使用 Actuator 的功能。

## 监控应用程序的健康状况

Actuator 最重要的特性之一是它能够监控应用程序的健康状况。默认情况下，Actuator 公开一个 `/health` 端点，您可以使用它来检查应用程序的健康状况。

`/health` 端点返回一个 `status` 属性，该属性可以具有以下值之一：

- `UP`：应用程序已启动并正在运行。
- `DOWN`：应用程序已关闭。
- `OUT_OF_SERVICE`：应用程序停止服务。

`/health` 端点还返回一个 `details` 属性，其中包含有关应用程序健康状况的更多信息。例如，“详细信息”属性可能包含有关应用程序的数据库连接或当前正在运行的线程数的信息。

除了“/health”端点之外，Actuator 还公开了一个“/info”端点，您可以使用它来获取有关应用程序的信息。 `/info` 端点返回一个 `build` 属性，其中包含有关应用程序构建的信息，例如版本号和构建时间戳。

## 监控应用程序的性能

除了监控应用程序的健康状况之外，Actuator 还可以帮助您监控应用程序的性能。 Actuator 公开了许多与性能相关的端点，例如 `/metrics`、`/dump` 和 `/trace`。

`/metrics` 端点返回许多与性能相关的指标，例如已处理的请求数、平均响应时间和发生的错误数。

`/dump` 端点返回应用程序的线程转储，这对于调试目的很有用。

`/trace` 端点返回应用程序的跟踪，这对于理解应用程序的流程很有用。

## 创建自定义端点

除了内置端点，Actuator 还允许您创建自定义端点。要创建自定义端点，您需要创建一个实现“端点”接口的类。

例如，以下类创建一个自定义的“/myendpoint”端点，它返回一个“message”属性：

```java
@Component
public class MyEndpoint implements Endpoint<Map<String, String>> {

    @Override
    public String getId() {
        return "/myendpoint";
    }

    @Override
    public Map<String, String> invoke() {
        Map<String, String> result = new HashMap<>();
        result.put("message", "Hello, world!");
        return result;
    }

    @Override
    public boolean isSensitive() {
        return false;
    }

}
```

## 结论

在这篇文章中，我们研究了如何使用 Spring Boot 的 Actuator 来监控您的应用程序。 Actuator 是监控应用程序运行状况和性能的绝佳工具。此外，Actuator 允许您创建自定义端点以获取有关您的应用程序的信息。