---
title: 083: Building a CRUD Application with Spring Boot and JPA
description: 
published: true
date: 2023-02-05T13:32:29.028Z
tags: 
editor: markdown
dateCreated: 2023-02-05T13:32:22.887Z
---

- [083: Creación de una aplicación CRUD con Spring Boot y JPA***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/083-building-a-crud-application-with-spring-boot-and-jpa)
{.links-list}
- [083：使用 Spring Boot 和 JPA 构建 CRUD 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/083-building-a-crud-application-with-spring-boot-and-jpa)
{.links-list}
- [083: Spring Boot와 JPA로 CRUD 애플리케이션 구축***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/083-building-a-crud-application-with-spring-boot-and-jpa)
{.links-list}


083: Building a CRUD Application with Spring Boot and JPA
========================================================

In this article, we'll learn how to build a CRUD application with Spring Boot and JPA.

We'll first create a resource representation class. This class will be used to represent our data in the application.

Next, we'll create a repository interface. This interface will be used to access our data.

Finally, we'll create a controller. This controller will be used to handle HTTP requests and responses.

Creating the Resource Representation Class
------------------------------------------

The first step is to create a resource representation class. This class will be used to represent our data in the application.

We'll start by creating a class called `User`. This class will have three fields: `id`, `name`, and `email`.


    public class User {
    
        private Long id;
        private String name;
        private String email;
    
        // Getters and setters
    
    }


Creating the Repository Interface
---------------------------------

Next, we'll create a repository interface. This interface will be used to access our data.

We'll start by creating an interface called `UserRepository`. This interface will extend `JpaRepository`. `JpaRepository` is a Spring Data JPA interface that provides CRUD operations for us.


    public interface UserRepository extends JpaRepository<User, Long> {
    
    }


Creating the Controller
-----------------------

Finally, we'll create a controller. This controller will be used to handle HTTP requests and responses.

We'll start by creating a class called `UserController`. This class will have two methods: `getAllUsers` and `createUser`.

The `getAllUsers` method will be used to handle a GET request to `/users`. This method will return a list of all users in the database.

The `createUser` method will be used to handle a POST request to `/users`. This method will create a new user in the database.


    @RestController
    public class UserController {
    
        @Autowired
        private UserRepository userRepository;
    
        @GetMapping("/users")
        public List<User> getAllUsers() {
            return userRepository.findAll();
        }
    
        @PostMapping("/users")
        public User createUser(@RequestBody User user) {
            return userRepository.save(user);
        }
    
    }


Testing the Application
-----------------------

Now that we've created our resource representation class, repository interface, and controller, we're ready to test our application.

We'll start by creating a `User` object.


    User user = new User();
    user.setName("John Doe");
    user.setEmail("john.doe@example.com");


Next, we'll call the `createUser` method.


    user = userController.createUser(user);


Finally, we'll call the `getAllUsers` method.


    List<User> users = userController.getAllUsers();
    assertThat(users).contains(user);


If everything went well, you should see the following output:


    [
        {
            "id": 1,
            "name": "John Doe",
            "email": "john.doe@example.com"
        }
    ]


You can find the complete source code for this example on GitHub.