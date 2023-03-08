---
title: 010: 使用 Spring Boot 和 Redis 实现缓存
description: 
published: true
date: 2023-02-03T08:43:41.420Z
tags: 
editor: markdown
dateCreated: 2023-02-03T08:43:36.493Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [010: Implementing caching with Spring Boot and Redis***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/010-implementing-caching-with-spring-boot-and-redis)
{.links-list}


# 使用 Spring Boot 和 Redis 实现缓存

在这篇文章中，我们将介绍如何使用 Spring Boot 和 Redis 实现缓存。我们将从简要概述缓存及其有用的原因开始。然后我们将看看如何配置 Spring Boot 以使用 Redis 进行缓存。最后，我们将编写一个简单的 Spring Boot 应用程序来演示如何使用 Redis 进行缓存。

## 什么是缓存？

缓存是一种将数据存储在临时内存位置以加快对该数据的后续访问的技术。当数据被缓存时，未来对该数据的请求可以得到更快的服务，因为数据已经在内存中。

有两种主要的缓存类型：应用程序缓存和数据库缓存。应用程序缓存用于将数据缓存在应用程序的内存中，而数据库缓存用于将数据缓存在数据库的内存中。

## 为什么要使用缓存？

缓存可用于通过减少从慢速存储介质（如数据库）读取数据的次数来提高应用程序的性能。缓存还可以用于通过将数据副本存储在更快的存储介质（例如内存）中来减少需要从慢速存储介质读取的数据量。

## 配置 Spring Boot 使用 Redis 进行缓存

Spring Boot 提供了对 Redis 的内置支持，可以轻松配置 Redis 以进行缓存。要配置 Spring Boot 使用 Redis 进行缓存，需要在项目中添加如下依赖：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

您还需要在 application.properties 文件中配置 Redis 服务器主机和端口：

```properties
spring.redis.host=localhost
spring.redis.port=6379
```

## 编写 Spring Boot 应用程序以使用 Redis 进行缓存

现在我们已经将 Spring Boot 配置为使用 Redis 进行缓存，让我们编写一个简单的 Spring Boot 应用程序来演示如何使用 Redis 进行缓存。

我们将从创建一个简单的数据模型来代表用户开始：

```java
public class User {

    private Long id;
    private String name;
    private Integer age;

    // getters and setters
}
```

接下来，我们将使用单个 REST 控制器创建一个简单的 Spring Boot 应用程序来管理用户：

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        // code to get user from database
    }

    @PostMapping
    public User createUser(@RequestBody User user) {
        // code to create user in database
    }

    @PutMapping("/{id}")
    public User updateUser(@PathVariable Long id, @RequestBody User user) {
        // code to update user in database
    }

    @DeleteMapping("/{id}")
    public void deleteUser(@PathVariable Long id) {
        // code to delete user from database
    }
}
```

我们现在可以使用这个控制器来管理我们数据库中的用户。但是，每次我们调用 getUser() 方法时，都会执行数据库查询以从数据库中获取用户。这可能很慢，尤其是在数据库很大的情况下。

我们可以通过使用 Redis 缓存 getUser() 方法的结果来提高应用程序的性能。为此，我们将 @Cacheable 注释添加到 getUser() 方法：

```java
@Cacheable("users")
@GetMapping("/{id}")
public User getUser(@PathVariable Long id) {
    // code to get user from database
}
```

此注释告诉 Spring 将 getUser() 方法的结果缓存在名为“users”的 Redis 缓存中。下次使用相同的 id 调用 getUser() 方法时，将返回缓存的结果，而不是执行数据库查询。

我们还可以使用 @CacheEvict 注释来删除缓存条目：

```java
@CacheEvict("users")
@DeleteMapping("/{id}")
public void deleteUser(@PathVariable Long id) {
    // code to delete user from database
}
```

当调用 deleteUser() 方法时，此注释告诉 Spring 删除具有给定 id 的用户的缓存条目。

## 结论

在这篇文章中，我们介绍了如何使用 Spring Boot 和 Redis 实现缓存。我们已经了解了如何配置 Spring Boot 以使用 Redis 进行缓存，并且编写了一个简单的 Spring Boot 应用程序来演示如何使用 Redis 进行缓存。