---
title: 011：使用 Actuator 监控和管理 Spring Boot 应用程序
description: 
published: true
date: 2023-02-03T09:04:41.913Z
tags: 
editor: markdown
dateCreated: 2023-02-03T09:04:36.916Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [011: Monitoring and managing a Spring Boot application with Actuator***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/011-monitoring-and-managing-a-spring-boot-application-with-actuator)
{.links-list}


# 使用 Actuator 监控和管理 Spring Boot 应用程序

Actuator 是一个可用于监控和管理 Spring Boot 应用程序的工具。它提供了许多可用于监视和管理应用程序的功能，包括：

- 健康检查
- 指标
- 记录
- 配置
- 端点

在这篇文章中，我们将重点介绍如何使用 Actuator 来监控和管理 Spring Boot 应用程序。我们将首先了解如何在 Spring Boot 应用程序中配置 Actuator。然后，我们将了解如何使用 Actuator 的健康检查功能来监控应用程序的健康状况。最后，我们将了解如何使用 Actuator 的指标功能来监控应用程序的性能。

## 在 Spring Boot 应用程序中配置执行器

在 Spring Boot 应用程序中默认情况下不启用执行器。要启用 Actuator，我们需要将以下依赖项添加到我们的项目中：

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

添加依赖项后，我们可以通过将以下属性添加到我们的 application.properties 文件来启用 Actuator：

```
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always
```

第一个属性 management.endpoints.web.exposure.include 公开了所有执行器端点。第二个属性 management.endpoint.health.show-details 确保健康检查端点包含有关我们应用程序健康状况的详细信息。

## 使用执行器的健康检查功能

执行器的健康检查功能可用于监控我们应用程序的健康状况。默认情况下，Actuator 提供了许多内置的健康检查，包括对数据库、磁盘空间和 JMS 的检查。

除了内置的健康检查，我们还可以添加自己的自定义健康检查。要添加自定义健康检查，我们需要创建一个实现 HealthIndicator 接口的类。例如，以下类为我们称为 MyService 的服务实施健康检查：

```java
public class MyServiceHealthIndicator implements HealthIndicator {

   @Override
   public Health health() {
      // check the health of our service
      // if the service is healthy, return a Health.Builder with a status of UP
      // if the service is not healthy, return a Health.Builder with a status of DOWN
   }
}
```

一旦我们创建了自定义健康检查，我们需要在 Spring 中注册它。我们可以通过在我们的类中添加 @Component 注释来做到这一点。例如：

```java
@Component
public class MyServiceHealthIndicator implements HealthIndicator {

   @Override
   public Health health() {
      // check the health of our service
      // if the service is healthy, return a Health.Builder with a status of UP
      // if the service is not healthy, return a Health.Builder with a status of DOWN
   }
}
```

## 使用执行器的指标功能

Actuator 的指标功能可用于监控我们应用程序的性能。默认情况下，Actuator 提供了许多内置指标，包括数据库、JMS 和 Web 请求的指标。

除了内置指标外，我们还可以添加自己的自定义指标。要添加自定义指标，我们需要创建一个实现 MetricWriter 接口的类。例如，以下类为我们称为 MyService 的服务实现了一个指标：

```java
public class MyServiceMetricWriter implements MetricWriter {

   @Override
   public void write(Metric<?> metric) {
      // write the metric to our monitoring system
   }
}
```

一旦我们创建了自定义指标，我们就需要在 Spring 中注册它。我们可以通过在我们的类中添加 @Component 注释来做到这一点。例如：

```java
@Component
public class MyServiceMetricWriter implements MetricWriter {

   @Override
   public void write(Metric<?> metric) {
      // write the metric to our monitoring system
   }
}
```

## 结论

在本文中，我们了解了如何使用 Actuator 来监控和管理 Spring Boot 应用程序。我们已经了解了如何在 Spring Boot 应用程序中配置 Actuator，以及如何使用 Actuator 的健康检查和指标功能来监控应用程序的健康状况和性能。