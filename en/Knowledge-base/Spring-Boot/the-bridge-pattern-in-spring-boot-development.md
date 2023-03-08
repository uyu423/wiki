---
title: The Bridge Pattern in Spring Boot Development
description: 
published: true
date: 2023-02-06T09:17:19.669Z
tags: 
editor: markdown
dateCreated: 2023-02-06T09:17:14.248Z
---

- [El patrón de puente en el desarrollo de Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/the-bridge-pattern-in-spring-boot-development)
{.links-list}
- [Spring Boot开发中的桥接模式***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/the-bridge-pattern-in-spring-boot-development)
{.links-list}
- [Spring Boot 개발의 브리지 패턴***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/the-bridge-pattern-in-spring-boot-development)
{.links-list}


# The Bridge Pattern in Spring Boot Development

One of the most useful design patterns is the bridge pattern. This pattern is useful for decoupling an abstraction from its implementation so that the two can vary independently. The bridge pattern is often used in conjunction with the adapter pattern.

In Spring Boot, the bridge pattern is used to decouple the application from the underlying database. This is done by using the Repository and @Transactional annotations.

The Repository annotation is used to mark a class as a repository. A repository is a class that provides CRUD operations for an entity. The @Transactional annotation is used to mark a method as being part of a transaction.


Here is an example of a repository:

```java
@Repository
public class PersonRepository {
 
    @Transactional
    public void save(Person person) {
        // save person
    }
 
    @Transactional
    public Person findById(Long id) {
        // find person by id
    }
 
    @Transactional
    public void delete(Person person) {
        // delete person
    }
}
```

In the example above, the PersonRepository class is marked as a repository. The save, findById, and delete methods are marked as being part of a transaction.

The bridge pattern is a useful pattern for decoupling an abstraction from its implementation. In Spring Boot, the Repository and @Transactional annotations are used to decouple the application from the underlying database.