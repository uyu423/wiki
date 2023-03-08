---
title: Reactive Programming with Spring WebFlux
description: 
published: true
date: 2023-01-31T19:04:50.633Z
tags: 
editor: markdown
dateCreated: 2023-01-31T19:04:48.920Z
---

- [Spring WebFlux를 사용한 리액티브 프로그래밍***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/reactive-programming-with-spring-webflux)
{.links-list}
- [Spring WebFlux を使用したリアクティブ プログラミング***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/reactive-programming-with-spring-webflux)
{.links-list}
- [使用 Spring WebFlux 进行响应式编程***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/reactive-programming-with-spring-webflux)
{.links-list}



# Reactive Programming with Spring WebFlux

Reactive programming is a declarative programming paradigm concerned with data streams and the propagation of change. This means that it becomes possible to express static (e.g. arrays) or dynamic (e.g. event emitters) data streams with ease, and also that an application can react to changes in the data streams.

The need for reactive programming has arisen due to the increasing demand for more responsive and resilient applications. In the past, applications were often built as monoliths, with all functionality contained within a single codebase. This made it difficult to achieve responsiveness, as a change in one part of the codebase could have unforeseen consequences in another part.

Reactive programming allows for a more modular approach, where different parts of the application can be decoupled and built independently. This makes it easier to create responsive applications, as changes in one part of the codebase are less likely to affect other parts.

Spring WebFlux is a reactive web framework that is built on top of the Reactor project. It allows you to build web applications that are more responsive and resilient, and can be easily integrated with other reactive libraries.

In this article, we will look at how to use Spring WebFlux to build a reactive web application. We will also look at some of the benefits of using a reactive approach.

## What is Reactive Programming?

Reactive programming is a declarative programming paradigm concerned with data streams and the propagation of change. This means that it becomes possible to express static (e.g. arrays) or dynamic (e.g. event emitters) data streams with ease, and also that an application can react to changes in the data streams.

The need for reactive programming has arisen due to the increasing demand for more responsive and resilient applications. In the past, applications were often built as monoliths, with all functionality contained within a single codebase. This made it difficult to achieve responsiveness, as a change in one part of the codebase could have unforeseen consequences in another part.

Reactive programming allows for a more modular approach, where different parts of the application can be decoupled and built independently. This makes it easier to create responsive applications, as changes in one part of the codebase are less likely to affect other parts.

Reactive programming is based on the Observer pattern, which is a way of designing applications around the notion of events and event-handlers. In the Observer pattern, an object (known as the Subject) maintains a list of observers, and notifies them when something interesting happens. The observers can then take appropriate action.

![Reactive Programming](https://i.imgur.com/EwP52Uv.png)

In reactive programming, the data streams are the Subjects, and the observers are the consumers of the data. The consumers can choose to react to the data in any way they see fit.

Reactive programming has its roots in functional programming, and shares many of the same principles. In particular, reactive programming is based on the idea of declarative programming, where the programmer declares what they want to happen, rather than how it should happen.

## What is Spring WebFlux?

Spring WebFlux is a reactive web framework that is built on top of the Reactor project. It allows you to build web applications that are more responsive and resilient, and can be easily integrated with other reactive libraries.

Spring WebFlux is an alternative to the traditional Spring MVC model. In the traditional model, a web request is handled by a single thread, and the response is returned when the thread is finished. This can lead to performance issues, as the thread is blocked while waiting for the response.

In the reactive model, a web request is handled by a non-blocking thread, and the response is returned immediately. This allows for better performance, as the thread is not blocked while waiting for the response.

![Spring WebFlux](https://i.imgur.com/5B6qDfu.png)

Spring WebFlux also supports backpressure, which is a way of managing the flow of data so that the producer does not produce more data than the consumer can handle. This is important in situations where the consumer is not able to keep up with the producer, as it prevents the consumer from being overwhelmed.

Backpressure is managed by the Reactive Streams specification, which is a set of standards for reactive programming. Spring WebFlux implements the Reactive Streams specification, and provides backpressure support out of the box.

## Getting Started

In this section, we will look at how to get started with Spring WebFlux. We will create a simple web application that will display a list of users.

### Prerequisites

Before we get started, we need to make sure that we have the following tools installed:

* Java 8 or higher
* Maven 3.5 or higher

### Create the Project

We can create the project using the Spring Initializr tool. This tool allows us to select the dependencies that we need for our project, and generates the project structure for us.

We need to select the following dependencies:

* Web - This dependency includes the WebFlux framework, and is required for building web applications.
* Lombok - This dependency is used for reducing boilerplate code, and is optional.

Once the dependencies have been selected, we can generate the project structure.

### Add the Dependencies

Next, we need to add the dependencies that we selected in the previous step to the `pom.xml` file.

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-webflux</artifactId>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>
```

### Create the User Model

We need to create a model to represent the user data. We can do this by creating a `User.java` file in the `src/main/java/com/example` directory.

```java
@Data
public class User {
    private String id;
    private String name;
    private String email;
}
```

We have used the `@Data` annotation from the Lombok library to reduce boilerplate code. This annotation will generate getters, setters, and a toString method for us.

### Create the User Service

Next, we need to create a service to fetch the user data. We can do this by creating a `UserService.java` file in the `src/main/java/com/example` directory.

```java
@Service
public class UserService {
    private List<User> users = new ArrayList<>();

    public UserService() {
        this.users.add(new User("1", "John Doe", "john.doe@example.com"));
        this.users.add(new User("2", "Jane Doe", "jane.doe@example.com"));
    }

    public List<User> getUsers() {
        return this.users;
    }
}
```

In this service, we have created a list of users that we can use to fetch the data.

### Create the User Controller

Next, we need to create a controller to handle the web requests. We can do this by creating a `UserController.java` file in the `src/main/java/com/example` directory.

```java
@RestController
@RequestMapping("/users")
public class UserController {
    private UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping
    public Flux<User> getUsers() {
        return this.userService.getUsers()
                .stream()
                .map(user -> User.builder()
                        .id(user.getId())
                        .name(user.getName())
                        .email(user.getEmail())
                        .build())
                .collect(Collectors.toList())
                .flux();
    }
}
```

In this controller, we have mapped the `/users` path to the `getUsers()` method. This method fetches the list of users from the service, and returns it as a `Flux`.

A `Flux` is a stream of data that can be emitted asynchronously. It is similar to an `Observable` in RxJava.

### Run the Application

We can now run the application by executing the following command:

```
./mvnw spring-boot:run
```

We can then access the application at `http://localhost:8080/users`.

## Conclusion

In this article, we have looked at how to use Spring WebFlux to build a reactive web application. We have also looked at some of the benefits of using a reactive approach.

If you would like to learn more about reactive programming, here are some resources that you may find helpful:

* [Reactive Programming](https://en.wikipedia.org/wiki/Reactive_programming)
* [Reactive Streams](http://www.reactive-streams.org/)
* [Reactor](https://projectreactor.io/)
* [Spring WebFlux](https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html)