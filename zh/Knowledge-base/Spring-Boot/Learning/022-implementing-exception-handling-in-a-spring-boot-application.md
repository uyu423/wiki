---
title: 022: 在 Spring Boot 应用程序中实现异常处理
description: 
published: true
date: 2023-02-03T14:32:37.803Z
tags: 
editor: markdown
dateCreated: 2023-02-03T14:32:36.230Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [022: Implementing exception handling in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/022-implementing-exception-handling-in-a-spring-boot-application)
{.links-list}


# 在 Spring Boot 应用程序中实现异常处理

异常处理是任何应用程序的关键部分。在 Spring Boot 应用程序中，有几种方法可以实现异常处理。

在这篇文章中，我们将回顾 Spring Boot 应用程序中异常处理的一些基础知识。我们将从一个简单的示例开始，然后我们将讨论一些更高级的主题。

## 基本异常处理

在 Spring Boot 应用程序中处理异常的最简单方法是使用 @ControllerAdvice 注释。这个注解可以用在一个类上来全局处理异常。

例如，假设我们有一个返回用户列表的简单控制器：

```java
@RestController
public class UserController {
 
    @GetMapping("/users")
    public List<User> getUsers() {
        // ...
    }
}
```

如果在获取用户列表时出现错误，我们可以使用@ControllerAdvice 注解来处理异常：

```java
@ControllerAdvice
public class ExceptionHandlerController {
 
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleException(Exception ex) {
        // ...
    }
}
```

在上面的示例中，我们使用@ExceptionHandler 注释来处理控制器中发生的任何异常。我们还使用 @ControllerAdvice 注释来确保我们的异常处理程序在全局范围内应用。

## 高级异常处理

在某些情况下，您可能希望更好地控制异常的处理方式。例如，您可能希望针对不同类型的异常返回不同的响应。

在 Spring Boot 中，可以使用@ExceptionHandler 注解来处理特定类型的异常。例如，假设我们有一个返回用户列表的控制器：

```java
@RestController
public class UserController {
 
    @GetMapping("/users")
    public List<User> getUsers() {
        // ...
    }
}
```

如果在获取用户列表时出现错误，我们可以使用@ExceptionHandler 注解来处理异常：

```java
@ControllerAdvice
public class ExceptionHandlerController {
 
    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleUserNotFoundException(UserNotFoundException ex) {
        // ...
    }
 
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleException(Exception ex) {
        // ...
    }
}
```

在上面的示例中，我们使用 @ExceptionHandler 注释来处理特定类型的异常。我们还使用 @ControllerAdvice 注释来确保我们的异常处理程序在全局范围内应用。

## 结论

异常处理是任何应用程序的关键部分。在 Spring Boot 应用程序中，有几种方法可以实现异常处理。

在本文中，我们介绍了 Spring Boot 应用程序中异常处理的一些基础知识。我们从一个简单的示例开始，然后讨论了一些更高级的主题。