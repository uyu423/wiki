---
title: Spring Data JPA：高级技术
description: 
published: true
date: 2023-02-06T23:17:42.498Z
tags: 
editor: markdown
dateCreated: 2023-02-06T23:17:40.924Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Data JPA: Advanced Techniques***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-data-jpa-advanced-techniques)
{.links-list}


# Spring Data JPA：高级技术

Java Persistence API (JPA) 是一种 Java 规范，用于在关系数据库中存储、访问和管理数据。 Spring Data JPA 是 JPA 的 Spring 框架实现，它使在 Spring 应用程序中使用 JPA 变得更加容易。

在本文中，我们将介绍 Spring Data JPA 中的一些高级主题，包括：

- 预测
- 查询dsl
- 标准API

## 预测

投影是一种指定要从数据库中检索实体的哪些字段的方法。 Spring Data JPA 支持两种类型的投影：

- 基于界面的预测
- 动态预测

### 基于接口的投影

使用基于接口的投影，您可以创建一个定义要检索的字段的接口，Spring Data JPA 在运行时生成该接口的实现。这是使用投影的推荐方式，因为它允许您利用 IDE 的类型安全和代码完成功能。

要使用基于接口的投影，您首先需要创建一个接口来定义您要检索的字段：

```java
public interface UserNameOnly {
    String getUsername();
}
```

然后您可以在查询中使用该接口：

```java
List<UserNameOnly> users = userRepository.findAll(projection(UserNameOnly.class));
```

### 动态预测

使用动态投影，您可以将要检索的字段指定为字符串。这不如基于接口的投影类型安全，但如果您想要检索不属于您的实体模型的字段，它会很有用。

要使用动态投影，您首先需要创建一个定义要检索的字段的类：

```java
public class UserNameOnly {
    private String username;

    public String getUsername() {
        return username;
    }
}
```

然后您可以在查询中使用该类：

```java
List<UserNameOnly> users = userRepository.findAll(projection(UserNameOnly.class, "username"));
```

## 查询dsl

Querydsl 是一个库，允许您使用基于 Java 的领域特定语言创建类型安全的查询。它可以与 JPA、JDO 和其他数据访问框架一起使用。

要将 Querydsl 与 Spring Data JPA 一起使用，您需要将 Querydsl JPA 依赖项添加到您的项目中：

```xml
<dependency>
    <groupId>com.querydsl</groupId>
    <artifactId>querydsl-jpa</artifactId>
    <version>${querydsl.version}</version>
</dependency>
```

您还需要配置 Querydsl 来为您的实体生成代码：

```xml
<build>
    <plugins>
        ...
        <plugin>
            <groupId>com.mysema.maven</groupId>
            <artifactId>apt-maven-plugin</artifactId>
            <version>1.1.3</version>
            <configuration>
                <outputDirectory>target/generated-sources/java</outputDirectory>
                <processor>com.querydsl.apt.jpa.JPAAnnotationProcessor</processor>
            </configuration>
            <executions>
                <execution>
                    <goals>
                        <goal>process</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
        ...
    </plugins>
</build>
```

配置 Querydsl 后，您可以使用它来创建类型安全的查询：

```java
QUser user = QUser.user;
List<User> users = queryFactory
    .selectFrom(user)
    .where(user.username.eq("johndoe"))
    .fetch();
```

## 标准 API

Criteria API 是用于构建类型安全查询的 Java API。它是 JPA 规范的一部分，可以与任何符合 JPA 的数据访问框架一起使用。

要将 Criteria API 与 Spring Data JPA 一起使用，您需要创建一个 CriteriaQuery：

```java
CriteriaBuilder builder = entityManager.getCriteriaBuilder();
CriteriaQuery<User> criteria = builder.createQuery(User.class);
```

然后，您可以使用 CriteriaQuery 来构建查询：

```java
Root<User> user = criteria.from(User.class);
criteria.select(user);
criteria.where(builder.equal(user.get("username"), "johndoe"));
```

最后，您可以执行查询：

```java
List<User> users = entityManager.createQuery(criteria).getResultList();
```

## 结论

在本文中，我们介绍了 Spring Data JPA 中的一些高级主题，包括投影、Querydsl 和 Criteria API。我们还看到了如何在 Spring 应用程序中使用这些功能中的每一个。