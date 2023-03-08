---
title: Spring Boot 中的模型-视图-控制器 (MVC) 模式
description: 
published: true
date: 2023-02-01T06:57:43.263Z
tags: 
editor: markdown
dateCreated: 2023-02-01T06:57:41.714Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [The Model-View-Controller (MVC) Pattern in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-model-view-controller-mvc-pattern-in-spring-boot)
{.links-list}



# Spring Boot 中的模型-视图-控制器 (MVC) 模式

模型-视图-控制器 (MVC) 是一种架构软件设计模式，它将应用程序分为三个主要的逻辑组件：模型、视图和控制器。

MVC 模式通常用于 Web 应用程序，以将表示层（视图）与业务逻辑（模型）和控制流（控制器）分开。这种关注点分离使代码库保持清洁和可维护，并使测试和扩展应用程序变得更加容易。

在 Spring MVC 应用程序中，控制器负责处理用户请求并生成适当的响应。视图负责呈现对用户的响应。模型是一种数据结构，用于存储要在视图中显示的数据。

MVC 模式不限于 Web 应用程序。它可以用于任何类型的应用程序，包括桌面、移动和 Web。

## MVC 模式如何工作？

当用户请求进入应用程序时，控制器负责处理它。控制器决定渲染哪个视图，并将要在视图中显示的数据传递给视图。然后视图将响应呈现给用户。

MVC 模式具有以下优点：

- 它分离了应用程序的关注点，使代码库更易于维护和测试。
- 它使扩展应用程序变得更加容易。
- 它使向应用程序添加新功能变得更加容易。

## 在 Spring Boot 中实现 MVC 模式

Spring Boot 是一种流行的 Java Web 应用程序框架，可以轻松创建独立的、生产级的基于 Spring 的应用程序。

Spring Boot MVC 应用程序通常分为以下三层：

- 控制器层
- 服务层
- 存储层

控制器层负责处理用户请求并生成适当的响应。服务层负责业务逻辑。存储库层负责数据访问。

下图展示了三层之间的关系：

![Spring Boot MVC](https://miro.medium.com/max/875/1*tYH4i0zAj7zQLxB7-tscKg.png)

在 Spring Boot MVC 应用程序中，控制器通常是 Spring @RestController。服务层通常是 Spring @Service。存储库层通常是 Spring @Repository。

以下代码片段显示了如何注释控制器、服务和存储库：

```java
@RestController
public class HelloController {

    @RequestMapping("/hello")
    public String hello() {
        return "Hello, world!";
    }
}
```

```java
@Service
public class HelloService {

    public String getHelloMessage() {
        return "Hello, world!";
    }
}
```

```java
@Repository
public class HelloRepository {

    public String getHelloMessage() {
        return "Hello, world!";
    }
}
```

## 结论

MVC 模式是一种流行的软件设计模式，它将应用程序分为三个主要的逻辑组件：模型、视图和控制器。

在 Spring MVC 应用程序中，控制器负责处理用户请求并生成适当的响应。视图负责呈现对用户的响应。模型是一种数据结构，用于存储要在视图中显示的数据。

MVC 模式具有以下优点：

- 它分离了应用程序的关注点，使代码库更易于维护和测试。
- 它使扩展应用程序变得更加容易。
- 它使向应用程序添加新功能变得更加容易。

## 参考

- [模型视图控制器](https://en.wikipedia.org/wiki/Model–view–controller)
- [Spring MVC](https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc)
- [Spring Boot MVC](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-spring-mvc.html)