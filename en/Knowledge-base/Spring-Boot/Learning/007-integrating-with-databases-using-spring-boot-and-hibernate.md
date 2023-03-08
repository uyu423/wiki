---
title: 007: Integrating with databases using Spring Boot and Hibernate
description: 
published: true
date: 2023-02-03T08:04:19.102Z
tags: 
editor: markdown
dateCreated: 2023-02-03T08:04:17.495Z
---

- [007: Integración con bases de datos usando Spring Boot e Hibernate***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/007-integrating-with-databases-using-spring-boot-and-hibernate)
{.links-list}
- [007：使用 Spring Boot 和 Hibernate 与数据库集成***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/007-integrating-with-databases-using-spring-boot-and-hibernate)
{.links-list}
- [007: Spring Boot 및 Hibernate를 사용하여 데이터베이스와 통합***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/007-integrating-with-databases-using-spring-boot-and-hibernate)
{.links-list}


# 007: Integrating with databases using Spring Boot and Hibernate

## Introduction

In this post, we'll learn how to integrate with databases using Spring Boot and Hibernate. We'll cover the following topics:

* Configuring Spring Boot for database integration
* Using Hibernate for database access
* Creating a REST API for database access

## Configuring Spring Boot for database integration

Spring Boot makes it easy to configure and connect to databases. In the application.properties file, we can specify the database driver, URL, username, and password. For example, for a MySQL database, the configuration would look like this:

```
spring.datasource.driverClassName=com.mysql.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/test
spring.datasource.username=root
spring.datasource.password=password
```

## Using Hibernate for database access

Hibernate is a powerful ORM tool that makes it easy to access and query databases. In a Spring Boot application, we can use Hibernate's @PersistenceContext annotation to inject a EntityManager into our beans. For example:

```java
@Service
public class MyService {
    
    @PersistenceContext
    private EntityManager entityManager;
    
    public List<MyEntity> findAll() {
        return entityManager.createQuery("from MyEntity", MyEntity.class)
            .getResultList();
    }
}
```

## Creating a REST API for database access

We can use Spring MVC to easily create a REST API for database access. For example, we can create a controller with an endpoint for retrieving all entities:

```java
@RestController
@RequestMapping("/api/v1/myentities")
public class MyEntityController {
    
    @Autowired
    private MyService myService;
    
    @GetMapping
    public List<MyEntity> findAll() {
        return myService.findAll();
    }
}
```

## Conclusion

In this post, we've learned how to integrate with databases using Spring Boot and Hibernate. We've seen how to configure Spring Boot for database integration and how to use Hibernate for database access. Finally, we've created a REST API for database access.