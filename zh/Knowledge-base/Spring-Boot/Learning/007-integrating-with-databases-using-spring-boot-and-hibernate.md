---
title: 007：使用 Spring Boot 和 Hibernate 与数据库集成
description: 
published: true
date: 2023-02-03T08:04:22.351Z
tags: 
editor: markdown
dateCreated: 2023-02-03T08:04:17.488Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [007: Integrating with databases using Spring Boot and Hibernate***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/007-integrating-with-databases-using-spring-boot-and-hibernate)
{.links-list}


# 007：使用 Spring Boot 和 Hibernate 与数据库集成

## 介绍

在本文中，我们将学习如何使用 Spring Boot 和 Hibernate 与数据库集成。我们将涵盖以下主题：

* 为数据库集成配置 Spring Boot
* 使用 Hibernate 访问数据库
* 创建用于数据库访问的 REST API

## 为数据库集成配置 Spring Boot

Spring Boot 使配置和连接到数据库变得容易。在 application.properties 文件中，我们可以指定数据库驱动程序、URL、用户名和密码。例如，对于 MySQL 数据库，配置如下所示：

```
spring.datasource.driverClassName=com.mysql.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/test
spring.datasource.username=root
spring.datasource.password=password
```

## 使用 Hibernate 访问数据库

Hibernate 是一个强大的 ORM 工具，可以轻松访问和查询数据库。在 Spring Boot 应用程序中，我们可以使用 Hibernate 的 @PersistenceContext 注释将 EntityManager 注入到我们的 bean 中。例如：

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

## 创建用于数据库访问的 REST API

我们可以使用 Spring MVC 轻松创建用于数据库访问的 REST API。例如，我们可以创建一个带有端点的控制器来检索所有实体：

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

## 结论

在本文中，我们学习了如何使用 Spring Boot 和 Hibernate 与数据库集成。我们已经了解了如何为数据库集成配置 Spring Boot 以及如何使用 Hibernate 进行数据库访问。最后，我们创建了一个用于数据库访问的 REST API。