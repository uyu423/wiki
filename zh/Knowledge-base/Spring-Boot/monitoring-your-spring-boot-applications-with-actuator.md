---
title: 使用 Actuator 监控您的 Spring Boot 应用程序
description: 
published: true
date: 2023-02-17T18:02:46.366Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:16:13.706Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Monitoring Your Spring Boot Applications with Actuator***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/monitoring-your-spring-boot-applications-with-actuator)
{.links-list}


# 使用 Actuator 监控您的 Spring Boot 应用程序

监控是任何应用程序的一个关键方面，Spring Boot 提供了一种使用 Actuator 监控应用程序的简单方法。 Actuator 是一个 Spring Boot 模块，提供各种监控和管理端点。在本文中，我们将了解如何使用 Actuator 来监控您的 Spring Boot 应用程序。

## 启用执行器端点

要使用 Actuator，您需要将 spring-boot-actuator 依赖项添加到您的项目中。您可以将此依赖项添加到您的 `pom.xml` 文件中：

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-actuator</artifactId>
  <version>2.1.2.RELEASE</version>
</dependency>
```

添加依赖项后，您可以通过将“@EnableActuator”注释添加到“@SpringBootApplication”类来启用执行器端点：

```java
@SpringBootApplication
@EnableActuator
public class Application {

  public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
  }
}
```

## 监控您的应用程序

启用 Actuator 后，您可以通过导航到“http://localhost:8080/{context-path}/actuator”来访问 Actuator 端点。 `{context-path}` 是您的应用程序的上下文路径。例如，如果您的应用程序在“http://localhost:8080/my-app”上运行，您可以在“http://localhost:8080/my-app/actuator”访问执行器端点。

执行器端点使您能够以多种方式监控您的应用程序。例如，您可以监控应用程序的运行状况、指标数据、配置等。

### 监控应用程序运行状况

`health` 端点提供有关应用程序健康状况的信息。要访问“health”端点，请导航至“http://localhost:8080/{context-path}/actuator/health”。

`health` 端点以 JSON 格式返回有关应用程序健康状况的信息。 JSON 格式包含以下信息：

- `status`：应用程序的状态。可能的值为“UP”或“DOWN”。
- `details`：应用程序的健康细节。运行状况详细信息包含有关应用程序各个组件的信息。

以下是一个“健康”端点响应示例：

```json
{
  "status": "UP",
  "details": {
    "diskSpace": {
      "status": "UP",
      "details": {
        "total":49989655552,
        "free":3246466048,
        "threshold":10485760
      }
    }
  }
}
```

### 监控应用指标

`metrics` 端点提供有关应用程序指标的信息。要访问 `metrics` 端点，请导航至 `http://localhost:8080/{context-path}/actuator/metrics`。

`metrics` 端点以 JSON 格式返回有关应用程序指标的信息。 JSON 格式包含以下信息：

- `names`：指标的名称。
- `values`：指标的值。

以下是一个示例“指标”端点响应：

```json
{
  "names": [
    "jvm.memory.max",
    "jvm.memory.used"
  ],
  "values": {
    "jvm.memory.max":49989655552,
    "jvm.memory.used":3246466048
  }
}
```

### 监控应用程序配置

`configprops` 端点提供有关应用程序配置属性的信息。要访问 `configprops` 端点，请导航至 `http://localhost:8080/{context-path}/actuator/configprops`。

`configprops` 端点以 JSON 格式返回有关应用程序配置属性的信息。 JSON 格式包含以下信息：

- `propertySources`：应用程序的属性来源。

以下是 `configprops` 端点响应示例：

```json
{
  "propertySources": [
    {
      "name": "application.properties",
      "properties": {
        "server.port": "8080",
        "spring.application.name": "demo"
      }
    },
    {
      "name": "systemProperties",
      "properties": {
        "java.runtime.name": "OpenJDK Runtime Environment",
        "sun.boot.library.path": "/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.131-3.b12.el7_3.x86_64/jre/lib/boot",
        ...
      }
    },
    ...
  ]
}
```

## 结论

在本文中，我们了解了如何使用 Actuator 来监控您的 Spring Boot 应用程序。 Actuator 提供了一种简单而强大的方法来监控您的应用程序。通过使用 Actuator 端点，您可以获得有关应用程序的运行状况、指标和配置的详细信息。