---
title: 使用 Spring Boot 构建 CRUD 应用程序
description: 
published: true
date: 2023-02-06T08:33:26.044Z
tags: 
editor: markdown
dateCreated: 2023-02-06T08:33:24.335Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Building a CRUD Application with Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/building-a-crud-application-with-spring-boot)
{.links-list}


# 使用 Spring Boot 构建 CRUD 应用程序

开发 CRUD（创建、读取、更新、删除）应用程序是构建 Web 应用程序时的常见要求。 Spring Boot 可以轻松创建独立的、生产级的基于 Spring 的应用程序，您可以“直接运行”。在本文中，我们将重点介绍如何使用 Spring Boot 创建 CRUD 应用程序。

## 什么是 Spring Boot？

Spring Boot 是一个基于 Java 的框架，用于创建独立的、生产级的基于 Spring 的应用程序。它采用了 Spring 平台和第三方库的自以为是的观点，因此您可以毫不费力地开始。大多数 Spring Boot 应用程序需要很少的 Spring 配置。

## 为什么要使用 Spring Boot？

SpringBoot 提供了许多功能，可以轻松开发 Web 应用程序。

- 可直接嵌入Tomcat、Jetty或Undertow（无需部署WAR文件）
- 它使用固执己见的配置方法
- 它减少了样板代码
- 它提供生产就绪的功能，例如指标、健康检查和外部化配置

## 入门

在本节中，我们将向您展示如何使用 Spring Boot 创建一个简单的 CRUD 应用程序。

### 先决条件

要继续阅读本文，您需要具备以下条件：

- Java 8 或更高版本
- Spring Boot 2.0 或更高版本
- 您选择的 IDE
- Maven 3.0 或更高版本

### 创建项目

首先，在您的 IDE 中创建一个 Maven 项目。确保选择“Spring Boot”启动项目和“web”模块。

![创建 Spring Boot 项目](https://i.imgur.com/5BkRJN4.png)

### 添加依赖

接下来，我们需要向我们的 `pom.xml` 文件添加一些依赖项。

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <scope>runtime</scope>
    </dependency>
</dependencies>
```

`spring-boot-starter-data-jpa` 依赖项会将 Spring Data 和 Hibernate 添加到我们的项目中。 `spring-boot-starter-web` 依赖项将添加 Spring MVC 和 Tomcat。最后，`postgresql` 依赖项将添加 PostgreSQL 驱动程序。

### 配置数据库

接下来，我们需要配置我们的数据库。在此示例中，我们将使用 PostgreSQL，但您可以使用任何您喜欢的数据库。

首先，在 `src/main/resources` 目录中创建一个名为 `application.properties` 的文件并添加以下行：

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=postgres
spring.datasource.password=postgres
spring.jpa.show-sql=true
```

这将配置我们的应用程序以连接到在端口 5432 上的本地主机上运行的 PostgreSQL 数据库。用户名和密码均为“postgres”。

### 创建实体

现在，我们需要创建一个实体类。实体是表示数据库表的 Java 类。在这个例子中，我们将创建一个 `User` 实体。

```java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;
    // ... getters and setters
}
```

@Entity 注释告诉 Hibernate 这个类是一个实体。 `@Id` 注释告诉 Hibernate `id` 字段是主键。 `@GeneratedValue` 注释告诉 Hibernate 为主键生成一个唯一值。

### 创建存储库

接下来，我们需要创建一个存储库接口。存储库是一个 Java 接口，它提供用于存储和检索数据的方法。在这个例子中，我们将创建一个 UserRepository 接口。

```java
public interface UserRepository extends CrudRepository<User, Long> {
}
```

`CrudRepository` 接口提供了 CRUD 操作的方法。我们将使用此接口来实现我们的“UserRepository”。

### 创建服务

现在，我们需要创建一个服务类。服务是包含业务逻辑的 Java 类。在这个例子中，我们将创建一个 `UserService` 类。

```java
@Service
public class UserService {
    private final UserRepository userRepository;
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
    public User createUser(User user) {
        return userRepository.save(user);
    }
    public User getUserById(Long id) {
        return userRepository.findById(id).orElseThrow(() -> new RuntimeException("User not found"));
    }
    public List<User> getAllUsers() {
        return userRepository.findAll();
    }
    public User updateUser(User user) {
        return userRepository.save(user);
    }
    public void deleteUserById(Long id) {
        userRepository.deleteById(id);
    }
}
```

`@Service` 注解告诉 Spring 这是一个服务 bean。 `UserService` 类包含用于创建、检索、更新和删除用户的方法。

### 创建控制器

接下来，我们需要创建一个控制器类。控制器是一个 Java 类，它包含处理 HTTP 请求的方法。在这个例子中，我们将创建一个 `UserController` 类。

```java
@RestController
@RequestMapping("/users")
public class UserController {
    private final UserService userService;
    public UserController(UserService userService) {
        this.userService = userService;
    }
    @PostMapping
    public User createUser(@RequestBody User user) {
        return userService.createUser(user);
    }
    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        return userService.getUserById(id);
    }
    @GetMapping
    public List<User> getAllUsers() {
        return userService.getAllUsers();
    }
    @PutMapping
    public User updateUser(@RequestBody User user) {
        return userService.updateUser(user);
    }
    @DeleteMapping("/{id}")
    public void deleteUserById(@PathVariable Long id) {
        userService.deleteUserById(id);
    }
}
```

`@RestController` 注释告诉 Spring 这是一个控制器 bean。 @RequestMapping 注释将 HTTP 请求映射到控制器方法。 `UserController` 类包含用于创建、检索、更新和删除用户的方法。

### 运行应用程序

现在我们已经配置了我们的应用程序，我们可以运行它了。要运行应用程序，只需执行 Application 类中的 main 方法即可。

```java
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

该应用程序将在端口 8080 上启动。

## 测试应用程序

现在我们的应用程序已启动并运行，让我们对其进行测试。我们可以使用 `curl` 向我们的应用程序发送 HTTP 请求。

### 创建用户

要创建用户，我们可以使用 POST 方法。

```
curl -X POST localhost:8080/users -d '{"name": "John Doe", "email": "john.doe@example.com"}' -H "Content-Type: application/json"
```

这将创建一个名为“John Doe”和电子邮件地址为“john.doe@example.com”的用户。

### 通过ID获取用户

要检索用户，我们可以使用“GET”方法。

```
curl localhost:8080/users/1
```

这将检索 ID 为“1”的用户。

### 获取所有用户

要检索所有用户，我们可以使用“GET”方法。

```
curl localhost:8080/users
```

这将检索所有用户。

### 更新用户

要更新用户，我们可以使用 PUT 方法。

```
curl -X PUT localhost:8080/users -d '{"id": "1", "name": "John Doe", "email": "john.doe@example.com"}' -H "Content-Type: application/json"
```

这将更新 ID 为“1”的用户。

### 删除用户

要删除用户，我们可以使用 DELETE 方法。

```
curl -X DELETE localhost:8080/users/1
```

这将删除 ID 为“1”的用户。

## 结论

在本文中，我们向您展示了如何使用 Spring Boot 创建一个简单的 CRUD 应用程序。我们还向您展示了如何使用“curl”测试应用程序。

现在您知道如何使用 Spring Boot 创建 CRUD 应用程序，您可以创建自己的应用程序。您还可以在 Spring Boot 网站上找到更多信息：https://spring.io/projects/spring-boot