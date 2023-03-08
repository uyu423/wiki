---
title: 使用 Spring Boot 进行异常处理
description: 
published: true
date: 2023-02-17T18:04:32.806Z
tags: 
editor: markdown
dateCreated: 2023-01-30T12:32:23.167Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Exception Handling with Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/exception-handling-with-spring-boot)
{.links-list}

    
    
# Spring Boot 的异常处理

Spring Boot 提供了许多用于处理异常的实用程序。在本文中，我们将了解一些最常用的技术。

## 使用@ExceptionHandler 处理异常

在 SpringBoot 中处理异常的最常见方法是使用 @ExceptionHandler 注解。该注解可以应用于控制器方法，当控制器抛出指定类型的异常时，它将导致调用该方法。

例如，假设我们有一个具有以下方法的控制器：

```java
public class MyController {
    
    @ExceptionHandler(Exception.class)
    public void handleException(Exception e) {
        // ...
    }
    
    public void someMethod() {
        throw new Exception("something went wrong");
    }
}
```

如果 someMethod() 方法抛出异常，将调用 handleException() 方法。这是因为handleException()方法被@ExceptionHandler注解，可以处理Exception类型的异常。

也可以使用 @ExceptionHandler 注释控制器方法并指定多个异常类型，如下所示：

```java
@ExceptionHandler({IOException.class, MyCustomException.class})
public void handleException(Exception e) {
    // ...
}
```

在这种情况下，如果控制器抛出 IOException 或 MyCustomException，将调用 handleException() 方法。

## 使用@ControllerAdvice 处理异常

如果你想为所有控制器全局处理异常，你可以使用@ControllerAdvice 注解。这个注释可以应用于类，当控制器抛出异常时，它会导致类中的所有方法被调用。

例如，假设我们有一个具有以下方法的类：

```java
@ControllerAdvice
public class GlobalExceptionHandler {
    
    @ExceptionHandler(Exception.class)
    public void handleException(Exception e) {
        // ...
    }
    
    public void someMethod() {
        // ...
    }
}
```

在这种情况下，只要控制器抛出异常，就会调用 handleException() 方法。请注意，也会调用 someMethod() 方法，但它不会影响异常处理。

## 使用@RestControllerAdvice 处理异常

如果您正在使用 Spring 的 REST 支持，则可以使用 @RestControllerAdvice 注释为所有 REST 控制器全局处理异常。此注释类似于@ControllerAdvice，但它特定于 REST 控制器。

例如，假设我们有一个具有以下方法的类：

```java
@RestControllerAdvice
public class GlobalRestExceptionHandler {
    
    @ExceptionHandler(Exception.class)
    public void handleException(Exception e) {
        // ...
    }
    
    public void someMethod() {
        // ...
    }
}
```

在这种情况下，只要 REST 控制器抛出异常，就会调用 handleException() 方法。请注意，也会调用 someMethod() 方法，但它不会影响异常处理。

## 使用@ResponseStatus 处理异常

如果要将异常映射到特定的 HTTP 状态代码，可以使用 @ResponseStatus 注释。该注解可以应用于控制器方法，当方法抛出异常时，它会导致返回指定的 HTTP 状态码。

例如，假设我们有一个具有以下方法的控制器：

```java
@ResponseStatus(HttpStatus.BAD_REQUEST)
public class MyController {
    
    public void someMethod() {
        throw new Exception("something went wrong");
    }
}
```

在这种情况下，someMethod()方法会抛出异常，HTTP状态码400（Bad Request）会返回给客户端。

## 结论

异常处理是开发的重要组成部分，Spring Boot 提供了许多用于处理异常的实用程序。在本文中，我们了解了一些最常用的技术。