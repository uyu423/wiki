---
title: 将 Hibernate 与 Spring Boot 集成
description: 
published: true
date: 2023-02-06T07:32:35.445Z
tags: 
editor: markdown
dateCreated: 2023-02-06T07:32:29.629Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Integrating Hibernate with Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/integrating-hibernate-with-spring-boot)
{.links-list}


# 将 Hibernate 与 Spring Boot 集成

在本文中，我们将了解如何将 Hibernate 与 Spring Boot 框架集成。

## 什么是休眠？

Hibernate 是一个 Java 框架，它简化了 Java 应用程序持久化的开发。它提供了一个强大的对象关系映射工具，用于在关系数据库中存储数据。

## 什么是 Spring Boot？

Spring Boot 是一个基于 Java 的框架，它提供了一种简单的方法来创建独立的、生产级的基于 Spring 的应用程序。这是构建微服务的绝佳选择。

## 为什么要在 Spring Boot 中使用 Hibernate？

对于希望在基于 Spring 的应用程序中使用关系数据库的 Java 开发人员来说，Hibernate 是一个流行的选择。它易于设置并具有广泛的功能，包括对象缓存和查询优化。

## 如何将 Hibernate 与 Spring Boot 集成

将 Hibernate 与 Spring Boot 集成有两种方式：

### 1.使用Spring Boot内置的Hibernate支持

Spring Boot 提供了对 Hibernate 的内置支持。您只需将以下依赖项添加到项目的 `pom.xml` 文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

这将为 Hibernate 添加所有必需的依赖项，包括 Hibernate Core 和 JPA（Java Persistence API）库。

### 2. 使用特定于 Hibernate 的 Spring Boot 启动器

或者，您可以使用特定于 Hibernate 的 Spring Boot starter，它提供了对 Hibernate 配置的更细粒度的控制。要使用此启动器，请将以下依赖项添加到项目的“pom.xml”文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-hibernate</artifactId>
</dependency>
```

## 使用 Spring Boot 配置 Hibernate

添加所需的依赖项后，您可以通过将以下属性添加到 application.properties 文件来配置 Hibernate：

```properties
# Hibernate settings
spring.jpa.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
spring.jpa.hibernate.ddl-auto=update
```

`spring.jpa.hibernate.dialect` 属性配置要使用的 Hibernate 方言。这告诉 Hibernate 如何将 Java 对象翻译成 SQL 语句。

`spring.jpa.hibernate.ddl-auto` 属性配置 Hibernate 的自动 DDL 模式。这告诉 Hibernate 自动为实体生成所需的 SQL 模式。 `update` 模式将在模式发生变化时更新它，但如果模式不存在则不会创建它。

## 创建一个 Hibernate 实体

要创建 Hibernate 实体，您只需创建一个 Java 类来表示数据库中的一个表。例如，以下代码定义了一个 `User` 实体：

```java
@Entity
public class User {
 
    @Id
    @GeneratedValue
    private Long id;
 
    @Column(nullable = false)
    private String name;
 
    // ...
}
```

@Entity 注释将类标记为 Hibernate 实体。 `@Id` 注解将 `id` 字段标记为主键。 `@Column` 注释将 `name` 字段标记为数据库表中的一列。

## 创建 Hibernate 存储库

要创建 Hibernate 存储库，您只需创建一个扩展 `CrudRepository` 接口的接口。例如，下面的代码定义了一个 `UserRepository`：

```java
public interface UserRepository extends CrudRepository<User, Long> {
}
```

此存储库为“用户”实体提供基本的 CRUD 操作。

## 将存储库注入服务

要将存储库注入服务，您可以使用“@Autowired”注释。例如，以下代码将 `UserRepository` 注入到 `UserService` 中：

```java
@Service
public class UserService {
 
    @Autowired
    private UserRepository userRepository;
 
    // ...
}
```

## 使用存储库

将存储库注入服务后，您可以使用它对实体执行 CRUD 操作。例如，以下代码创建一个新的 `User`：

```java
@Service
public class UserService {
 
    @Autowired
    private UserRepository userRepository;
 
    public User create(String name) {
        User user = new User();
        user.setName(name);
        return userRepository.save(user);
    }
 
    // ...
}
```

## 参考

- [休眠](https://hibernate.org/)
- [春季启动](https://spring.io/projects/spring-boot)
- [Spring Data JPA](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/# reference)
- [春季数据休眠](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-sql.html# boot-features-hibernate)