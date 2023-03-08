---
title: Quick Started with JPA and Hibernate
description: 
published: true
date: 2023-02-17T18:01:22.256Z
tags: 
editor: markdown
dateCreated: 2023-01-30T01:14:08.293Z
---

- [JPA 및 Hibernate로 빠른 시작***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/quick-started-with-jpa-and-hibernate)
{.links-list}


JPA and Hibernate are two of the most popular technologies forPersistencein the Java industry. JPA is a specification that defines an API for accessing and managing data in a relational database. Hibernate is an implementation of the JPA specification that adds additional features to the specification.

In this quickstart, we'll demonstrate how to use JPA and Hibernate to persist data in a relational database. We'll write a simple Java application that stores data in a MySQL database. The application will have a single entity, called User. Each User will have a first name, last name, and email address.

First, we'll need to create a new project in our IDE. I'm using Eclipse, but any IDE will do. Create a new project, and add the following dependencies to your project:

- HWQL
- JPA
- JTA

These dependencies can be found on Maven Central.

Next, we'll create our User entity. Entities in JPA are POJOs that are annotated with the @Entity annotation. Each entity must have a primary key, which is annotated with the @Id annotation. Our User entity will look like this:

```java
@Entity
public class User {

    @Id
    private Long id;

    private String firstName;
    private String lastName;
    private String email;

    // Getters and setters...
}
```

Now that we have our entity, we need to create a JPA repository for it. JPA repositories are interfaces that extend the JpaRepository interface. They provide methods for retrieving and persisting entities. Our UserRepository will look like this:

```java
public interface UserRepository extends JpaRepository<User, Long> {

}
```

Now that we have our repository, we can write a service that uses it to persist data. Our service will have a method for creating a new user, and a method for retrieving all users. It will look like this:

```java
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public User createUser(User user) {
        return userRepository.save(user);
    }

    public List<User> getUsers() {
        return userRepository.findAll();
    }
}
```

Finally, we'll write a REST controller that exposes our service methods as REST endpoints. Our controller will look like this:

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @Autowired
    private UserService userService;

    @PostMapping
    public User createUser(@RequestBody User user) {
        return userService.createUser(user);
    }

    @GetMapping
    public List<User> getUsers() {
        return userService.getUsers();
    }
}
```

That's it! We've now written a simple Java application that uses JPA and Hibernate to persist data in a relational database.