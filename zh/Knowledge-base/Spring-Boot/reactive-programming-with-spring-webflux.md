---
title: 使用 Spring WebFlux 进行响应式编程
description: 
published: true
date: 2023-01-31T19:04:52.651Z
tags: 
editor: markdown
dateCreated: 2023-01-31T19:04:48.927Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Reactive Programming with Spring WebFlux***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/reactive-programming-with-spring-webflux)
{.links-list}



# 使用 Spring WebFlux 进行响应式编程

响应式编程是一种声明式编程范例，涉及数据流和变化的传播。这意味着可以轻松地表达静态（例如数组）或动态（例如事件发射器）数据流，并且应用程序可以对数据流中的变化做出反应。

由于对更具响应性和弹性的应用程序的需求不断增加，因此出现了对反应式编程的需求。过去，应用程序通常构建为单体，所有功能都包含在一个代码库中。这使得难以实现响应能力，因为代码库的一部分发生变化可能会对另一部分产生无法预料的后果。

响应式编程允许采用更加模块化的方法，应用程序的不同部分可以分离并独立构建。这使得创建响应式应用程序变得更加容易，因为代码库的一部分中的更改不太可能影响其他部分。

Spring WebFlux 是一个反应式 Web 框架，它建立在 Reactor 项目之上。它允许您构建响应速度更快、更有弹性的 Web 应用程序，并且可以轻松地与其他响应式库集成。

在本文中，我们将了解如何使用 Spring WebFlux 构建响应式 Web 应用程序。我们还将了解使用反应式方法的一些好处。

## 什么是响应式编程？

响应式编程是一种声明式编程范例，涉及数据流和变化的传播。这意味着可以轻松地表达静态（例如数组）或动态（例如事件发射器）数据流，并且应用程序可以对数据流中的变化做出反应。

由于对更具响应性和弹性的应用程序的需求不断增加，因此出现了对反应式编程的需求。过去，应用程序通常构建为单体，所有功能都包含在一个代码库中。这使得难以实现响应能力，因为代码库的一部分发生变化可能会对另一部分产生无法预料的后果。

响应式编程允许采用更加模块化的方法，应用程序的不同部分可以分离并独立构建。这使得创建响应式应用程序变得更加容易，因为代码库的一部分中的更改不太可能影响其他部分。

响应式编程基于观察者模式，这是一种围绕事件和事件处理程序的概念设计应用程序的方法。在观察者模式中，一个对象（称为主题）维护一个观察者列表，并在有趣的事情发生时通知他们。然后观察者可以采取适当的行动。

![响应式编程](https://i.imgur.com/EwP52Uv.png)

在响应式编程中，数据流是主体，观察者是数据的消费者。消费者可以选择以他们认为合适的任何方式对数据做出反应。

响应式编程起源于函数式编程，并且共享许多相同的原则。特别是，反应式编程基于声明式编程的思想，程序员声明他们想要发生什么，而不是它应该如何发生。

## 什么是 Spring WebFlux？

Spring WebFlux 是一个反应式 Web 框架，它建立在 Reactor 项目之上。它允许您构建响应速度更快、更有弹性的 Web 应用程序，并且可以轻松地与其他响应式库集成。

Spring WebFlux 是传统 Spring MVC 模型的替代方案。在传统模型中，Web 请求由单个线程处理，线程完成后返回响应。这可能会导致性能问题，因为线程在等待响应时被阻塞。

在响应式模型中，Web 请求由非阻塞线程处理，并立即返回响应。这允许更好的性能，因为线程在等待响应时不会被阻塞。

![Spring WebFlux](https://i.imgur.com/5B6qDfu.png)

Spring WebFlux 还支持背压，这是一种管理数据流的方式，这样生产者就不会产生超过消费者可以处理的数据。这在消费者无法跟上生产者的情况下很重要，因为它可以防止消费者不知所措。

背压由 Reactive Streams 规范管理，该规范是反应式编程的一组标准。 Spring WebFlux 实现了 Reactive Streams 规范，并提供开箱即用的背压支持。

## 入门

在本节中，我们将了解如何开始使用 Spring WebFlux。我们将创建一个简单的 Web 应用程序来显示用户列表。

###先决条件

在开始之前，我们需要确保安装了以下工具：

* Java 8 或更高版本
* Maven 3.5 或更高版本

### 创建项目

我们可以使用 Spring Initializr 工具创建项目。该工具允许我们选择项目所需的依赖项，并为我们生成项目结构。

我们需要选择以下依赖项：

* Web - 此依赖项包括 WebFlux 框架，并且是构建 Web 应用程序所必需的。
* Lombok - 此依赖项用于减少样板代码，并且是可选的。

一旦选择了依赖项，我们就可以生成项目结构。

### 添加依赖

接下来，我们需要将我们在上一步中选择的依赖项添加到 `pom.xml` 文件中。

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

### 创建用户模型

我们需要创建一个模型来表示用户数据。我们可以通过在 `src/main/java/com/example` 目录中创建一个 `User.java` 文件来做到这一点。

```java
@Data
public class User {
    private String id;
    private String name;
    private String email;
}
```

我们使用 Lombok 库中的“@Data”注解来减少样板代码。该注解将为我们生成 getter、setter 和一个 toString 方法。

### 创建用户服务

接下来，我们需要创建一个服务来获取用户数据。我们可以通过在 `src/main/java/com/example` 目录中创建一个 `UserService.java` 文件来做到这一点。

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

在此服务中，我们创建了可用于获取数据的用户列表。

### 创建用户控制器

接下来，我们需要创建一个控制器来处理网络请求。我们可以通过在 `src/main/java/com/example` 目录中创建一个 `UserController.java` 文件来做到这一点。

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

在此控制器中，我们已将“/users”路径映射到“getUsers()”方法。此方法从服务中获取用户列表，并将其作为 Flux 返回。

`Flux` 是可以异步发出的数据流。它类似于 RxJava 中的 `Observable`。

### 运行应用程序

我们现在可以通过执行以下命令来运行应用程序：

```
./mvnw spring-boot:run
```

然后我们可以在 http://localhost:8080/users 访问应用程序。

## 结论

在本文中，我们了解了如何使用 Spring WebFlux 构建响应式 Web 应用程序。我们还研究了使用反应式方法的一些好处。

如果您想了解有关反应式编程的更多信息，以下资源可能会对您有所帮助：

* [响应式编程](https://en.wikipedia.org/wiki/Reactive_programming)
* [反应流](http://www.reactive-streams.org/)
* [反应堆](https://projectreactor.io/)
* [Spring WebFlux](https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html)