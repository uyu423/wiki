---
title: Spring Boot 中的异常处理
description: 
published: true
date: 2023-01-31T05:17:23.813Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:17:22.161Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Exception Handling in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/exception-handling-in-spring-boot)
{.links-list}




# Spring Boot 中的异常处理

在开发 spring boot 应用程序时，重要的是要有一个健壮的异常处理机制。这将确保应用程序可以优雅地处理运行时可能发生的任何意外错误。

Spring Boot 应用程序中可能发生两种类型的错误：
- 应用程序本身抛出的异常。
- 底层系统或框架抛出的异常。

在 spring boot 应用程序中处理这两种类型的异常很重要。

## 应用异常的异常处理

应用程序异常是由应用程序本身抛出的异常。这些通常是应用程序可以预见和妥善处理的错误。

例如，考虑一个具有用于创建用户帐户的 RestController 端点的 spring boot 应用程序。如果应用程序收到使用无效电子邮件地址创建用户帐户的请求，它应该抛出 BadRequestException。

```java
@RestController
public class UserController {

    @PostMapping("/users")
    public User createUser(@Valid @RequestBody User user) {
        // logic to create user
    }
}
```

在上面的示例中，如果请求正文中提供的电子邮件地址无效，应用程序将抛出 BadRequestException。

 为了处理这个异常，我们可以使用@ControllerAdvice 和@ExceptionHandler。 @ControllerAdvice 注释用于为应用程序中的所有控制器定义全局异常处理程序。 @ExceptionHandler 注释用于指定将由该方法处理的异常类型。

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ResponseStatus(HttpStatus.BAD_REQUEST)
    @ExceptionHandler(BadRequestException.class)
    public void handleBadRequestException(BadRequestException e) {
        // exception handling logic
    }
}
```

在上面的示例中，当应用程序中的任何控制器抛出 BadRequestException 时，将调用 handleBadRequestException() 方法。可以在此方法中定义异常处理逻辑。

也可以定义 @RestControllerAdvice 而不是 @ControllerAdvice。这将使异常处理程序能够返回响应主体，而不仅仅是状态代码。

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ResponseBody
    @ExceptionHandler(BadRequestException.class)
    @ResponseStatus(HttpStatus.BAD_REQUEST)
    public Map<String, String> handleBadRequestException(BadRequestException e) {
        Map<String, String> response = new HashMap<>();
        response.put("error", "Invalid email address");
        return response;
    }
}
```

在上面的示例中，当应用程序中的任何控制器抛出 BadRequestException 时， handleBadRequestException() 方法将返回一个带有错误消息的响应主体。

## 系统异常的异常处理

系统异常是由底层系统或框架抛出的异常。这些通常是应用程序无法预料的意外错误。

例如，考虑一个使用 JDBC 数据库的 spring boot 应用程序。如果数据库不可用，应用程序将抛出 DataAccessException。

为了处理这个异常，我们可以使用@ControllerAdvice 和@ExceptionHandler。

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ResponseStatus(HttpStatus.INTERNAL_SERVER_ERROR)
    @ExceptionHandler(DataAccessException.class)
    public void handleDataAccessException(DataAccessException e) {
        // exception handling logic
    }
}
```

在上面的示例中，当应用程序中的任何控制器抛出 DataAccessException 时，将调用 handleDataAccessException() 方法。可以在此方法中定义异常处理逻辑。

也可以使用 @RestControllerAdvice 而不是 @ControllerAdvice。这将使异常处理程序能够返回响应主体，而不仅仅是状态代码。

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ResponseBody
    @ExceptionHandler(DataAccessException.class)
    @ResponseStatus(HttpStatus.INTERNAL_SERVER_ERROR)
    public Map<String, String> handleDataAccessException(DataAccessException e) {
        Map<String, String> response = new HashMap<>();
        response.put("error", "Database unavailable");
        return response;
    }
}
```

在上面的示例中，当应用程序中的任何控制器抛出 DataAccessException 时， handleDataAccessException() 方法将返回一个带有错误消息的响应主体。