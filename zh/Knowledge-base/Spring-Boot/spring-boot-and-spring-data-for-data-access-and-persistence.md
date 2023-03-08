---
title: 用于数据访问和持久化的 Spring Boot 和 Spring Data
description: 
published: true
date: 2023-02-08T06:32:33.245Z
tags: 
editor: markdown
dateCreated: 2023-02-08T06:32:31.671Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot and Spring Data for Data Access and Persistence***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-spring-data-for-data-access-and-persistence)
{.links-list}


# 用于数据访问和持久化的 Spring Boot 和 Spring Data

## 介绍

Spring Boot 是一种流行的 Java Web 应用程序框架，它提供了一系列功能，包括 CLI、嵌入式 Tomcat 和自动配置。 Spring Data是Spring的一个子项目，专注于为Java应用程序提供数据访问和持久化解决方案。

在本文中，我们将了解如何使用 Spring Boot 和 Spring Data 访问和保存关系数据库中的数据。我们还将探索使 Spring Data 成为 Java 应用程序中数据访问和持久性的良好选择的一些特性。

## 为关系数据库配置 Spring Boot

Spring Boot 可以配置为与各种关系数据库一起工作，包括 MySQL、PostgreSQL 和 Oracle。在本节中，我们将了解如何配置 Spring Boot 以使用 MySQL 数据库。

首先，我们需要将以下依赖项添加到我们的 `pom.xml` 文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

接下来，我们需要在我们的 application.properties 文件中配置一些属性：

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydatabase
spring.datasource.username=myusername
spring.datasource.password=mypassword

spring.jpa.database=MYSQL
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update
```

在 `spring.datasource` 属性中，我们正在为 MySQL 数据库配置 URL、用户名和密码。在 spring.jpa 属性中，我们配置数据库类型 (MySQL)，告诉 Spring Boot 显示 SQL 查询，并告诉 Hibernate 自动更新数据库模式。

## 使用 Spring Data 访问数据

Spring Data 使得使用 Java 访问关系数据库中的数据变得容易。在本节中，我们将了解如何使用 Spring Data 访问 MySQL 数据库中的数据。

首先，我们需要为我们的数据创建一个“@Repository”接口：

```java
@Repository
public interface MyRepository extends JpaRepository<MyEntity, Long> {

}
```

@Repository 注释告诉 Spring 这是一个数据存储库。 `JpaRepository` 接口提供了访问关系数据库中数据的方法。 `MyEntity` 类是一个实体类，代表我们数据库中的一行。 `Long` 类型是我们实体的主键类型。

接下来，我们需要创建一个实体类：

```java
@Entity
public class MyEntity {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    // Getters and setters
}
```

@Entity 注释告诉 Spring 这是一个实体类。 `@Id` 注释告诉 Spring `id` 字段是实体的主键。 `@GeneratedValue` 注解告诉 Spring `id` 字段应该由数据库自动生成。

现在我们已经设置了存储库和实体类，我们可以使用它们来访问数据库中的数据。例如，我们可以使用 findAll() 方法来查找数据库中的所有实体：

```java
List<MyEntity> myEntities = myRepository.findAll();
```

我们还可以使用 `save()` 方法将实体保存到我们的数据库中：

```java
MyEntity myEntity = new MyEntity();
myEntity.setName("John Smith");

myRepository.save(myEntity);
```

## 结论

在本文中，我们了解了如何使用 Spring Boot 和 Spring Data 访问和保存关系数据库中的数据。我们还看到了 Spring Data 如何使访问 Java 应用程序中的数据变得容易。