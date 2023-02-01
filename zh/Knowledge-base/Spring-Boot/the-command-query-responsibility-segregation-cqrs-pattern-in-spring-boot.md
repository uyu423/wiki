---
title: Spring Boot 中的命令查询责任分离 (CQRS) 模式
description: 
published: true
date: 2023-02-01T14:49:31.033Z
tags: 
editor: markdown
dateCreated: 2023-02-01T14:49:31.033Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [The Command Query Responsibility Segregation (CQRS) Pattern in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-command-query-responsibility-segregation-cqrs-pattern-in-spring-boot)
{.links-list}


# Spring Boot 中的命令查询责任分离 (CQRS) 模式

CQRS 模式是一种众所周知的设计模式，已经存在了一段时间。它通常用于分布式系统和微服务架构。 CQRS 背后的主要思想是将系统的职责分为两部分：**命令**端和**查询**端。命令端负责写入，而查询端负责读取。这种关注点分离可以带来许多好处，例如改进的性能、可伸缩性和可用性。

有许多方法可以在 Spring Boot 应用程序中实现 CQRS。在本文中，我们将看看使用 **Spring Data REST** 和 **Spring Data JPA** 模块执行此操作的一种方法。

##先决条件

在我们开始之前，您需要准备好几件事。首先，您需要启动并运行一个 **Spring Boot** 应用程序。您可以在 [Spring Boot 文档](https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html) 中找到有关如何执行此操作的更多信息。

接下来，您需要将以下依赖项添加到您的项目中：

- spring-boot-starter-data-rest
- spring-boot-starter-data-jpa

## 在 Spring Boot 中实现 CQRS

现在我们已经设置好项目，可以开始实施 CQRS 模式了。我们将从创建两个 JPA 实体开始：**User** 和 **Address**。

```java
@Entity
public class User {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    @OneToOne(cascade = CascadeType.ALL, mappedBy = "user")
    private Address address;

    // Getters and setters omitted for brevity
}
```

```java
@Entity
public class Address {

    @Id
    @GeneratedValue
    private Long id;

    private String street;
    private String city;
    private String state;
    private String zipCode;

    @OneToOne
    @JoinColumn(name = "user_id")
    private User user;

    // Getters and setters omitted for brevity
}
```

接下来，我们将创建两个存储库：每个实体一个。 **UserRepository** 将扩展 **CrudRepository** 接口，而 **AddressRepository** 将扩展 **PagingAndSortingRepository** 接口。

```java
public interface UserRepository extends CrudRepository<User, Long> {

}
```

```java
public interface AddressRepository extends PagingAndSortingRepository<Address, Long> {

}
```

现在我们已经设置了存储库，我们可以创建我们的 **UserResource** 和 **AddressResource** 类。这些类将负责将我们的实体公开为 REST 资源。

```java
@RepositoryRestResource
public class UserResource extends CrudRepositoryRestResourceSupport<User> {

    private final UserRepository userRepository;

    public UserResource(UserRepository userRepository) {
        super(userRepository);
        this.userRepository = userRepository;
    }

    @Override
    public User save(@Valid User user) {
        return userRepository.save(user);
    }
}
```

```java
@RepositoryRestResource
public class AddressResource extends PagingAndSortingRepositoryRestResourceSupport<Address> {

    private final AddressRepository addressRepository;

    public AddressResource(AddressRepository addressRepository) {
        super(addressRepository);
        this.addressRepository = addressRepository;
    }

    @Override
    public Address save(@Valid Address address) {
        return addressRepository.save(address);
    }
}
```

现在我们已经设置好资源，可以开始实施 CQRS 模式了。在我们的 **UserResource** 类中，我们将向 **save()** 方法添加一个 **@CommandHandler** 注释。此注释将告诉 Spring 将对此方法的任何请求路由到 **CommandBus**。

```java
@RepositoryRestResource
public class UserResource extends CrudRepositoryRestResourceSupport<User> {

    private final UserRepository userRepository;

    public UserResource(UserRepository userRepository) {
        super(userRepository);
        this.userRepository = userRepository;
    }

    @Override
    @CommandHandler
    public User save(@Valid User user) {
        return userRepository.save(user);
    }
}
```

在我们的 **AddressResource** 类中，我们将向 **save()** 方法添加一个 **@QueryHandler** 注释。此注释将告诉 Spring 将对此方法的任何请求路由到 **QueryBus**。

```java
@RepositoryRestResource
public class AddressResource extends PagingAndSortingRepositoryRestResourceSupport<Address> {

    private final AddressRepository addressRepository;

    public AddressResource(AddressRepository addressRepository) {
        super(addressRepository);
        this.addressRepository = addressRepository;
    }

    @Override
    @QueryHandler
    public Address save(@Valid Address address) {
        return addressRepository.save(address);
    }
}
```

现在我们已经设置了资源，我们可以通过使用以下 JSON 正文向 **/users** 端点发送 POST 请求来测试我们的实现：

```json
{
    "name": "John Doe",
    "address": {
        "street": "123 Main Street",
        "city": "New York",
        "state": "NY",
        "zipCode": "10001"
    }
}
```

如果我们向 **/users** 端点发送 GET 请求，我们应该看到以下响应：

```json
[
    {
        "id": 1,
        "name": "John Doe",
        "address": {
            "id": 1,
            "street": "123 Main Street",
            "city": "New York",
            "state": "NY",
            "zipCode": "10001"
        }
    }
]
```

我们还可以向 **/addresses** 端点发送 GET 请求以查看我们创建的地址：

```json
[
    {
        "id": 1,
        "street": "123 Main Street",
        "city": "New York",
        "state": "NY",
        "zipCode": "10001"
    }
]
```

## 结论

在本文中，我们研究了一种使用 Spring Data REST 和 Spring Data JPA 模块在 Spring Boot 应用程序中实现 CQRS 模式的方法。我们还看到了这种关注点分离如何带来许多好处，例如改进的性能、可伸缩性和可用性。