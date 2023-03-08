---
title: Kotlin 和 Spring Data：连接到数据库
description: 
published: true
date: 2023-02-08T09:17:31.324Z
tags: 
editor: markdown
dateCreated: 2023-02-08T09:17:29.678Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kotlin and Spring Data: Connecting to a Database***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-spring-data-connecting-to-a-database)
{.links-list}


# Kotlin 和 Spring Data：连接到数据库

Kotlin 是一种静态类型的编程语言，运行在 Java 虚拟机上，也可以编译成 JavaScript 源代码。 Kotlin 由 JetBrains 开发。

Spring Data 是一个项目，可以更轻松地在 Spring 框架中使用数据访问技术，例如关系数据库。

在本文中，我们将了解如何使用 Kotlin 和 Spring Data 连接到数据库。

## 设置项目

首先，我们需要使用 Spring Initializr 创建一个新的 Kotlin 项目。我们需要选择以下依赖项：

- 网络
- 春季数据 JPA
- H2数据库

![spring-initializr](https://i.imgur.com/G9dLNcJ.png)

生成项目后，我们可以将其导入到我们最喜欢的 IDE 中。我将使用 IntelliJ IDEA。

## 配置数据源

接下来，我们需要配置数据源。我们可以通过将以下内容添加到 `application.properties` 文件来做到这一点：

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

spring.jpa.generate-ddl=true
spring.jpa.hibernate.ddl-auto=create-drop
```

`spring.datasource.url` 属性定义了数据库的 URL。 `spring.datasource.driverClassName` 属性定义了驱动类名。 `spring.datasource.username` 属性定义了用户名。 `spring.datasource.password` 属性定义密码。

`spring.jpa.generate-ddl` 属性告诉 Spring Data 生成数据库模式。 `spring.jpa.hibernate.ddl-auto` 属性告诉 Hibernate 创建和删除数据库模式。

## 创建实体

接下来，我们需要创建一个实体。实体是表示数据库中表的类。我们可以通过使用 @Entity 注释来注释类来创建实体。

```kotlin
@Entity
class User(
        @Id @GeneratedValue val id: Long,
        val name: String,
        val age: Int
)
```

`@Entity` 注释表示这是一个实体。 `@Id` 注解表示 `id` 属性是主键。 `@GeneratedValue` 注解表示 `id` 属性应该由数据库生成。

`name` 和 `age` 属性将映射到数据库中的列。

## 创建存储库

接下来，我们需要创建一个存储库。存储库是提供对数据库中数据的访问的类。我们可以通过使用 @Repository 注释来注释类来创建存储库。

```kotlin
@Repository
interface UserRepository : CrudRepository<User, Long>
```

`@Repository` 注释表示这是一个存储库。 `CrudRepository` 接口提供了 CRUD 操作的方法。

## 创建服务

接下来，我们需要创建一个服务。服务是包含业务逻辑的类。我们可以通过使用 @Service 注释来注释类来创建服务。

```kotlin
@Service
class UserService(
        private val userRepository: UserRepository
) {
    fun createUser(user: User): User {
        return userRepository.save(user)
    }

    fun getUserById(id: Long): User? {
        return userRepository.findById(id).orElse(null)
    }

    fun getAllUsers(): List<User> {
        return userRepository.findAll().toList()
    }

    fun updateUser(user: User): User {
        return userRepository.save(user)
    }

    fun deleteUserById(id: Long) {
        userRepository.deleteById(id)
    }
}
```

`@Service` 注释表示这是一项服务。 `createUser` 方法创建一个新用户。 `getUserById` 方法通过 id 获取用户。 `getAllUsers` 方法获取所有用户。 `updateUser` 方法更新用户。 `deleteUserById` 方法通过 id 删除用户。

## 创建控制器

最后，我们需要创建一个控制器。控制器是一个包含处理 HTTP 请求的方法的类。我们可以通过使用 @RestController 注释来注释类来创建控制器。

```kotlin
@RestController
@RequestMapping("/users")
class UserController(
        private val userService: UserService
) {
    @PostMapping
    fun createUser(@RequestBody user: User): User {
        return userService.createUser(user)
    }

    @GetMapping("/{id}")
    fun getUserById(@PathVariable id: Long): User? {
        return userService.getUserById(id)
    }

    @GetMapping
    fun getAllUsers(): List<User> {
        return userService.getAllUsers()
    }

    @PutMapping
    fun updateUser(@RequestBody user: User): User {
        return userService.updateUser(user)
    }

    @DeleteMapping("/{id}")
    fun deleteUserById(@PathVariable id: Long) {
        userService.deleteUserById(id)
    }
}
```

`@RestController` 注释表明这是一个控制器。 @RequestMapping 注释将 HTTP 请求映射到控制器中的方法。 `@PostMapping` 注释将 HTTP POST 请求映射到 `createUser` 方法。 `@GetMapping` 注释将 HTTP GET 请求映射到 `getUserById` 方法。 `@PutMapping` 注释将 HTTP PUT 请求映射到 `updateUser` 方法。 `@DeleteMapping` 注释将 HTTP DELETE 请求映射到 `deleteUserById` 方法。

## 测试端点

我们可以使用 curl 或 Postman 测试端点。

```
$ curl -X POST localhost:8080/users -d '{"name": "John Doe", "age": 42}' -H "Content-Type: application/json"
{"id":1,"name":"John Doe","age":42}

$ curl localhost:8080/users/1
{"id":1,"name":"John Doe","age":42}

$ curl localhost:8080/users
[{"id":1,"name":"John Doe","age":42}]

$ curl -X PUT localhost:8080/users -d '{"id": 1, "name": "Jane Doe", "age": 43}' -H "Content-Type: application/json"
{"id":1,"name":"Jane Doe","age":43}

$ curl -X DELETE localhost:8080/users/1
```

## 结论

在本文中，我们了解了如何使用 Kotlin 和 Spring Data 连接到数据库。