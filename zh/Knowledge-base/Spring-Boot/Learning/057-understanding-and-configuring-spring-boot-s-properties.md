---
title: 057：了解和配置 Spring Boot 的属性
description: 
published: true
date: 2023-02-04T20:32:18.759Z
tags: 
editor: markdown
dateCreated: 2023-02-04T20:32:17.135Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [057: Understanding and Configuring Spring Boot's Properties***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/057-understanding-and-configuring-spring-boot-s-properties)
{.links-list}


# Spring Boot 属性

在本文中，我们将了解 Spring Boot 属性。我们将了解它们是什么、如何配置它们以及如何使用它们来自定义 Spring Boot 应用程序的行为。

## 什么是 Spring Boot 属性？

Spring Boot 属性用于配置 Spring Boot 应用程序。它们可用于为各种 Spring Boot 设置设置值，例如应用程序名称、服务器端口等。

可以通过多种方式配置属性，例如在属性文件中、通过环境变量或以编程方式。

## 如何配置 Spring Boot 属性

可以通过多种方式配置 Spring Boot 属性。

最常见的方法是使用属性文件。 Spring Boot 将在类路径中查找名为“application.properties”的文件。该文件可用于覆盖任何默认的 Spring Boot 属性。

例如，以下“application.properties”文件会将服务器端口设置为 8080：

```
server.port=8080
```

配置 Spring Boot 属性的另一种方法是通过环境变量。 Spring Boot 将查找以 `spring.` 开头的环境变量，并使用它们来覆盖任何相应的属性。

例如，以下环境变量会将服务器端口设置为 8080：

```
spring.server.port=8080
```

最后，还可以通过编程方式配置 Spring Boot 属性。这可以通过创建一个“@Configuration”类并使用“@ConfigurationProperties”注释来完成。

例如，以下“@Configuration”类会将“server.port”属性映射到“serverPort”字段：

```java
@Configuration
@ConfigurationProperties(prefix="server")
public class ServerConfig {

    private int port;

    public int getPort() {
        return port;
    }

    public void setPort(int port) {
        this.port = port;
    }

}
```

## 自定义 Spring Boot 应用程序

Spring Boot 属性可用于自定义 Spring Boot 应用程序的行为。

例如，`spring.main.banner-mode` 属性可用于禁用 Spring Boot 横幅：

```
spring.main.banner-mode=off
```

`spring.jpa.show-sql` 属性可用于为 JPA 启用 SQL 日志记录：

```
spring.jpa.show-sql=true
```

`spring.thymeleaf.cache` 属性可用于启用 Thymeleaf 模板缓存：

```
spring.thymeleaf.cache=true
```

等等。

## 结论

在本文中，我们了解了 Spring Boot 属性。我们已经了解了如何配置它们，如何使用它们来自定义 Spring Boot 应用程序的行为，以及在哪里可以找到有关它们的更多信息。