---
title: Spring Boot 开发中的享元模式
description: 
published: true
date: 2023-02-03T21:17:36.868Z
tags: 
editor: markdown
dateCreated: 2023-02-03T21:17:34.495Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [The Flyweight Pattern in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-flyweight-pattern-in-spring-boot-development)
{.links-list}


# Spring Boot 开发中的享元模式

享元模式是在处理大量对象时优化代码的有用工具。关键思想是重用现有对象而不是创建新对象，这样可以节省时间和内存。

在 Spring Boot 开发中，享元模式可用于通过缓存公共对象并跨请求重用它们来提高性能。例如，如果您有一个返回用户列表的服务，您可以缓存该列表并重新使用它，而不是每次都从数据库中获取它。

要在 Spring Boot 中实现享元模式，可以使用 Spring Cache 抽象。这允许您以声明方式指定应缓存哪些对象以及应如何使它们失效。

在本文中，我们将了解如何在 Spring Boot 开发中使用享元模式。我们将从查看该模式可以解决的问题开始。然后我们将看看如何使用 Spring Cache 抽象来实现该模式。最后，我们将查看一些与享元模式相关的更高级的主题。

## 问题

考虑一个简单的 Spring Boot 应用程序，它公开一个用于管理用户的 REST API。 API 有一个返回用户列表的 GET 端点。端点如下所示：

```
@GetMapping("/users")
public List<User> getUsers() {
    return userService.getUsers();
}
```
@Repository
public interface UserRepository extends CrudRepository<User, Long> {

}
```
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public List<User> getUsers() {
        return userRepository.findAll();
    }

}
```
@服务
公共类用户服务{

    @Autowired
    私有用户存储库用户存储库；

    公共列表<用户> getUsers() {
        返回 userRepository.findAll();
    }

}
```

```UserService``` 使用```UserRepository``` 从数据库中获取用户。 ```UserRepository``` 是一个简单的 CRUD 存储库：

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-cache</artifactId>
</dependency>
```

现在，假设我们的数据库中有大量用户。当我们向 ```/users``` 端点发出请求时，需要很长时间才能从数据库中获取所有用户。这可能会导致我们的应用程序变得缓慢且无响应。

解决这个问题的一种方法是缓存用户列表。这样，当我们向 ```/users``` 端点发出请求时，我们可以简单地返回缓存的用户列表，而不是每次都从数据库中获取它。

## 实现享元模式

我们可以使用 Spring Cache 抽象在我们的示例应用程序中实现 Flyweight 模式。首先，我们需要将 ```spring-boot-starter-cache``` 依赖项添加到我们的 ```pom.xml``` 中：

```
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    @Cacheable(value = "users")
    public List<User> getUsers() {
        return userRepository.findAll();
    }

}
```

接下来，我们需要配置 ```UserService``` 来使用缓存。我们可以通过使用 ```@Cacheable``` 注释来注释 ```getUsers()``` 方法来做到这一点：

```
@Cacheable(value = "users", key = "#id")
public User getUserById(Long id) {
    return userRepository.findById(id).orElse(null);
}
```

```
@CacheEvict(value = "users", key = "#id")
public void deleteUserById(Long id) {
    userRepository.deleteById(id);
}
```/users``` 端点发出请求时，```getUsers()``` 方法将返回缓存的用户列表。第一次调用该方法时，它将从数据库中获取用户并缓存它们。后续调用将简单地返回缓存的用户列表。

我们还可以配置```@Cacheable```注解来控制缓存结果如何失效。例如，我们可以使用 ```key``` 属性来指定缓存对象的键：

```
@Cacheable(value = "users", expire = 60)
public List<User> getUsers() {
    return userRepository.findAll();
}
```

在此示例中，我们已指定缓存结果应由 ```id``` 参数键入。这意味着只要 ```id``` 发生变化，缓存的结果就会失效。

我们还可以使用 ```@CacheEvict``` 注释从缓存中显式驱逐对象：

```
@CacheEvict(value = "users", allEntries = true)
public void deleteUserById(Long id) {
    userRepository.deleteById(id);
}
```

在此示例中，我们使用“@CacheEvict”注释对“deleteUserById()”方法进行了注释。这告诉 Spring 在调用 ```deleteUserById()``` 方法时清除 ```getUserById()``` 方法的缓存结果。

## 高级主题

有几个与享元模式相关的高级主题值得一提。

### 过期

默认情况下，Spring Cache 抽象会在经过一定时间后使缓存的对象过期。默认到期时间为两小时。

我们可以通过使用```@Cacheable```注解的```expire```属性来控制缓存对象的过期时间：

```
public class User {

    private Long id;

    private String name;

    private Date birthDate;

    // Getters and setters...

}
```

在此示例中，我们已指定缓存结果应在 60 秒后过期。

我们还可以使用 ```@CacheEvict``` 注释来显式使对象过期：

```
public class User implements Serializable {

    private static final long serialVersionUID = 1L;

    private Long id;

    private String name;

    private Date birthDate;

    // Getters and setters...

}
```

在此示例中，我们使用“@CacheEvict”注释对“deleteUserById()”方法进行了注释。 ```allEntries``` 属性告诉 Spring 使 ```users``` 缓存中的所有对象过期。

### 序列化

Spring Cache 抽象可用于缓存任何类型的对象。但是，重要的是要了解 CacheManager 将序列化和反序列化缓存的对象这一事实。

如果缓存的对象不可序列化，这可能会导致问题。例如，考虑以下 ```User``` 类：

```
public class SerializableUser implements Serializable {

    private static final long serialVersionUID = 1L;

    private User user;

    // Getters and setters...

}
```

```User``` 类不可序列化，因为它包含一个```Date``` 字段。这意味着我们不能缓存 ```User``` 对象。

解决此问题的一种方法是使 ```User``` 类可序列化：

```
公共类用户实现序列化{

    private static final long serialVersionUID = 1L;

    私人长号；

    私有字符串名称；

    私人日期出生日期；

    // 获取器和设置器...

}
```

在这个例子中，我们通过添加一个 ```serialVersionUID``` 字段使 ```User``` 类可序列化。 ```Serializable``` 接口需要这个字段。

解决此问题的另一种方法是使用```Serializable```包装类：

```
公共类 SerializableUser 实现 Serializable {

    private static final long serialVersionUID = 1L;

    私人用户用户；

    // 获取器和设置器...

}
```

在这个例子中，我们创建了一个 ```SerializableUser``` 类，它包装了一个 ```User``` 对象。这允许我们缓存 ```SerializableUser``` 对象，而不必使 ```User``` 类可序列化。

## 结论

在本文中，我们了解了如何在 Spring Boot 开发中使用享元模式。我们首先查看该模式可以解决的问题。然后我们研究了如何使用 Spring Cache 抽象来实现该模式。最后，我们研究了一些与享元模式相关的更高级的主题。