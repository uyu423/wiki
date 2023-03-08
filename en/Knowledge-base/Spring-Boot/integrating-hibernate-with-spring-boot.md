---
title: Integrating Hibernate with Spring Boot
description: 
published: true
date: 2023-02-06T07:32:31.339Z
tags: 
editor: markdown
dateCreated: 2023-02-06T07:32:29.635Z
---

- [Integrando Hibernate con Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/integrating-hibernate-with-spring-boot)
{.links-list}
- [将 Hibernate 与 Spring Boot 集成***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/integrating-hibernate-with-spring-boot)
{.links-list}
- [스프링 부트와 하이버네이트 통합***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/integrating-hibernate-with-spring-boot)
{.links-list}


# Integrating Hibernate with Spring Boot

In this article, we'll take a look at how to integrate Hibernate with the Spring Boot framework.

## What is Hibernate?

Hibernate is a Java framework that simplifies the development of Java application persistence. It provides a powerful object-relational mapping tool for storing data in a relational database.

## What is Spring Boot?

Spring Boot is a Java-based framework that provides a simple way to create stand-alone, production-grade Spring-based applications. It is a great choice for building microservices.

## Why use Hibernate with Spring Boot?

Hibernate is a popular choice for Java developers who want to use a relational database with their Spring-based applications. It is easy to set up and has a wide range of features, including object caching and query optimization.

## How to integrate Hibernate with Spring Boot

There are two ways to integrate Hibernate with Spring Boot:

### 1. Use Spring Boot's built-in Hibernate support

Spring Boot provides built-in support for Hibernate. You can simply add the following dependency to your project's `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

This will add all the required dependencies for Hibernate, including the Hibernate Core and JPA (Java Persistence API) libraries.

### 2. Use the Hibernate-specific Spring Boot starter

Alternatively, you can use the Hibernate-specific Spring Boot starter, which provides a more fine-grained control over the Hibernate configuration. To use this starter, add the following dependency to your project's `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-hibernate</artifactId>
</dependency>
```

## Configuring Hibernate with Spring Boot

Once you have added the required dependencies, you can configure Hibernate by adding the following properties to your `application.properties` file:

```properties
# Hibernate settings
spring.jpa.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
spring.jpa.hibernate.ddl-auto=update
```

The `spring.jpa.hibernate.dialect` property configures the Hibernate dialect to use. This tells Hibernate how to translate the Java objects into SQL statements.

The `spring.jpa.hibernate.ddl-auto` property configures Hibernate's automatic DDL mode. This tells Hibernate to automatically generate the required SQL schema for the entities. The `update` mode will update the schema if it has changed, but will not create it if it does not exist.

## Creating a Hibernate entity

To create a Hibernate entity, you simply need to create a Java class that represents a table in your database. For example, the following code defines a `User` entity:

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

The `@Entity` annotation marks the class as a Hibernate entity. The `@Id` annotation marks the `id` field as the primary key. The `@Column` annotation marks the `name` field as a column in the database table.

## Creating a Hibernate repository

To create a Hibernate repository, you simply need to create an interface that extends the `CrudRepository` interface. For example, the following code defines a `UserRepository`:

```java
public interface UserRepository extends CrudRepository<User, Long> {
}
```

This repository provides basic CRUD operations for the `User` entity.

## Injecting the repository into a service

To inject the repository into a service, you can use the `@Autowired` annotation. For example, the following code injects the `UserRepository` into a `UserService`:

```java
@Service
public class UserService {
 
    @Autowired
    private UserRepository userRepository;
 
    // ...
}
```

## Using the repository

Once you have injected the repository into a service, you can use it to perform CRUD operations on the entities. For example, the following code creates a new `User`:

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

## References

- [Hibernate](https://hibernate.org/)
- [Spring Boot](https://spring.io/projects/spring-boot)
- [Spring Data JPA](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#reference)
- [Spring Data Hibernate](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-sql.html#boot-features-hibernate)