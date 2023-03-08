---
title: Spring Boot开发中的原型模式
description: 
published: true
date: 2023-01-31T15:43:33.013Z
tags: 
editor: markdown
dateCreated: 2023-01-31T15:43:31.386Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [The Prototype Pattern in Spring Boot Development***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-prototype-pattern-in-spring-boot-development)
{.links-list}


# Spring Boot开发中的原型模式

Prototype 模式是一种创建型设计模式，它允许您克隆一个对象，同时避免从头开始创建一个新对象的开销。在 Spring 中，Prototype 作用域用于创建只能使用一次的 bean。当您需要创建大量具有相同配置的 bean 时，这会很有用。

当您创建原型 bean 时，Spring 将为每个请求创建一个新的 bean 实例。这对于创建成本高昂的 bean 很有用，例如需要从数据库中查询的对象。

要使用 Prototype 作用域，您可以使用 @Scope("prototype") 注释来注释您的 bean 类。这将告诉 Spring 为每个请求创建一个新的 bean 实例。

例如，假设您有一个需要查询数据库的 bean。您可以使用 @Scope("prototype") 批注来批注此 bean，以确保为每个请求创建一个新实例。这样，每个请求都会获得自己的数据库连接。

```java
@Scope("prototype")
@Component
public class MyBean {
   ...
}
```

如果需要将原型 bean 注入单例 bean，可以使用 @Autowired 注解。这将告诉 Spring 为每个请求创建原型 bean 的新实例。

```java
@Autowired
MyBean myBean;
```

您还可以使用 @Resource 注释将原型 bean 注入到单例 bean 中。这将告诉 Spring 为每个请求创建原型 bean 的新实例。

```java
@Resource(name="myBean")
MyBean myBean;
```

当您使用 Prototype 范围时，重要的是要记住每个请求都将获得它自己的 bean 实例。这意味着您存储在 bean 中的任何状态都不会在请求之间共享。

如果需要在原型 bean 之间共享状态，可以使用 ThreadLocal 类。此类允许您以线程安全的方式存储数据。

```java
@Scope("prototype")
@Component
public class MyBean {
   private ThreadLocal<Integer> count = new ThreadLocal<Integer>();

   public void increment() {
      count.set(count.get() + 1);
   }

   public int getCount() {
      return count.get();
   }
}
```

在上面的示例中，我们使用 ThreadLocal 来存储计数。这将确保每个请求都有自己的计数。

同样重要的是要注意 Prototype 范围不是继承的。这意味着，如果您有一个使用 @Scope("prototype") 注释进行注释的 bean，并且将其注入到子 bean 中，则该子 bean 将不是原型。

```java
@Component
@Scope("prototype")
public class ParentBean {
   ...
}

@Component
public class ChildBean {
   @Autowired
   private ParentBean parentBean;

   ...
}
```

在上面的示例中，ChildBean 将不是原型。这是因为 @Scope("prototype") 注解没有被继承。

如果需要让子 bean 成为原型，可以使用 @Scope("prototype") 注解对其进行注解。

```java
@Component
@Scope("prototype")
public class ParentBean {
   ...
}

@Component
@Scope("prototype")
public class ChildBean {
   @Autowired
   private ParentBean parentBean;

   ...
}
```

在上面的示例中，ChildBean 将是一个原型。这是因为 @Scope("prototype") 注解应用于 ChildBean 类。

原型模式是一个强大的工具，可用于提高应用程序的性能。如果使用得当，它可以帮助您避免从头开始创建新对象的开销。