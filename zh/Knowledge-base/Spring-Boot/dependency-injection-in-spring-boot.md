---
title: Spring Boot 中的依赖注入
description: 
published: true
date: 2023-01-31T14:57:25.307Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:57:23.775Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Dependency Injection in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/dependency-injection-in-spring-boot)
{.links-list}


# Spring Boot 中的依赖注入

## 介绍

依赖注入 (DI) 是现代编程中广泛使用的一种技术，用于增加应用程序的模块化。通过将依赖项注入到一个对象中，我们可以避免对这些依赖项进行硬编码，并使我们的代码更加灵活，更易于测试和维护。

在本文中，我们将了解 DI 如何在 Spring Framework 的上下文中工作，以及如何使用它来使我们基于 Spring 的应用程序更加模块化和更易于测试。

## 什么是依赖注入？

依赖注入是一种将对象的依赖与对象本身解耦的技术。

在传统编程中，一个对象会对其依赖项进行硬编码，这意味着如果这些依赖项发生变化，则该对象也需要进行更改。这种紧密耦合使代码难以维护和测试。

使用 DI，对象的依赖项在运行时注入到对象中，而不是硬编码。这允许在不更改使用它们的对象的情况下更改依赖项。

## DI 在 Spring 中是如何工作的？

在 Spring 中，DI 是通过使用 @Autowired 注解来完成的。此注释可用于字段、setter 方法和构造函数。当在字段上使用时，该字段将在运行时注入依赖项。当在 setter 方法上使用时，依赖项将在调用时注入到该方法中。当在构造函数上使用时，依赖项将在创建对象时注入到对象中。

@Autowired注解也可以用在用@Configuration注解的方法上，在这种情况下，依赖项将在方法被调用时注入到方法中。

## 如何在 Spring Boot 中使用 DI

Spring Boot 使在您的应用程序中使用 DI 变得容易。要在 Spring Boot 中使用 DI，只需要在要注入依赖的字段、setter 方法或构造函数中添加 @Autowired 注解即可。

例如，假设我们有一个简单的服务，我们想要向其中注入依赖项。我们可以通过使用@Autowired 注释该字段来做到这一点：

```java
@Service
public class MyService {
    @Autowired
    private MyDependency myDependency;
}
```

或者，我们可以注释一个 setter 方法：

```java
@Service
public class MyService {
    private MyDependency myDependency;
    
    @Autowired
    public void setMyDependency(MyDependency myDependency) {
        this.myDependency = myDependency;
    }
}
```

或者，我们可以注释构造函数：

```java
@Service
public class MyService {
    private MyDependency myDependency;
    
    @Autowired
    public MyService(MyDependency myDependency) {
        this.myDependency = myDependency;
    }
}
```

## 结论

依赖注入是一种强大的技术，可用于增加应用程序的模块化。在 Spring 中，DI 是通过使用 @Autowired 注解来完成的。

Spring Boot 使在您的应用程序中使用 DI 变得容易。要在 Spring Boot 中使用 DI，只需要在要注入依赖的字段、setter 方法或构造函数中添加 @Autowired 注解即可。