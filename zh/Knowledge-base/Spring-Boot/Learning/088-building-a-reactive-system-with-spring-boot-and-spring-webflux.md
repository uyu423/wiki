---
title: 088：使用 Spring Boot 和 Spring WebFlux 构建响应式系统
description: 
published: true
date: 2023-02-05T18:32:33.271Z
tags: 
editor: markdown
dateCreated: 2023-02-05T18:32:31.612Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [088: Building a Reactive System with Spring Boot and Spring WebFlux***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/088-building-a-reactive-system-with-spring-boot-and-spring-webflux)
{.links-list}


# 088：使用 Spring Boot 和 Spring WebFlux 构建响应式系统

在本文中，我们将学习如何使用 Spring Boot 和 Spring WebFlux 构建响应式系统。

反应式系统是那些使用反应式宣言原则构建的系统。这些系统是响应式的、有弹性的、有弹性的和消息驱动的。

在反应式系统中，每个组件都是消息生产者和消息消费者。这些组件使用消息异步地相互通信。

消息驱动系统比传统系统更具可扩展性和弹性，因为它们可以在不影响系统其余部分的情况下处理故障。

Spring Boot 是一个框架，可以轻松创建独立的、生产级的基于 Spring 的应用程序。

Spring WebFlux 是一个反应式 Web 框架，用于使用反应式编程模型构建 Web 应用程序。

在本文中，我们将学习如何使用 Spring Boot 和 Spring WebFlux 构建一个简单的响应式系统。

## 创建一个 Spring Boot 项目

我们可以使用 Spring Initializr 创建 Spring Boot 项目。我们需要选择以下依赖项：

- 网络
- 反应网络
- 龙目岛

Lombok 是一个库，可用于减少我们应用程序中的样板代码。

## 编写代码

我们将从创建一个返回字符串列表的简单控制器开始。

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public List<String> hello() {
        return Arrays.asList("Hello", "World");
    }
}
```

在控制器中，我们用“@GetMapping”注释对“hello()”方法进行了注释。此注释将 `hello()` 方法映射到 `/hello` 路径。

我们还使用 `@RestController` 注释对 `HelloController` 类进行了注释。此注释将类标记为控制器并使 Spring 能够处理 Web 请求。

`@RestController` 注解是一个方便的注解，相当于用`@Controller` 和`@ResponseBody` 注解来注解一个类。

`@ResponseBody` 注释告诉 Spring 将 `hello()` 方法的返回值序列化为 JSON 并将其发送到响应主体中。

当我们运行应用程序并向 /hello 路径发出请求时，我们应该看到以下 JSON 响应：

```json
["Hello","World"]
```

## 使 `hello()` 方法具有反应性

我们可以通过返回 `Mono<List<String>>` 而不是 `List<String>` 来使 `hello()` 方法具有反应性。

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public Mono<List<String>> hello() {
        return Mono.just(Arrays.asList("Hello", "World"));
    }
}
```

`Mono` 类表示 0 或 1 元素的流。在这种情况下，我们使用它来包装我们的字符串列表。

`just()` 方法创建一个包含指定元素的 `Mono`。

当我们向 `/hello` 路径发出请求时，我们应该会看到与之前相同的 JSON 响应。

## 使 `hello()` 方法异步

我们可以使用 `publishOn()` 运算符使 `hello()` 方法异步。

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

`publishOn()` 运算符告诉 Spring 在指定的调度程序上发布流的元素。在这种情况下，我们使用的是 `elastic` 调度程序，它是一个异步调度程序。

当我们向 `/hello` 路径发出请求时，我们应该会看到与之前相同的 JSON 响应。

## 使 `hello()` 方法成为非阻塞的

我们可以使用 subscribeOn() 运算符使 `hello()` 方法成为非阻塞的。

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

`subscribeOn()` 运算符告诉 Spring 在指定的调度程序上订阅流。在这种情况下，我们使用的是 `elastic` 调度程序，它是一个异步调度程序。

当我们向 `/hello` 路径发出请求时，我们应该会看到与之前相同的 JSON 响应。

## 结论

在本文中，我们学习了如何使用 Spring Boot 和 Spring WebFlux 构建响应式系统。我们还学习了如何使 `hello()` 方法具有反应性、异步性和非阻塞性。