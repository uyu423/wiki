---
title: Spring Boot 与 MongoDB
description: 
published: true
date: 2023-02-07T10:32:36.674Z
tags: 
editor: markdown
dateCreated: 2023-02-07T10:32:34.919Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot with MongoDB***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-with-mongodb)
{.links-list}


# Spring Boot 与 MongoDB

Spring Boot 是一种流行的基于 Java 的框架，用于构建微服务。它提供了一种简单的方法来创建独立的、生产级的基于 Spring 的应用程序，您可以“直接运行”。

 MongoDB 是一个使用面向文档的数据模型的开源 NoSQL 数据库。它是数据管理和分析的强大工具。

在本文中，我们将向您展示如何连接 Spring Boot 和 MongoDB。

## 先决条件

要阅读本文，您需要具备以下条件：

- Java 8 或更高版本
- Spring Boot 2.0 或更高版本
- MongoDB 3.6 或更高版本

## 创建一个 Spring Boot 项目

我们将使用 Spring Initializr 来生成我们的 Spring Boot 项目。

转到 http://start.spring.io/，然后选择以下内容：

- 项目：Maven 项目
- 语言：Java
- 弹簧引导：2.0.3
- 组：com.example
- 神器：演示

单击 **生成项目**。

## 配置 MongoDB

Spring Boot 将在 `src/main/resources` 目录中查找名为 `application.properties`（或 `application.yml`）的文件。这是我们将配置 MongoDB 连接的地方。

将以下内容添加到您的“application.properties”文件中：

```
spring.data.mongodb.uri=mongodb://localhost/test
```

这将连接到 `localhost` 上名为 `test` 的 MongoDB 数据库。

如果您使用的是 application.yml，配置将如下所示：

```yaml
spring:
  data:
    mongodb:
      uri: mongodb://localhost/test
```

## 创建 MongoDB 存储库

接下来，我们将为我们的 MongoDB 数据库创建一个存储库接口。这将扩展 Spring Data MongoDB 提供的 `MongoRepository` 接口。

```java
package com.example.demo.repository;

import org.springframework.data.mongodb.repository.MongoRepository;

import com.example.demo.model.User;

public interface UserRepository extends MongoRepository<User, String> {

}
```

`UserRepository` 接口将对 MongoDB 中的 `User` 集合执行 CRUD 操作。

## 创建一个 MongoDB 模型

现在我们将创建一个 User 类来表示 User 集合中的文档。

```java
package com.example.demo.model;

import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;

@Document
public class User {

    @Id
    private String id;

    private String name;
    private int age;

    // Getters and setters
}
```

`@Document` 注释告诉 Spring Data MongoDB `User` 类是 `User` 集合中的文档。

`@Id` 注释将 `id` 字段标记为文档的主键。

## 创建一个 REST 控制器

现在我们将创建一个 REST 控制器来将我们的 MongoDB 存储库公开为 REST API。

```java
package com.example.demo.controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

import com.example.demo.model.User;
import com.example.demo.repository.UserRepository;

@RestController
@RequestMapping("/api/v1/users")
public class UserController {

    @Autowired
    private UserRepository userRepository;

    @RequestMapping(method = RequestMethod.GET)
    public List<User> getUsers() {
        return userRepository.findAll();
    }
}
```

`@RestController` 注释将 `UserController` 类标记为 REST 控制器。

@RequestMapping 注释将 HTTP 请求映射到控制器中的方法。在这种情况下，`/api/v1/users` 路径被映射到 `getUsers()` 方法。

`@Autowired` 注释将 `UserRepository` 注入到控制器中。

`getUsers()` 方法从 MongoDB 数据库中检索用户列表并将其作为 JSON 返回。

## 运行应用程序

要运行该应用程序，只需在您的终端中键入以下命令：

```
./mvnw spring-boot:run
```

您应该看到以下输出：

```
...
2017-12-01 10:21:59.593  INFO 85511 --- [           main] s.b.c.e.t.TomcatEmbeddedServletContainer : Tomcat started on port(s): 8080 (http)
2017-12-01 10:21:59.596  INFO 85511 --- [           main] com.example.demo.DemoApplication         : Started DemoApplication in 4.166 seconds (JVM running for 4.681)
```

您现在可以在 http://localhost:8080/api/v1/users 访问 REST API。

## 结论

在本文中，我们向您展示了如何将 Spring Boot 与 MongoDB 连接起来。我们还为 MongoDB 数据库上的 CRUD 操作创建了一个简单的 REST API。

有关 Spring Boot 的更多信息，请参阅以下资源：

- [Spring Boot 文档](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/)
- [使用 MongoDB 的 Spring Boot 教程](https://www.baeldung.com/spring-boot-mongodb)

有关 MongoDB 的更多信息，请参阅以下资源：

- [MongoDB 文档](https://docs.mongodb.com/)
- [MongoDB 大学](https://university.mongodb.com/)