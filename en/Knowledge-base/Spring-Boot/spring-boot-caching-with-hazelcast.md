---
title: Spring Boot Caching with Hazelcast
description: 
published: true
date: 2023-01-31T22:18:03.391Z
tags: 
editor: markdown
dateCreated: 2023-01-31T22:17:59.603Z
---

- [Hazelcast를 사용한 스프링 부트 캐싱***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-caching-with-hazelcast)
{.links-list}
- [Hazelcast を使用した Spring Boot キャッシング***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/spring-boot-caching-with-hazelcast)
{.links-list}
- [使用 Hazelcast 进行 Spring Boot 缓存***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-caching-with-hazelcast)
{.links-list}


# Spring Boot Caching with Hazelcast

Caching is a critical component of any high-performance application. It can improve response times by orders of magnitude and reduce the load on your application servers.

There are many caching solutions available, but one of the most popular is Hazelcast. Hazelcast is an open source distributed caching solution that can be easily integrated with Spring Boot applications.

In this article, we'll take a look at how to use Hazelcast for caching in Spring Boot applications. We'll start with a simple example and then explore some of the more advanced features that Hazelcast has to offer.

## Setting up Hazelcast

The first thing we need to do is set up a Hazelcast instance. We can do this using the Hazelcast Spring Boot Starter.

To add the starter to your project, just add the following dependency to your build file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-hazelcast</artifactId>
</dependency>
```

Once the starter is added to your project, Hazelcast will be automatically configured and started when your application is run.

## Caching with Hazelcast

Now that we have Hazelcast up and running, let's take a look at how we can use it for caching.

We'll start with a simple example. Suppose we have a service that returns a list of users:

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    );

    public List<User> getUsers() {
        return users;
    }
}
```

This service is invoked by a REST controller:

```java
@RestController
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/users")
    public List<User> getUsers() {
        return userService.getUsers();
    }
}
```

We can improve the performance of this controller by caching the result of the `getUsers` method:

```java
@RestController
public class UserController {

    private final UserService userService;

    private final HazelcastInstance hazelcastInstance;

    public UserController(UserService userService, HazelcastInstance hazelcastInstance) {
        this.userService = userService;
        this.hazelcastInstance = hazelcastInstance;
    }

    @GetMapping("/users")
    public List<User> getUsers() {
        List<User> users = hazelcastInstance.getList("users");
        if (users == null) {
            users = userService.getUsers();
            hazelcastInstance.setList("users", users);
        }
        return users;
    }
}
```

In this example, we're using a `List` as our cache. Hazelcast also supports `Map`, `Set`, and `Queue` structures.

We can also cache the results of individual methods:

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    );

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }
}
```

In this case, we don't need to explicitly configure the cache. Spring Boot will automatically configure a cache manager and cache the results of the `getUsers` method.

## Evicting entries from the cache

It's important to keep in mind that, once an entry is cached, it will remain in the cache until it is explicitly evicted. This can lead to stale data being returned if the underlying data changes.

We can evict an entry from the cache using the `@CacheEvict` annotation:

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    );

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }

    @CacheEvict("users")
    public void evictUsers() {
    }
}
```

In this example, we've annotated the `evictUsers` method with `@CacheEvict`. This will cause the `users` cache to be cleared when the method is invoked.

We can also evict all entries from all caches using the `@CacheEvict(allEntries = true)` annotation:

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    );

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }

    @CacheEvict(allEntries = true)
    public void evictAll() {
    }
}
```

## Updating cached entries

We can also update cached entries using the `@CachePut` annotation:

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    );

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }

    @CachePut("users")
    public List<User> updateUsers() {
        return users;
    }
}
```

In this example, the `updateUsers` method is annotated with `@CachePut`. This will cause the `users` cache to be updated when the method is invoked.

## Conclusion

In this article, we've looked at how to use Hazelcast for caching in Spring Boot applications. We've seen how to set up Hazelcast and how to use it for caching data. We've also seen how to evict entries from the cache and how to update cached entries.

Caching is a critical component of any high-performance application. By using Hazelcast, we can easily add caching to our Spring Boot applications.