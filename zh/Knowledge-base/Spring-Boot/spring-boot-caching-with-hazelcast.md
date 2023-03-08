---
title: 使用 Hazelcast 进行 Spring Boot 缓存
description: 
published: true
date: 2023-01-31T22:18:01.230Z
tags: 
editor: markdown
dateCreated: 2023-01-31T22:17:59.605Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Spring Boot Caching with Hazelcast***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-caching-with-hazelcast)
{.links-list}


# 使用 Hazelcast 进行 Spring Boot 缓存

缓存是任何高性能应用程序的关键组件。它可以将响应时间缩短几个数量级，并减少应用程序服务器上的负载。

有许多可用的缓存解决方案，但最流行的解决方案之一是 Hazelcast。 Hazelcast 是一个开源分布式缓存解决方案，可以很容易地与 Spring Boot 应用程序集成。

在本文中，我们将了解如何在 Spring Boot 应用程序中使用 Hazelcast 进行缓存。我们将从一个简单的示例开始，然后探索 Hazelcast 必须提供的一些更高级的功能。

## 设置 Hazelcast

我们需要做的第一件事是设置一个 Hazelcast 实例。我们可以使用 Hazelcast Spring Boot Starter 来做到这一点。

要将启动程序添加到您的项目中，只需将以下依赖项添加到您的构建文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-hazelcast</artifactId>
</dependency>
```

一旦将启动器添加到您的项目中，Hazelcast 将在您的应用程序运行时自动配置和启动。

## 使用 Hazelcast 进行缓存

现在我们已经启动并运行了 Hazelcast，让我们来看看如何使用它进行缓存。

我们将从一个简单的例子开始。假设我们有一个返回用户列表的服务：

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    );

    public List<User> getUsers() {
        return users;
    }
}
```

此服务由 REST 控制器调用：

```java
@RestController
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/users")
    public List<User> getUsers() {
        return userService.getUsers();
    }
}
```

我们可以通过缓存 getUsers 方法的结果来提高这个控制器的性能：

```java
@RestController
public class UserController {

    private final UserService userService;

    private final HazelcastInstance hazelcastInstance;

    public UserController(UserService userService, HazelcastInstance hazelcastInstance) {
        this.userService = userService;
        this.hazelcastInstance = hazelcastInstance;
    }

    @GetMapping("/users")
    public List<User> getUsers() {
        List<User> users = hazelcastInstance.getList("users");
        if (users == null) {
            users = userService.getUsers();
            hazelcastInstance.setList("users", users);
        }
        return users;
    }
}
```

在这个例子中，我们使用 `List` 作为我们的缓存。 Hazelcast 还支持“Map”、“Set”和“Queue”结构。

我们还可以缓存单个方法的结果：

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    );

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }
}
```

在这种情况下，我们不需要显式配置缓存。 Spring Boot 会自动配置缓存管理器并缓存 getUsers 方法的结果。

## 从缓存中逐出条目

请务必记住，一旦条目被缓存，它将一直保留在缓存中，直到它被显式逐出。如果基础数据发生变化，这可能会导致返回过时的数据。

我们可以使用 @CacheEvict 注释从缓存中逐出一个条目：

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    );

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }

    @CacheEvict("users")
    public void evictUsers() {
    }
}
```

在这个例子中，我们用 @CacheEvict 注释了 evictUsers 方法。这将导致在调用该方法时清除“用户”缓存。

我们还可以使用 @CacheEvict(allEntries = true) 注释从所有缓存中逐出所有条目：

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    );

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }

    @CacheEvict(allEntries = true)
    public void evictAll() {
    }
}
```

## 更新缓存条目

我们还可以使用 @CachePut 注释更新缓存的条目：

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    );

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }

    @CachePut("users")
    public List<User> updateUsers() {
        return users;
    }
}
```

在此示例中，“updateUsers”方法使用“@CachePut”注释。这将导致在调用该方法时更新“用户”缓存。

## 结论

在本文中，我们了解了如何在 Spring Boot 应用程序中使用 Hazelcast 进行缓存。我们已经了解了如何设置 Hazelcast 以及如何使用它来缓存数据。我们还了解了如何从缓存中逐出条目以及如何更新缓存的条目。

缓存是任何高性能应用程序的关键组件。通过使用 Hazelcast，我们可以轻松地向我们的 Spring Boot 应用程序添加缓存。