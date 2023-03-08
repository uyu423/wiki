---
title: Auto-configuration in Spring Boot: A Deep Dive
description: 
published: true
date: 2023-02-17T18:02:06.264Z
tags: 
editor: markdown
dateCreated: 2023-01-30T08:53:11.957Z
---

- [Spring Boot의 자동 구성: 심층 분석***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/auto-configuration-in-spring-boot-a-deep-dive)
{.links-list}


# Auto-configuration in Spring Boot: A Deep Dive

Spring Boot auto-configuration is a powerful feature that can drastically simplify application configuration. In this post, we'll take a deep dive into how auto-configuration works and how it can be used to simplify your application development.

Spring Boot auto-configuration is triggered by the presence of certain classes on the classpath. When Spring Boot detects one of these classes, it will automatically configure a beans of that type. For example, if Spring Boot detects Hibernate on the classpath, it will automatically configure a Hibernate SessionFactory.

There are a few different ways to customize the auto-configuration process. One is to use the @Conditional annotation to specify conditions under which a particular configuration should be applied. Another is to use the @ConfigurationProperties annotation to map property values to bean properties.

As an example, let's configure a Spring Data JPA repository using auto-configuration. First, we'll add the following dependencies to our build: spring-boot-starter-data-jpa, h2, and mysql.

Next, we'll create a JpaRepository class:

```java
@Repository
public interface MyRepository extends JpaRepository<User, Long> {

}
```

We can then enable auto-configuration by adding the @EnableAutoConfiguration annotation to our Application class:

```java
@SpringBootApplication
@EnableAutoConfiguration
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

Finally, we can configure our application properties:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/test
spring.datasource.username=root
spring.datasource.password=password
spring.jpa.database=MYSQL
spring.jpa.show-sql=true
```

Spring Boot will automatically configure a DataSource and JpaRepository based on the properties we've configured. We can inject our repository into a service class and use it to save and retrieve data:

```java
@Service
public class MyService {

    @Autowired
    private MyRepository repository;

    public void save(User user) {
        repository.save(user);
    }

    public List<User> findAll() {
        return repository.findAll();
    }

}
```

Auto-configuration can be a huge time-saver when developing Spring Boot applications. In most cases, it will Just Work(tm) without any configuration required. When it doesn't, the configuration is usually straightforward.