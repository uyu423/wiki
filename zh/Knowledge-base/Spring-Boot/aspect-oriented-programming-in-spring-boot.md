---
title: Spring Boot 中的面向切面编程
description: 
published: true
date: 2023-02-08T09:33:11.442Z
tags: 
editor: markdown
dateCreated: 2023-02-08T09:33:05.467Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Aspect-Oriented Programming in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/aspect-oriented-programming-in-spring-boot)
{.links-list}


# Spring Boot 中的面向切面编程

面向方面的编程 (AOP) 是一种编程范例，旨在通过允许分离横切关注点来提高模块化。 AOP构成了Spring AOP的核心，用于实现企业应用。

## 什么是 AOP？

面向方面的编程是一种范例，它允许开发人员模块化横切关注点，例如日志记录、安全性和事务管理。这是通过将这些关注点封装到单独的模块（称为方面）中来完成的。然后可以在编译时、加载时甚至运行时将方面编织到主应用程序代码中。

AOP 与面向对象编程 (OOP) 正交，并且可以结合使用。事实上，AOP 的许多好处都可以通过使用 OOP 技术来实现，例如继承和组合。但是，AOP 提供了许多优于 OOP 的优势，我们将在稍后讨论。

## AOP 的好处

### 1.增加模块化

如前所述，AOP 的主要好处之一是增加了模块化。通过将横切关注点模块化为单独的方面，我们可以使我们的代码更加模块化和更容易理解。

### 2.减少代码重复

AOP 的另一个好处是减少了代码重复。横切关注点通常在整个应用程序的多个位置实现。例如，考虑一个日志方面。我们可能希望记录代码中不同位置的方法调用。如果没有 AOP，我们将不得不在每个地方都复制我们的日志记录代码。使用 AOP，我们可以将日志记录代码封装在一个方面，并在整个应用程序中重用它。

### 3. 提高可读性和可维护性

AOP还可以提高我们代码的可读性和可维护性。考虑以下示例：

```java
public void foo() {
  // do something
  bar();
  // do something else
}

public void bar() {
  // do something
}
```

在此示例中，foo() 方法调用 bar() 方法。如果我们想向 foo() 添加一些日志记录代码，我们必须在调用 bar() 之前和之后添加它。使用 AOP，我们可以将此日志记录代码封装在一个方面并将其应用于 foo() 和 bar()。这将导致以下代码：

```java
public void foo() {
  // do something
  // logging code
  bar();
  // logging code
  // do something else
}

public void bar() {
  // logging code
  // do something
  // logging code
}
```

如您所见，日志记录代码现在集中在方面中，这使得 foo() 和 bar() 方法更易于阅读和维护。

### 4. 改进的可测试性

AOP 还可以通过允许我们模拟方面来提高代码的可测试性。例如，考虑一个使用数据库的系统。我们可能想为我们的系统编写一些单元测试，但我们不想实际访问数据库。使用 AOP，我们可以模拟数据库访问方面并在不访问数据库的情况下编写我们的单元测试。

## AOP 的缺点

虽然 AOP 提供了许多好处，但它也有一些缺点。

### 1. 增加的复杂性

AOP 的主要缺点之一是增加了复杂性。 AOP 引入了额外的抽象级别，这会使我们的代码更难理解。

### 2.运行时开销

AOP 的另一个缺点是运行时开销。 AOP 引入的额外抽象会导致内存使用量增加和性能下降。

## 何时使用 AOP？

那么，您应该在下一个项目中使用 AOP 吗？与软件开发中的大多数事情一样，答案是“视情况而定”。

如果您需要 AOP 的好处，例如增加模块化或减少代码重复，那么 AOP 可能非常适合您的项目。但是，如果您正在处理一个对性能有严格要求的项目，AOP 可能不是最佳选择。

## 如何在 Spring Boot 中使用 AOP？

Spring AOP 用于实现企业应用程序。它基于 AOP 联盟并使用 Java 5 语法。

要在 Spring Boot 中使用 AOP，我们需要将 spring-boot-starter-aop 依赖项添加到我们的 pom.xml 中：

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
```

我们还需要通过将 @EnableAspectJAutoProxy 注释添加到我们的主类来在我们的 Spring Boot 应用程序中启用 AOP：

```java
@SpringBootApplication
@EnableAspectJAutoProxy
public class Application {

  public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
  }

}
```

## 创建一个方面

现在我们已经在我们的应用程序中配置了 AOP，让我们创建一个切面。 Spring AOP 中的切面是使用带有 @Aspect 注释的常规 Java 类实现的。

考虑以下示例：

```java
@Aspect
public class MyAspect {

  // methods and pointcuts go here

}
```

在此示例中，我们创建了一个名为 MyAspect 的简单方面。方面可以包含任意数量的方法和切入点。稍后我们将更详细地讨论方法和切入点。

## 应用方面

一旦我们创建了切面，我们就需要将它应用到我们的代码中。这是使用切入点完成的。切入点是匹配连接点的谓词。连接点是我们程序执行中的一个点，例如方法调用。

可以使用正则表达式或 Java 5 语法定义切入点。例如，以下切入点匹配 com.example 包中的所有方法：

```java
@Pointcut("execution(* com.example..*.*(..))")
public void myPointcut() {}
```

myPointcut() 方法只是我们切入点的占位符。我们现在可以使用@Before 和@After 注释将我们的方面应用到我们的代码中。 @Before注解会导致切面在方法调用前执行，@After注解会导致切面在方法调用后执行。

考虑以下示例：

```java
@Aspect
public class MyAspect {

  @Pointcut("execution(* com.example..*.*(..))")
  public void myPointcut() {}

  @Before("myPointcut()")
  public void before(JoinPoint joinPoint) {
    // do something
  }

  @After("myPointcut()")
  public void after(JoinPoint joinPoint) {
    // do something
  }

}
```

在这个例子中，我们定义了一个匹配 com.example 包中所有方法的切入点。我们还定义了一个 before() 方法，它将在调用匹配的方法之前执行，以及一个 after() 方法，将在调用匹配的方法之后执行。

## 结论

在本文中，我们讨论了面向方面的编程以及如何在 Spring Boot 中使用它。我们还看到了如何在 Spring Boot 中创建和应用切面。