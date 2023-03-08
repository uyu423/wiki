---
title: Effective Bean Configuration in Spring Boot
description: 
published: true
date: 2023-02-17T18:01:14.125Z
tags: 
editor: markdown
dateCreated: 2023-01-30T00:59:28.637Z
---

- [Spring Boot의 효과적인 Bean 구성***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/effective-bean-configuration-in-spring-boot)
{.links-list}



## 1. Introduction

Beans are the basic building blocks of a Spring application. A Spring bean is an object that is instantiated, assembled, and managed by the Spring IoC container. These beans are created with the configuration metadata that you supply to the container, usually in the form of XML files.

The Spring Framework provides a comprehensive set of features for constructing, configuring, and managing beans within an application. This includes features for dependency injection, bean scopes, and providing lifecycle callbacks.

In Spring Boot, beans are configured automatically based on the contents of your classpath. However, there are a number of ways to further customize the configuration of these beans. In this post, we'll take a look at some of the most effective ways to configure beans in Spring Boot.

## 2. Dependency Injection

Dependency injection is a core feature of the Spring Framework. It is a technique for achieving loose coupling between components in a system. With dependency injection, the dependencies of a particular component are injected into that component by an external entity. This external entity is typically the Spring IoC container.

Dependency injection is used to achieve two primary goals:

* Reduce the tight coupling between components in a system.

* Facilitate the provision of dependencies to a component.

The Spring Framework provides comprehensive support for dependency injection. In Spring Boot, dependency injection is enabled by default. However, there are a few things to keep in mind when using dependency injection in Spring Boot.

First, when using dependency injection, it is generally a good idea to use the @Autowired annotation on your fields. This annotation tells the Spring container to inject a dependency into the annotated field. For example:

```java
@Autowired
private MyBean myBean;
```

In the above example, the MyBean dependency will be injected into the myBean field.

Another thing to keep in mind is that, by default, the Spring container will only inject dependencies that are required. That is, if a dependency is not required, the container will not inject it. This behavior can be changed by using the @Primary annotation. This annotation can be used on a bean to indicate that it should be injected by default. For example:

```java
@Primary
@Bean
public MyBean myBean() {
    return new MyBean();
}
```

In the above example, the myBean bean will be injected by default.

## 3. Bean Scopes

Bean scopes are used to control the visibility and lifetime of a bean within an application. Spring defines five different scopes for beans:

* singleton
* prototype
* request
* session
* global session

The default scope for a bean is singleton. This means that, by default, only one instance of a bean will be created per application. The other scopes are generally used for beans that need to maintain state. For example, the request scope is typically used for beans that need to maintain state for a single HTTP request.

The scope of a bean can be configured using the @Scope annotation. For example:

```java
@Scope("request")
@Bean
public MyBean myBean() {
    return new MyBean();
}
```

In the above example, the myBean bean will be created for each HTTP request.

## 4. Bean Lifecycle

The lifecycle of a Spring bean is managed by the Spring IoC container. When a bean is first created, the container will call the bean's init() method. This method can be used to perform any initialization that is required for the bean. For example:

```java
@Bean
public MyBean myBean() {
    return new MyBean();
}

@PostConstruct
public void init() {
    // Perform any initialization here
}
```

In the above example, the init() method will be called after the myBean bean is created.

When the application is shut down, the container will call the destroy() method on each bean. This method can be used to perform any cleaning up that is required. For example:

```java
@PreDestroy
public void destroy() {
    // Perform any cleanup here
}
```

In the above example, the destroy() method will be called before the application is shut down.

## 5. External Links

* [Spring Boot Documentation - Configuring Beans](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#boot-features-beans)

* [Spring Framework Documentation - Dependency Injection](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#beans-di)

* [Spring Framework Documentation - Bean Scopes](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#beans-factory-scopes)

* [Spring Framework Documentation - Bean Lifecycle](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#beans-factory-lifecycle)