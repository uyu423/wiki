---
title: Building a CRUD Application with Spring Boot
description: 
published: true
date: 2023-02-06T08:33:30.087Z
tags: 
editor: markdown
dateCreated: 2023-02-06T08:33:24.339Z
---

- [Creación de una aplicación CRUD con Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/building-a-crud-application-with-spring-boot)
{.links-list}
- [使用 Spring Boot 构建 CRUD 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/building-a-crud-application-with-spring-boot)
{.links-list}
- [Spring Boot로 CRUD 애플리케이션 구축***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/building-a-crud-application-with-spring-boot)
{.links-list}


# Building a CRUD Application with Spring Boot

Developing a CRUD (Create, Read, Update, Delete) application is a common requirement when building web applications. Spring Boot makes it easy to create stand-alone, production-grade Spring-based applications that you can "just run". In this article, we'll focus on how to create a CRUD application with Spring Boot.

## What is Spring Boot?

Spring Boot is a Java-based framework used to create stand-alone, production-grade Spring-based applications. It takes an opinionated view of the Spring platform and third-party libraries, so you can get started with minimum fuss. Most Spring Boot applications need very little Spring configuration.

## Why use Spring Boot?

SpringBoot provides a number of features that make it easy to develop a web application.

- It can embed Tomcat, Jetty or Undertow directly (no need to deploy WAR files)
- It uses an opinionated approach to configuration
- It reduces boilerplate code
- It provides production-ready features such as metrics, health checks, and externalized configuration

## Getting Started

In this section, we'll show you how to create a simple CRUD application with Spring Boot.

### Prerequisites

To follow along with this article, you'll need the following:

- Java 8 or higher
- Spring Boot 2.0 or higher
- An IDE of your choice
- Maven 3.0 or higher

### Create the Project

First, create a Maven project in your IDE. Make sure to select the "Spring Boot" starter project and the "web" module.

![Create Spring Boot project](https://i.imgur.com/5BkRJN4.png)

### Add Dependencies

Next, we need to add a few dependencies to our `pom.xml` file.

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <scope>runtime</scope>
    </dependency>
</dependencies>
```

The `spring-boot-starter-data-jpa` dependency will add Spring Data and Hibernate to our project. The `spring-boot-starter-web` dependency will add Spring MVC and Tomcat. Finally, the `postgresql` dependency will add the PostgreSQL driver.

### Configure the Database

Next, we need to configure our database. In this example, we'll be using PostgreSQL, but you can use any database you like.

First, create a file called `application.properties` in the `src/main/resources` directory and add the following lines:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=postgres
spring.datasource.password=postgres
spring.jpa.show-sql=true
```

This will configure our application to connect to a PostgreSQL database running on localhost on port 5432. The username and password are both `postgres`.

### Create the Entity

Now, we need to create an entity class. An entity is a Java class that represents a database table. In this example, we'll create a `User` entity.

```java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;
    // ... getters and setters
}
```

The `@Entity` annotation tells Hibernate that this class is an entity. The `@Id` annotation tells Hibernate that the `id` field is the primary key. The `@GeneratedValue` annotation tells Hibernate to generate a unique value for the primary key.

### Create the Repository

Next, we need to create a repository interface. A repository is a Java interface that provides methods for storing and retrieving data. In this example, we'll create a `UserRepository` interface.

```java
public interface UserRepository extends CrudRepository<User, Long> {
}
```

The `CrudRepository` interface provides methods for CRUD operations. We'll be using this interface to implement our `UserRepository`.

### Create the Service

Now, we need to create a service class. A service is a Java class that contains business logic. In this example, we'll create a `UserService` class.

```java
@Service
public class UserService {
    private final UserRepository userRepository;
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
    public User createUser(User user) {
        return userRepository.save(user);
    }
    public User getUserById(Long id) {
        return userRepository.findById(id).orElseThrow(() -> new RuntimeException("User not found"));
    }
    public List<User> getAllUsers() {
        return userRepository.findAll();
    }
    public User updateUser(User user) {
        return userRepository.save(user);
    }
    public void deleteUserById(Long id) {
        userRepository.deleteById(id);
    }
}
```

The `@Service` annotation tells Spring that this is a service bean. The `UserService` class contains methods for creating, retrieving, updating, and deleting users.

### Create the Controller

Next, we need to create a controller class. A controller is a Java class that contains methods for handling HTTP requests. In this example, we'll create a `UserController` class.

```java
@RestController
@RequestMapping("/users")
public class UserController {
    private final UserService userService;
    public UserController(UserService userService) {
        this.userService = userService;
    }
    @PostMapping
    public User createUser(@RequestBody User user) {
        return userService.createUser(user);
    }
    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        return userService.getUserById(id);
    }
    @GetMapping
    public List<User> getAllUsers() {
        return userService.getAllUsers();
    }
    @PutMapping
    public User updateUser(@RequestBody User user) {
        return userService.updateUser(user);
    }
    @DeleteMapping("/{id}")
    public void deleteUserById(@PathVariable Long id) {
        userService.deleteUserById(id);
    }
}
```

The `@RestController` annotation tells Spring that this is a controller bean. The `@RequestMapping` annotation maps HTTP requests to controller methods. The `UserController` class contains methods for creating, retrieving, updating, and deleting users.

### Run the Application

Now that we have our application configured, we can run it. To run the application, simply execute the `main` method in the `Application` class.

```java
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

The application will start up on port 8080.

##Testing the Application

Now that our application is up and running, let's test it out. We can use `curl` to send HTTP requests to our application.

### Create a User

To create a user, we can use the `POST` method.

```
curl -X POST localhost:8080/users -d '{"name": "John Doe", "email": "john.doe@example.com"}' -H "Content-Type: application/json"
```

This will create a user with the name `John Doe` and the email address `john.doe@example.com`.

### Get a User by ID

To retrieve a user, we can use the `GET` method.

```
curl localhost:8080/users/1
```

This will retrieve the user with the ID `1`.

### Get All Users

To retrieve all users, we can use the `GET` method.

```
curl localhost:8080/users
```

This will retrieve all users.

### Update a User

To update a user, we can use the `PUT` method.

```
curl -X PUT localhost:8080/users -d '{"id": "1", "name": "John Doe", "email": "john.doe@example.com"}' -H "Content-Type: application/json"
```

This will update the user with the ID `1`.

### Delete a User

To delete a user, we can use the `DELETE` method.

```
curl -X DELETE localhost:8080/users/1
```

This will delete the user with the ID `1`.

##Conclusion

In this article, we've shown you how to create a simple CRUD application with Spring Boot. We've also shown you how to test the application using `curl`.

Now that you know how to create a CRUD application with Spring Boot, you can create your own applications. You can also find more information on the Spring Boot website: https://spring.io/projects/spring-boot