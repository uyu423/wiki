---
title: 使用 Spring Boot 验证输入
description: 
published: true
date: 2023-02-07T04:32:29.136Z
tags: 
editor: markdown
dateCreated: 2023-02-07T04:32:27.463Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Validating Input with Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/validating-input-with-spring-boot)
{.links-list}


# 使用 Spring Boot 验证输入

验证输入是任何应用程序的关键部分。如果不这样做，可能会导致各种安全和稳定性问题。

Spring Boot 提供了多种验证输入的方法。在本文中，我们将了解一些最流行的方法。

## JSR-303

Java 规范请求 303 或 JSR-303 是 Java 中的验证规范。它是 Spring Boot 应用程序中输入验证的流行选择。

要使用 JSR-303，我们首先需要将以下依赖项添加到我们的 pom.xml 中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

然后，我们可以在我们的请求映射上创建一个带有“@Valid”注释的“@Controller”：

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

`@Valid` 注释将触发输入验证。我们还可以使用 @Validated 注释来触发特定字段的验证：

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Validated({FirstGroup.class, SecondGroup.class}) @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

我们还可以验证方法参数：

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @RequestParam("id") Long id) {
        // ...
    }

}
```

JSR-303 提供了许多强大的功能，但它可能非常冗长。

## 休眠验证器

Hibernate Validator 是一个符合 JSR-303 的验证框架。它是 Spring Boot 应用程序中输入验证的流行选择。

要使用 Hibernate Validator，我们首先需要将以下依赖项添加到我们的 pom.xml 中：

```xml
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-validator</artifactId>
</dependency>
```

然后，我们可以在我们的请求映射上创建一个带有“@Valid”注释的“@Controller”：

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

`@Valid` 注释将触发输入验证。我们还可以使用 @Validated 注释来触发特定字段的验证：

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Validated({FirstGroup.class, SecondGroup.class}) @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

我们还可以验证方法参数：

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @RequestParam("id") Long id) {
        // ...
    }

}
```

Hibernate Validator 提供了许多强大的功能，但它可能非常冗长。

## 春季验证

Spring Validation 是一个建立在 JSR-303 和 Hibernate Validator 之上的验证框架。它是 Spring Boot 应用程序中输入验证的流行选择。

要使用 Spring Validation，我们首先需要将以下依赖项添加到我们的 pom.xml 中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

然后，我们可以在我们的请求映射上创建一个带有“@Valid”注释的“@Controller”：

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

`@Valid` 注释将触发输入验证。我们还可以使用 @Validated 注释来触发特定字段的验证：

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Validated({FirstGroup.class, SecondGroup.class}) @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

我们还可以验证方法参数：

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @RequestParam("id") Long id) {
        // ...
    }

}
```

Spring Validation 提供了许多强大的功能，但它可能非常冗长。

## 结论

有多种方法可以在 Spring Boot 应用程序中验证输入。在本文中，我们研究了一些最流行的方法。