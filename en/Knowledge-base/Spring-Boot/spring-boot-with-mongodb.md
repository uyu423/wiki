---
title: Spring Boot with MongoDB
description: 
published: true
date: 2023-02-07T10:32:40.707Z
tags: 
editor: markdown
dateCreated: 2023-02-07T10:32:34.925Z
---

- [Arranque de primavera con MongoDB***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-with-mongodb)
{.links-list}
- [Spring Boot 与 MongoDB***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-with-mongodb)
{.links-list}
- [MongoDB를 사용한 스프링 부트***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-with-mongodb)
{.links-list}


# Spring Boot with MongoDB

Spring Boot is a popular Java-based framework used for building microservices. It offers a simple way to create stand-alone, production-grade Spring based Applications that you can "just run". 

 MongoDB is an open source NoSQL database that uses a document-oriented data model. It is a powerful tool for data management and analysis.

In this article, we will show you how to connect Spring Boot with MongoDB.

## Prerequisites

To follow along with this article, you will need the following:

- Java 8 or higher
- Spring Boot 2.0 or higher
- MongoDB 3.6 or higher

## Creating a Spring Boot Project

We will use Spring Initializr to generate our Spring Boot project. 

Go to http://start.spring.io/, and select the following:

- Project: Maven Project
- Language: Java
- Spring Boot: 2.0.3 
- Group: com.example
- Artifact: demo

Click **Generate Project**.

## Configuring MongoDB

Spring Boot will look for a file called `application.properties` (or `application.yml`) in the `src/main/resources` directory. This is where we will configure our MongoDB connection.

Add the following to your `application.properties` file:

```
spring.data.mongodb.uri=mongodb://localhost/test
```

This will connect to a MongoDB database called `test` on `localhost`. 

If you are using `application.yml`, the configuration will look like this:

```yaml
spring:
  data:
    mongodb:
      uri: mongodb://localhost/test
```

## Creating a MongoDB Repository

Next, we will create a repository interface for our MongoDB database. This will extend the `MongoRepository` interface provided by Spring Data MongoDB.

```java
package com.example.demo.repository;

import org.springframework.data.mongodb.repository.MongoRepository;

import com.example.demo.model.User;

public interface UserRepository extends MongoRepository<User, String> {

}
```

The `UserRepository` interface will perform CRUD operations on the `User` collection in MongoDB.

## Creating a MongoDB Model

Now we will create a `User` class to represent documents in the `User` collection.

```java
package com.example.demo.model;

import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;

@Document
public class User {

    @Id
    private String id;

    private String name;
    private int age;

    // Getters and setters
}
```

The `@Document` annotation tells Spring Data MongoDB that the `User` class is a document in the `User` collection.

The `@Id` annotation marks the `id` field as the primary key for the document.

## Creating a REST Controller

Now we will create a REST controller to expose our MongoDB repository as a REST API.

```java
package com.example.demo.controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

import com.example.demo.model.User;
import com.example.demo.repository.UserRepository;

@RestController
@RequestMapping("/api/v1/users")
public class UserController {

    @Autowired
    private UserRepository userRepository;

    @RequestMapping(method = RequestMethod.GET)
    public List<User> getUsers() {
        return userRepository.findAll();
    }
}
```

The `@RestController` annotation marks the `UserController` class as a REST controller.

The `@RequestMapping` annotation maps HTTP requests to methods in the controller. In this case, the `/api/v1/users` path is mapped to the `getUsers()` method.

The `@Autowired` annotation injects the `UserRepository` into the controller.

The `getUsers()` method retrieves a list of users from the MongoDB database and returns it as JSON.

## Running the Application

To run the application, simply type the following command in your terminal:

```
./mvnw spring-boot:run
```

You should see the following output:

```
...
2017-12-01 10:21:59.593  INFO 85511 --- [           main] s.b.c.e.t.TomcatEmbeddedServletContainer : Tomcat started on port(s): 8080 (http)
2017-12-01 10:21:59.596  INFO 85511 --- [           main] com.example.demo.DemoApplication         : Started DemoApplication in 4.166 seconds (JVM running for 4.681)
```

You can now access the REST API at http://localhost:8080/api/v1/users.

## Conclusion

In this article, we have shown you how to connect Spring Boot with MongoDB. We have also created a simple REST API for CRUD operations on our MongoDB database.

For more information on Spring Boot, please see the following resources:

- [Spring Boot Documentation](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/)
- [Spring Boot with MongoDB Tutorial](https://www.baeldung.com/spring-boot-mongodb)

For more information on MongoDB, please see the following resources:

- [MongoDB Documentation](https://docs.mongodb.com/)
- [MongoDB University](https://university.mongodb.com/)