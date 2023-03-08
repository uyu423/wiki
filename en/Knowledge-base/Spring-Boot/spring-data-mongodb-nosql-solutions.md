---
title: Spring Data MongoDB: NoSQL Solutions
description: 
published: true
date: 2023-02-17T18:02:15.858Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:02:43.545Z
---

- [Spring Data MongoDB: NoSQL 솔루션***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/spring-data-mongodb-nosql-solutions)
{.links-list}


# Spring Data MongoDB: NoSQL Solutions

MongoDB is an open-source, document-oriented database management system (DBMS) written in C++. It is a powerful tool for data management and analysis. Spring Data MongoDB is a library that provides a high-level abstraction over MongoDB.

In this article, we will discuss how to use Spring Data MongoDB to develop NoSQL solutions. We will cover the following topics:

* Setting up a MongoDB database
* Developing a Spring Data MongoDB repository
* Querying data with Spring Data MongoDB

## Setting up a MongoDB database

Before we can start developing our Spring Data MongoDB repository, we need to set up a MongoDB database. We can do this using Docker:

```
$ docker run -d -p 27017:27017 --name mongodb mongo
```

This will start a MongoDB container and expose the MongoDB port (27017) on our host machine.

## Developing a Spring Data MongoDB repository

Now that we have our MongoDB database up and running, we can start developing our Spring Data MongoDB repository.

We will start by creating a Maven project with the following dependencies:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.data</groupId>
        <artifactId>spring-data-mongodb</artifactId>
        <version>2.1.11.RELEASE</version>
    </dependency>
</dependencies>
```

Next, we need to configure our Spring Data MongoDB repository. We can do this by adding the following to our `application.properties` file:

```properties
spring.data.mongodb.uri=mongodb://localhost/test
```

This will configure our Spring Data MongoDB repository to connect to our MongoDB database.

Now that we have our Spring Data MongoDB repository configured, we can start developing our Entity class. We will start by creating a `User` class:

```java
@Document
public class User {
 
    @Id
    private String id;
 
    private String name;
 
    private int age;
 
    // Getters and setters
}
```

The `@Document` annotation tells Spring Data MongoDB that this class is a document. The `@Id` annotation tells Spring Data MongoDB that the `id` field is the primary key for this document.

Now that we have our `User` class defined, we can create our `UserRepository` interface:

```java
@Repository
public interface UserRepository extends MongoRepository<User, String> {
 
    User findByName(String name);
 
}
```

The `@Repository` annotation tells Spring that this is a repository. The `MongoRepository` extended interface provides the basic CRUD operations for our `User` class. The `findByName` method is a custom query that we have defined.

Now that we have our `UserRepository` interface defined, we can write our service class:

```java
@Service
public class UserService {
 
    @Autowired
    private UserRepository userRepository;
 
    public User createUser(User user) {
        return userRepository.save(user);
    }
 
    public User findUserById(String id) {
        return userRepository.findById(id).orElse(null);
    }
 
    public User findUserByName(String name) {
        return userRepository.findByName(name);
    }
 
}
```

The `@Service` annotation tells Spring that this is a service class. The `@Autowired` annotation tells Spring to inject the `UserRepository` into this class.

The `createUser` method saves a `User` document to our MongoDB database. The `findUserById` and `findUserByName` methods query our MongoDB database for a `User` document.

Now that we have our service class defined, we can write our controller class:

```java
@RestController
public class UserController {
 
    @Autowired
    private UserService userService;
 
    @PostMapping("/user")
    public User createUser(@RequestBody User user) {
        return userService.createUser(user);
    }
 
    @GetMapping("/user/{id}")
    public User findUserById(@PathVariable String id) {
        return userService.findUserById(id);
    }
 
    @GetMapping("/user/name/{name}")
    public User findUserByName(@PathVariable String name) {
        return userService.findUserByName(name);
    }
 
}
```

The `@RestController` annotation tells Spring that this is a controller class. The `@Autowired` annotation tells Spring to inject the `UserService` into this class.

The `@PostMapping` annotation maps the `createUser` method to the `POST /user` endpoint. The `@GetMapping` annotation maps the `findUserById` and `findUserByName` methods to the `GET /user/{id}` and `GET /user/name/{name}` endpoints respectively.

## Querying data with Spring Data MongoDB

Now that we have our Spring Data MongoDB repository defined, we can start querying our data.

We will start by creating a `User` document:

```java
User user = new User();
user.setName("John Doe");
user.setAge(30);
 
userService.createUser(user);
```

This will create a `User` document in our MongoDB database with the name "John Doe" and the age 30.

We can query our MongoDB database for this `User` document using the `findUserById` and `findUserByName` methods:

```java
User user = userService.findUserById("123");
 
User user = userService.findUserByName("John Doe");
```

Both of these methods will return the `User` document with the name "John Doe" and the age 30.

We can also use the `MongoRepository` interface to query our data. The `MongoRepository` interface provides the following methods:

* `save` - Saves a document to the MongoDB database.
* `insert` - Inserts a document to the MongoDB database.
* `findById` - Finds a document by its id.
* `findAll` - Finds all documents.
* `findAllById` - Finds all documents by their ids.
* `count` - Counts the number of documents.
* `deleteById` - Deletes a document by its id.
* `delete` - Deletes a document.
* `deleteAll` - Deletes all documents.

We can use these methods to query our data in a more flexible way.

## Conclusion

In this article, we have discussed how to use Spring Data MongoDB to develop NoSQL solutions. We have covered the following topics:

* Setting up a MongoDB database
* Developing a Spring Data MongoDB repository
* Querying data with Spring Data MongoDB