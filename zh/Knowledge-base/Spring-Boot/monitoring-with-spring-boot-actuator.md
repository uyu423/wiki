---
title: 使用 Spring Boot Actuator 进行监控
description: 
published: true
date: 2023-02-07T01:32:46.884Z
tags: 
editor: markdown
dateCreated: 2023-02-07T01:32:45.194Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Monitoring with Spring Boot Actuator***English** document is available*](/en/Knowledge-base/Spring-Boot/monitoring-with-spring-boot-actuator)
{.links-list}



# 使用 Spring Boot Actuator 进行监控

Spring Boot Actuator 是 Spring Boot 框架的一个子项目，它提供生产就绪的功能来帮助您监控和管理您的应用程序。它还可以帮助您审核有关您的应用程序的健康信息。默认情况下不启用 Spring Boot Actuator。您需要使用“@EnableAutoConfiguration”或“@SpringBootApplication”注释来启用它。

## 启用 Spring Boot 执行器

要在您的 Spring Boot 应用程序中启用 Spring Boot Actuator，您需要将 `spring-boot-starter-actuator` 依赖项添加到您的 `pom.xml` 文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

您还可以通过将以下属性添加到您的 application.properties 文件来在您的应用程序中启用 Spring Boot Actuator：

```properties
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always
```

## 使用 Spring Boot Actuator 进行监控

Spring Boot Actuator 提供了许多生产就绪的端点，您可以使用它们来监视和管理您的应用程序。下表列出了最重要的端点：

|端点 |说明 |
| --- | --- |
| `/健康` |显示应用程序健康信息（默认为“UP”）。 |
| `/信息` |显示任意应用程序信息。 |
| `/指标` |显示应用程序指标信息。 |
| `/追踪` |显示应用程序跟踪信息。 |
| `/转储` |执行线程转储。 |
| `/约洛基亚` |通过 HTTP 公开 JMX bean（需要 `jolokia-core`）。 |
| `/日志文件` |返回日志文件的内容（如果配置了日志记录）。 |
| `/刷新` |刷新应用程序和配置缓存。 |
| `/飞行路线` |显示已应用的任何 Flyway 数据库迁移。 |
| `/liquibase` |显示已应用的任何 Liquibase 数据库迁移。 |

默认情况下，“/health”和“/info”端点是安全的。要使它们可公开访问，您需要将以下属性添加到您的“application.properties”文件中：

```properties
management.security.enabled=false
```

## 自定义 Spring Boot 执行器

Spring Boot Actuator 提供了多种方式来自定义其行为。

### 更改管理服务器端口

默认情况下，Spring Boot Actuator 使用端口 8080 作为管理服务器。您可以通过将以下属性添加到“application.properties”文件来更改此设置：

```properties
management.server.port=<port>
```

### 更改管理服务器路径

默认情况下，Spring Boot Actuator 使用 `/actuator` 路径作为管理服务器。您可以通过将以下属性添加到“application.properties”文件来更改此设置：

```properties
management.server.servlet.path=/<path>
```

### 更改端点 ID

默认情况下，Spring Boot Actuator 使用上表中的端点 ID。您可以通过将以下属性添加到“application.properties”文件来更改这些设置：

```properties
management.endpoints.web.exposure.include=<endpoint1>,<endpoint2>,...
```

### 更改端点路径

默认情况下，Spring Boot Actuator 使用上表中的端点路径。您可以通过将以下属性添加到“application.properties”文件来更改这些设置：

```properties
management.endpoint.<endpoint>.path=/<path>
```

### 更改端点敏感信息

默认情况下，Spring Boot Actuator 在端点响应主体中公开敏感信息。您可以通过将以下属性添加到“application.properties”文件来更改此设置：

```properties
management.endpoint.health.show-details=<value>
```

其中 `<value>` 可以是以下之一：

|价值 |说明 |
| --- | --- |
| `总是` |始终显示细节。 |
| `从不` |从不显示细节。 |
| `when_authorized` |在用户获得授权时显示详细信息。 |

### 更改端点安全性

默认情况下，Spring Boot Actuator 对端点使用 HTTP 基本身份验证。您可以通过将以下属性添加到“application.properties”文件来更改此设置：

```properties
management.security.enabled=false
```

### 更改端点用户名和密码

默认情况下，Spring Boot Actuator 使用用户名“user”和密码“password”作为端点。您可以通过将以下属性添加到“application.properties”文件来更改这些设置：

```properties
management.security.user.name=<username>
management.security.user.password=<password>
```

## 结论

在本文中，我们了解了如何使用 Spring Boot Actuator 来监视和管理您的应用程序。我们还了解了如何自定义执行器的行为。