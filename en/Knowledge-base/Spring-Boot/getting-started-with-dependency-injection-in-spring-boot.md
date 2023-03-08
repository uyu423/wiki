---
title: Getting Started with Dependency Injection in Spring Boot
description: 
published: true
date: 2023-02-17T18:01:11.304Z
tags: 
editor: markdown
dateCreated: 2023-01-30T00:51:02.791Z
---

- [Spring Boot에서 종속성 주입 시작하기***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/getting-started-with-dependency-injection-in-spring-boot)
{.links-list}


# Getting Started with Dependency Injection in Spring Boot

In this article, we'll take a look at what dependency injection is and how it can be used in Spring Boot applications. We'll also look at some of the benefits that come with using dependency injection.

## What is Dependency Injection?

Dependency injection is a technique for managing the dependencies of a software system. A dependency is an object that another object depends on. Injecting dependencies means providing them to an object from outside of that object.

There are two main types of dependency injection: constructor injection and setter injection. With constructor injection, dependencies are provided to an object when that object is created. Setter injection is done by calling a setter method on an object to set a dependency.

## Why Use Dependency Injection?

There are several benefits to using dependency injection.

### Loose Coupling

Dependency injection allows for loose coupling between objects. An object that is loosely coupled to its dependencies can be easily replaced with another object that provides the same dependencies. This makes it easy to change the behavior of an object without having to change the code that uses that object.

### Testability

Dependency injection makes it easy to write unit tests for an object. When an object has its dependencies injected, those dependencies can be replaced with mock objects that simulate the behavior of the real dependencies. This allows for unit tests to be written that don't rely on the real dependencies of an object.

### Flexibility

Dependency injection allows for greater flexibility in how an object is used. An object can be used in different ways by providing different dependencies to it. This can be useful when an object needs to be used in different contexts.

## How to Use Dependency Injection in Spring Boot

Spring Boot provides support for both constructor injection and setter injection.

### Constructor Injection

Constructor injection is the preferred method of dependency injection in Spring Boot. To use constructor injection, simply annotate a constructor with the @Autowired annotation. Spring Boot will then inject dependencies into that constructor.

```java
@Autowired
public MyService(Dependency1 dependency1, Dependency2 dependency2) {
    this.dependency1 = dependency1;
    this.dependency2 = dependency2;
}
```

### Setter Injection

Setter injection can be used by annotating a setter method with the @Autowired annotation. Spring Boot will call that setter method and inject the dependency into the object.

```java
@Autowired
public void setDependency1(Dependency1 dependency1) {
    this.dependency1 = dependency1;
}
```

## Conclusion

Dependency injection is a useful technique for managing the dependencies of a software system. It can be used to achieve loose coupling, improve testability, and increase flexibility. Spring Boot provides support for both constructor injection and setter injection.