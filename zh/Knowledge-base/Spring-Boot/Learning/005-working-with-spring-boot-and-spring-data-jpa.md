---
title: 005：使用 Spring Boot 和 Spring Data JPA
description: 
published: true
date: 2023-02-03T07:43:44.927Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:43:43.290Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [005: Working with Spring Boot and Spring Data JPA***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/005-working-with-spring-boot-and-spring-data-jpa)
{.links-list}


# 使用 Spring Boot 和 Spring Data JPA

在本文中，我们将了解如何使用 Spring Boot 和 Spring Data JPA。

我们将从了解 JPA 是什么以及我们为什么要使用它开始。然后，我们将看看如何配置 Spring Boot 以使用 JPA。最后，我们将编写一些简单的示例程序来展示如何在 Spring Boot 应用程序中使用 JPA。

## 什么是 JPA？

JPA 是 Java 持久性 API。它是关于如何将 Java 对象映射到关系数据库的规范。

JPA 有很多实现，最流行的是 Hibernate。使用 JPA 时，您可以针对 JPA API 编写代码，并让 JPA 实现（如 Hibernate）处理将对象映射到数据库的细节。

## 为什么要使用 JPA？

您可能希望在应用程序中使用 JPA 的原因有以下几个：

- **JPA 是一个标准**。这意味着有许多 JPA 实现可供选择，并且您可以根据需要切换实现。

- **JPA 是灵活的**。您可以将 JPA 与不同类型的数据库一起使用，并且可以以不同的方式将 Java 对象映射到数据库。

- **JPA 易于使用**。 JPA API 旨在易于使用，因此您可以快速开始使用 JPA。

## 为 JPA 配置 Spring Boot

Spring Boot 使配置 Spring 以与 JPA 一起使用变得容易。您需要做的就是将 spring-boot-starter-data-jpa 依赖项添加到您的项目中。

此依赖项将引入所有必需的 JPA 依赖项，并且还将配置 Spring Boot 以使用 JPA 实现（默认情况下为 Hibernate）。

## 在 Spring Boot 中使用 JPA

现在我们已经将 Spring Boot 配置为使用 JPA，让我们编写一些示例程序来展示如何在 Spring Boot 应用程序中使用 JPA。

### 示例 1：创建 JPA 实体

要在您的应用程序中使用 JPA，您需要创建一个 JPA 实体。 JPA 实体是映射到数据库表的 Java 类。

让我们创建一个简单的 JPA 实体：

```java
@Entity
public class Person {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    // ... getters and setters
}
```

此类映射到数据库中的“person”表。 `@Entity` 注释表示这是一个 JPA 实体。 `@Id` 注释表示 `id` 字段是实体的主键。 `@GeneratedValue` 注释告诉 JPA 为每个实体生成一个唯一的 ID。

### 示例 2：创建 JPA 存储库

现在我们有了 JPA 实体，我们需要一种访问它的方法。我们可以通过创建 JPA 存储库来做到这一点。

JPA 存储库是用于访问 JPA 实体的 Spring Data 存储库。要创建 JPA 存储库，我们需要创建一个扩展 JpaRepository 接口的接口：

```java
public interface PersonRepository extends JpaRepository<Person, Long> {

}
```

此接口用于访问 `Person` 实体。 `JpaRepository` 接口提供了许多用于处理 JPA 实体的方法，因此我们无需编写任何代码来实现此接口。

### 示例 3：使用 JPA 存储库

现在我们有了 JPA 实体和存储库，让我们编写一个使用存储库创建、读取、更新和删除实体的程序。

首先，我们将把 PersonRepository 注入到我们的程序中：

```java
@Autowired
private PersonRepository personRepository;
```

接下来，我们将使用存储库创建一个“Person”实体：

```java
Person person = new Person();
person.setName("John Doe");

personRepository.save(person);
```

这将在 person 表中插入一个新行。 `save` 方法将为实体生成一个唯一的 id 并将其设置在实体上。

我们可以使用 `findById` 方法通过其 id 检索实体：

```java
Person person = personRepository.findById(1L);
```

我们可以使用 `findAll` 方法来检索所有实体：

```java
List<Person> people = personRepository.findAll();
```

我们可以使用 deleteById 方法来删除一个实体：

```java
personRepository.deleteById(1L);
```

我们可以使用 delete 方法删除一个实体：

```java
personRepository.delete(person);
```

这些只是 JpaRepository 接口上可用的一些方法。有关方法的完整列表，请参阅 [JpaRepository 文档](https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/JpaRepository.html) .

## 结论

在本文中，我们了解了如何使用 Spring Boot 和 Spring Data JPA。我们已经了解了如何配置 Spring Boot 以使用 JPA，并且我们编写了一些简单的示例程序来展示如何在 Spring Boot 应用程序中使用 JPA。