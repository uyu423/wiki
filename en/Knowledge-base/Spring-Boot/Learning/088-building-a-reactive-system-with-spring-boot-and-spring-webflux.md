---
title: 088: Building a Reactive System with Spring Boot and Spring WebFlux
description: 
published: true
date: 2023-02-05T18:32:37.254Z
tags: 
editor: markdown
dateCreated: 2023-02-05T18:32:31.618Z
---

- [088: Creación de un sistema reactivo con Spring Boot y Spring WebFlux***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/088-building-a-reactive-system-with-spring-boot-and-spring-webflux)
{.links-list}
- [088：使用 Spring Boot 和 Spring WebFlux 构建响应式系统***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/088-building-a-reactive-system-with-spring-boot-and-spring-webflux)
{.links-list}
- [088: Spring Boot 및 Spring WebFlux를 사용하여 반응형 시스템 구축***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/088-building-a-reactive-system-with-spring-boot-and-spring-webflux)
{.links-list}


# 088: Building a Reactive System with Spring Boot and Spring WebFlux

In this post, we'll learn how to build a reactive system using Spring Boot and Spring WebFlux.

Reactive systems are those that are built using the reactive manifesto principles. These systems are responsive, resilient, elastic, and message-driven.

In a reactive system, every component is a message producer and a message consumer. The components communicate with each other asynchronously using messages.

Message-driven systems are more scalable and resilient than traditional systems because they can handle failures without affecting the rest of the system.

Spring Boot is a framework that makes it easy to create stand-alone, production-grade Spring-based applications.

Spring WebFlux is a reactive web framework for building web applications using the reactive programming model.

In this post, we'll learn how to build a simple reactive system using Spring Boot and Spring WebFlux.

## Creating a Spring Boot Project

We can use the Spring Initializr to create a Spring Boot project. We'll need to select the following dependencies:

- Web
- Reactive Web
- Lombok

Lombok is a library that can be used to reduce the boilerplate code in our application.

## Writing the Code

We'll start by creating a simple controller that returns a list of strings.

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public List<String> hello() {
        return Arrays.asList("Hello", "World");
    }
}
```

In the controller, we've annotated the `hello()` method with the `@GetMapping` annotation. This annotation maps the `hello()` method to the `/hello` path.

We've also annotated the `HelloController` class with the `@RestController` annotation. This annotation marks the class as a controller and enables Spring to handle web requests.

The `@RestController` annotation is a convenience annotation that is equivalent to annotating a class with the `@Controller` and `@ResponseBody` annotations.

The `@ResponseBody` annotation tells Spring to serialize the return value of the `hello()` method as JSON and send it in the response body.

When we run the application and make a request to the `/hello` path, we should see the following JSON response:

```json
["Hello","World"]
```

## Making the `hello()` Method Reactive

We can make the `hello()` method reactive by returning a `Mono<List<String>>` instead of a `List<String>`.

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public Mono<List<String>> hello() {
        return Mono.just(Arrays.asList("Hello", "World"));
    }
}
```

The `Mono` class represents a stream of 0 or 1 element. In this case, we're using it to wrap our list of strings.

The `just()` method creates a `Mono` that contains the specified element.

When we make a request to the `/hello` path, we should see the same JSON response as before.

## Making the `hello()` Method Asynchronous

We can make the `hello()` method asynchronous by using the `publishOn()` operator.

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public Mono<List<String>> hello() {
        return Mono.just(Arrays.asList("Hello", "World"))
                .publishOn(Schedulers.elastic());
    }
}
```

The `publishOn()` operator tells Spring to publish the elements of the stream on the specified Scheduler. In this case, we're using the `elastic` Scheduler, which is an asynchronous Scheduler.

When we make a request to the `/hello` path, we should see the same JSON response as before.

## Making the `hello()` Method Non-Blocking

We can make the `hello()` method non-blocking by using the `subscribeOn()` operator.

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public Mono<List<String>> hello() {
        return Mono.just(Arrays.asList("Hello", "World"))
                .subscribeOn(Schedulers.elastic());
    }
}
```

The `subscribeOn()` operator tells Spring to subscribe to the stream on the specified Scheduler. In this case, we're using the `elastic` Scheduler, which is an asynchronous Scheduler.

When we make a request to the `/hello` path, we should see the same JSON response as before.

## Conclusion

In this post, we've learned how to build a reactive system using Spring Boot and Spring WebFlux. We've also learned how to make the `hello()` method reactive, asynchronous, and non-blocking.