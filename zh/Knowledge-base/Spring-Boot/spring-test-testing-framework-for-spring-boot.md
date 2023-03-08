---
title: Spring Test：Spring Boot 的测试框架
description: 
published: true
date: 2023-02-17T18:16:58.360Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:57:36.271Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Spring Test: Testing Framework for Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-test-testing-framework-for-spring-boot)
{.links-list}


# Spring Test：Spring Boot 的测试框架

在本文中，我们将了解 Spring Boot 的 Spring Test 测试框架。我们将从框架的简要概述开始，然后是有关如何使用它的教程。之后，我们将讨论该框架的一些更高级的特性。

## 概述

Spring Test 是 Spring Boot 的测试框架。它旨在帮助您为 Spring Boot 应用程序编写测试。 Spring Test 提供了一种为 Spring Boot 应用程序编写测试的便捷方式。它还提供了许多功能，使您可以轻松地为您的应用程序编写测试。

## 教程

在本教程中，我们将向您展示如何使用 Spring Test 为您的 Spring Boot 应用程序编写测试。我们将使用计算数字阶乘的简单应用程序示例。

首先，我们需要在我们的项目中添加以下依赖：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

接下来，我们需要编写我们的测试用例。我们将使用@Test 注释来标记我们的测试用例。

```java
@Test
public void testFactorial() {
    ...
}
```

在我们的测试用例中，我们需要注入应用程序所需的依赖项。我们可以使用@Autowired 注释来做到这一点。

```java
@Autowired
private FactorialService service;
```

现在，我们可以编写我们的测试用例了。在我们的测试用例中，我们将调用 FactorialService 类的 factorial() 方法。我们将断言结果是正确的。

```java
@Test
public void testFactorial() {
    int result = service.factorial(5);
    assertThat(result, is(120));
}
```

现在，我们可以使用以下命令运行我们的测试用例：

```
$ mvn test
```

如果我们的测试用例通过，我们将看到以下输出：

```
Results :

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

[INFO] 
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ spring-boot-test-example ---
[INFO] 
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running com.example.test.ExampleTest
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.002 sec
[INFO] 
[INFO] Results:
[INFO] 
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO] 
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 2.142 s
[INFO] Finished at: 2015-05-27T16:33:21+0530
[INFO] Final Memory: 10M/155M
[INFO] ------------------------------------------------------------------------
```

## 断言

Spring Test 提供了许多可以在测试用例中使用的断言方法。这些断言方法在 org.springframework.test.util.AssertionErrors 类中定义。

以下是一些最常用的断言方法：

* assertTrue（条件）
* assertFalse(条件)
* assertEquals（预期，实际）
* assertNotEquals（预期，实际）
* assertNull(对象)
* assertNotNull(对象)

您可以在 AssertionErrors 类的 JavaDoc 中找到完整的断言方法列表。

## 异常处理

您可以使用 @Test(expected = Exception.class) 注释来处理测试用例中的预期异常。

例如，如果我们希望 factorial() 方法在输入为负时抛出 IllegalArgumentException，我们可以编写以下测试用例：

```java
@Test(expected = IllegalArgumentException.class)
public void testFactorialNegative() {
    service.factorial(-1);
}
```

## Java 8 Lambda 支持

Spring Test 提供对 Java 8 lambda 表达式的支持。您可以使用 lambda 表达式编写简洁易读的测试用例。

例如，以下测试用例检查数字列表是否已排序：

```java
@Test
public void testSort() {
    List<Integer> numbers = Arrays.asList(5, 4, 3, 2, 1);
    Collections.sort(numbers);
    assertThat(numbers, is(Arrays.asList(1, 2, 3, 4, 5)));
}
```

## 假设

您可以使用 Assume 类对应用程序的状态进行假设。如果不满足假设，则使用假设来跳过测试。

例如，以下测试用例检查数字是否为正数。如果数字为负，则跳过测试用例。

```java
@Test
public void testPositive() {
    int number = -1;
    Assume.assumeTrue(number > 0);
    assertThat(number, is(greaterThan(0)));
}
```

## 测试上下文

TestContext 框架提供了许多可以在测试用例中使用的特性。这些功能包括：

* 测试执行监听器
* 测试支持
* 测试事件发布
* 测试实例后处理
* 测试类的依赖注入

您可以使用这些功能为您的应用程序编写复杂的测试用例。

##结论

在本文中，我们了解了 Spring Boot 的 Spring Test 测试框架。我们已经了解了如何使用该框架为我们的应用程序编写测试。我们还看到了该框架的一些更高级的功能。