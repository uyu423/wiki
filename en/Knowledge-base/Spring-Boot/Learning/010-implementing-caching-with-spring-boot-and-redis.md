---
title: 010: Implementing caching with Spring Boot and Redis
description: 
published: true
date: 2023-02-03T08:43:38.254Z
tags: 
editor: markdown
dateCreated: 2023-02-03T08:43:36.500Z
---

- [010: Implementación de almacenamiento en caché con Spring Boot y Redis***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/010-implementing-caching-with-spring-boot-and-redis)
{.links-list}
- [010: 使用 Spring Boot 和 Redis 实现缓存***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/010-implementing-caching-with-spring-boot-and-redis)
{.links-list}
- [010: Spring Boot 및 Redis로 캐싱 구현***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/010-implementing-caching-with-spring-boot-and-redis)
{.links-list}


# Implementing caching with Spring Boot and Redis

In this post we'll cover how to implement caching with Spring Boot and Redis. We'll start with a brief overview of caching and why it's useful. We'll then look at how to configure Spring Boot to use Redis for caching. Finally, we'll write a simple Spring Boot application to demonstrate how to use Redis for caching.

## What is caching?

Caching is a technique for storing data in a temporary memory location in order to speed up subsequent access to that data. When data is cached, future requests for that data can be served much faster since the data is already in memory.

There are two main types of caching: application caching and database caching. Application caching is used to cache data in the application's memory, while database caching is used to cache data in the database's memory.

## Why use caching?

Caching can be used to improve the performance of an application by reducing the number of times data is read from a slow storage medium such as a database. Caching can also be used to reduce the amount of data that needs to be read from a slow storage medium by storing a copy of the data in a faster storage medium such as memory.

## Configuring Spring Boot to use Redis for caching

Spring Boot provides built-in support for Redis, making it easy to configure Redis for caching. To configure Spring Boot to use Redis for caching, you need to add the following dependency to your project:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

You also need to configure the Redis server host and port in the application.properties file:

```properties
spring.redis.host=localhost
spring.redis.port=6379
```

## Writing a Spring Boot application to use Redis for caching

Now that we've configured Spring Boot to use Redis for caching, let's write a simple Spring Boot application to demonstrate how to use Redis for caching.

We'll start by creating a simple data model to represent a user:

```java
public class User {

    private Long id;
    private String name;
    private Integer age;

    // getters and setters
}
```

Next, we'll create a simple Spring Boot application with a single REST controller to manage users:

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        // code to get user from database
    }

    @PostMapping
    public User createUser(@RequestBody User user) {
        // code to create user in database
    }

    @PutMapping("/{id}")
    public User updateUser(@PathVariable Long id, @RequestBody User user) {
        // code to update user in database
    }

    @DeleteMapping("/{id}")
    public void deleteUser(@PathVariable Long id) {
        // code to delete user from database
    }
}
```

We can now use this controller to manage users in our database. However, each time we call the getUser() method, a database query will be executed to fetch the user from the database. This can be slow, especially if the database is large.

We can improve the performance of our application by caching the results of the getUser() method using Redis. To do this, we'll add the @Cacheable annotation to the getUser() method:

```java
@Cacheable("users")
@GetMapping("/{id}")
public User getUser(@PathVariable Long id) {
    // code to get user from database
}
```

This annotation tells Spring to cache the results of the getUser() method in a Redis cache named "users". The next time the getUser() method is called with the same id, the cached result will be returned instead of executing a database query.

We can also use the @CacheEvict annotation to remove a cached entry:

```java
@CacheEvict("users")
@DeleteMapping("/{id}")
public void deleteUser(@PathVariable Long id) {
    // code to delete user from database
}
```

This annotation tells Spring to remove the cached entry for the user with the given id when the deleteUser() method is called.

## Conclusion

In this post we've covered how to implement caching with Spring Boot and Redis. We've seen how to configure Spring Boot to use Redis for caching, and we've written a simple Spring Boot application to demonstrate how to use Redis for caching.