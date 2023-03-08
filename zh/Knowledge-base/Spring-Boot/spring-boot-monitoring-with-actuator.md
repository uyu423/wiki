---
title: 使用 Actuator 进行 Spring Boot 监控
description: 
published: true
date: 2023-02-07T15:33:16.602Z
tags: 
editor: markdown
dateCreated: 2023-02-07T15:33:14.974Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot Monitoring with Actuator***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-monitoring-with-actuator)
{.links-list}


# 使用 Actuator 进行 Spring Boot 监控

在生产 Spring Boot 应用程序中，能够监控应用程序以识别和诊断可能出现的任何问题非常重要。 Spring Boot 提供了许多开箱即用的功能来帮助解决这个问题，包括 Actuator。

Actuator 是一种允许您监视和管理 Spring Boot 应用程序的工具。它提供了许多端点，使您无需编写任何代码即可监视和管理您的应用程序。

在本文中，我们将了解如何使用 Actuator 来监控 Spring Boot 应用程序。我们还将了解如何使用 Actuator 创建自定义端点以公开特定于应用程序的信息。

## 启用执行器

要使用 Actuator，首先需要在项目中添加 spring-boot-starter-actuator 依赖。这可以通过将以下依赖项添加到 pom.xml 文件来完成：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

或者，如果您使用的是 Gradle，则可以将以下依赖项添加到您的 build.gradle 文件中：

```groovy
dependencies {
    compile('org.springframework.boot:spring-boot-starter-actuator')
}
```

一旦您将 spring-boot-starter-actuator 依赖项添加到您的项目中，Actuator 将默认启用。默认情况下，只有具有“ADMIN”角色的用户才能访问执行器。

要更改此设置，您可以将以下属性添加到您的 application.properties 文件中：

```properties
management.security.enabled=false
```

这将禁用执行器端点的安全性。或者，您可以将 spring-boot-starter-security 依赖项添加到项目中，以配置 Actuator 端点的安全性。

## 执行器端点

Actuator 公开了许多端点。这些端点可用于监视和管理您的应用程序。端点分为两组：

* productionEndpoints：这些端点旨在用于生产，并提供有关应用程序健康和状态的信息。
* allEndpoints：这些端点提供有关应用程序的健康和状态的信息，以及特定于应用程序的信息。

allEndpoints 组包括所有 productionEndpoints，以及您创建的任何自定义端点。

下表列出了 Actuator 提供的 productionEndpoints：

|端点 |说明 |
| --- | --- |
| /审计事件|此端点提供有关已审核的应用程序事件的信息。 |
| /豆子 |此端点提供有关已由 Spring 容器创建的 bean 的信息。 |
| /配置道具 |此端点提供有关已为您的应用程序设置的配置属性的信息。 |
| /转储 |此端点可用于转储应用程序的状态。这对于故障排除很有用。 |
| /环境 |此端点提供有关已为您的应用程序设置的环境变量的信息。 |
| /飞路 |此端点提供有关 Flyway 应用的数据库迁移的信息。 |
| /健康 |此端点提供有关应用程序运行状况的信息。 |
| /信息 |此端点提供特定于应用程序的信息。 |
| /液基 |此端点提供有关 Liquibase 应用的数据库迁移的信息。 |
| /记录器 |此端点可用于为您的应用程序配置日志记录级别。 |
| /指标 |此端点提供有关已为您的应用程序收集的指标的信息。 |
| /映射|此端点提供有关已为您的应用程序定义的 @RequestMapping 路径的信息。 |
| /关机|此端点可用于关闭您的应用程序。 |
| /跟踪 |此端点提供有关已向您的应用程序发出的 HTTP 请求的信息。 |

要访问这些端点中的任何一个，您需要将端点附加到应用程序的路径中。例如，如果您的应用程序在 http://localhost:8080 上运行，您将在 http://localhost:8080/health 访问 /health 端点。

## 读取执行器端点

要从 Actuator 端点读取信息，您可以使用 curl、wget 或浏览器等工具。

例如，要读取 /health 端点，您可以使用 curl 如下：

```
$ curl http://localhost:8080/health
```

或者，您可以按如下方式使用 wget：

```
$ wget http://localhost:8080/health
```

如果您使用浏览器访问 /health 端点，您将看到以下输出：

```json
{
    "status": "UP",
    "diskSpace": {
        "status": "UP",
        "total": 499963648,
        "free": 367030272,
        "threshold": 10485760
    },
    "db": {
        "status": "UP",
        "database": "H2",
        "hello": 1
    },
    "redis": {
        "status": "UP"
    }
}
```

/health 端点的输出是一个 JSON 文档，其中包含有关应用程序运行状况的信息。状态字段指示您的应用程序的整体健康状况。 diskSpace、db 和 redis 字段包含有关特定子系统健康状况的信息。

## 创建自定义端点

除了内置端点之外，您还可以创建自定义端点。为此，您需要创建一个实现 org.springframework.boot.actuate.endpoint.annotation.Endpoint 接口的类。

例如，以下类定义了一个返回用户列表的自定义端点：

```java
@Endpoint(id="users")
public class UserEndpoint {

    private List<User> users;

    @ReadOperation
    public List<User> getUsers() {
        return this.users;
    }

    public void setUsers(List<User> users) {
        this.users = users;
    }

}
```

@Endpoint 注解用于注解类。 id 属性用于指定端点的标识符。这是将用于访问端点的标识符。

getUsers() 方法使用@ReadOperation 注释进行注释。此注释表示该方法可用于从端点读取信息。

setUsers() 方法使用@WriteOperation 注释进行注释。此注释指示该方法可用于将信息写入端点。

要注册端点，您需要在类中添加@Component 注解。例如：

```java
@Component
@Endpoint(id="users")
public class UserEndpoint {
    // ...
}
```

或者，您可以通过将端点添加到应用程序上下文来注册端点。例如：

```java
@Configuration
public class EndpointConfig {

    @Bean
    public UserEndpoint userEndpoint() {
        return new UserEndpoint();
    }

}
```

注册端点后，您可以通过将端点标识符附加到应用程序的路径来访问它。例如，如果您的应用程序在 http://localhost:8080 上运行，您可以在 http://localhost:8080/users 访问 /users 端点。

## 结论

在本文中，我们了解了如何使用 Actuator 来监控 Spring Boot 应用程序。我们还研究了如何使用 Actuator 创建自定义端点以公开特定于应用程序的信息。