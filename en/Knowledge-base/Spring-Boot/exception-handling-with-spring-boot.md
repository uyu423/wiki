---
title: Exception Handling with Spring Boot
description: 
published: true
date: 2023-02-17T18:04:27.051Z
tags: 
editor: markdown
dateCreated: 2023-01-30T12:32:23.126Z
---

- [Spring Boot로 예외 처리***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/exception-handling-with-spring-boot)
{.links-list}
- [Spring Boot による例外処理***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/exception-handling-with-spring-boot)
{.links-list}
- [使用 Spring Boot 进行异常处理***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/exception-handling-with-spring-boot)
{.links-list}

    
    
# Exception Handling with Spring Boot

Spring Boot provides a number of utilities for handling exceptions. In this article, we'll take a look at some of the most commonly used techniques.

## Handling Exceptions with @ExceptionHandler

The most common way to handle exceptions in SpringBoot is by using the @ExceptionHandler annotation. This annotation can be applied to controller methods, and it will cause the method to be invoked when an exception of the specified type is thrown by the controller.

For example, let's say we have a controller with the following methods:

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

If an exception is thrown by the someMethod() method, the handleException() method will be invoked. This is because the handleException() method is annotated with @ExceptionHandler, and it can handle exceptions of the Exception type.

It's also possible to annotate a controller method with @ExceptionHandler and specify multiple exception types, like so:

```java
@ExceptionHandler({IOException.class, MyCustomException.class})
public void handleException(Exception e) {
    // ...
}
```

In this case, the handleException() method will be invoked if either an IOException or a MyCustomException is thrown by the controller.

## Handling Exceptions with @ControllerAdvice

If you want to handle exceptions globally for all controllers, you can use the @ControllerAdvice annotation. This annotation can be applied to classes, and it will cause all methods in the class to be invoked when an exception is thrown by a controller.

For example, let's say we have a class with the following methods:

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

In this case, the handleException() method will be invoked whenever an exception is thrown by a controller. Note that the someMethod() method will also be invoked, but it will have no effect on the exception handling.

## Handling Exceptions with @RestControllerAdvice

If you're using Spring's REST support, you can use the @RestControllerAdvice annotation to handle exceptions globally for all REST controllers. This annotation is similar to @ControllerAdvice, but it's specific to REST controllers.

For example, let's say we have a class with the following methods:

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

In this case, the handleException() method will be invoked whenever an exception is thrown by a REST controller. Note that the someMethod() method will also be invoked, but it will have no effect on the exception handling.

## Handling Exceptions with @ResponseStatus

If you want to map an exception to a specific HTTP status code, you can use the @ResponseStatus annotation. This annotation can be applied to controller methods, and it will cause the specified HTTP status code to be returned when the method throws an exception.

For example, let's say we have a controller with the following methods:

```java
@ResponseStatus(HttpStatus.BAD_REQUEST)
public class MyController {
    
    public void someMethod() {
        throw new Exception("something went wrong");
    }
}
```

In this case, the someMethod() method will throw an exception, and the HTTP status code 400 (Bad Request) will be returned to the client.

## Conclusion

Exception handling is a important part of development, and Spring Boot provides a number of utilities for handling exceptions. In this article, we've looked at some of the most commonly used techniques.