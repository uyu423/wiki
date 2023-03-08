---
title: Exception Handling in Spring Boot
description: 
published: true
date: 2023-01-31T05:17:25.605Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:17:22.156Z
---

- [Spring Boot의 예외 처리***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/exception-handling-in-spring-boot)
{.links-list}
- [Spring Boot での例外処理***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/exception-handling-in-spring-boot)
{.links-list}
- [Spring Boot 中的异常处理***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/exception-handling-in-spring-boot)
{.links-list}




# Exception Handling in Spring Boot

When developing a spring boot application, it is important to have a robust exception handling mechanism in place. This will ensure that the application can gracefully handle any unexpected errors that may occur during runtime.

There are two types of errors that can occur in a spring boot application:
- Exceptions that are thrown by the application itself.
- Exceptions that are thrown by the underlying system or framework.

It is important to handle both types of exceptions in a spring boot application.

## Exception Handling for Application Exceptions

Application exceptions are those that are thrown by the application itself. These are usually errors that can be anticipated and handled gracefully by the application.

For example, consider a spring boot application that has a RestController endpoint for creating user accounts. If the application receives a request to create a user account with an invalid email address, it should throw a BadRequestException.

```java
@RestController
public class UserController {

    @PostMapping("/users")
    public User createUser(@Valid @RequestBody User user) {
        // logic to create user
    }
}
```

In the above example, if the email address provided in the request body is invalid, the application will throw a BadRequestException.

 To handle this exception, we can use a @ControllerAdvice and a @ExceptionHandler. The @ControllerAdvice annotation is used to define a global exception handler for all controllers in the application. The @ExceptionHandler annotation is used to specify the type of exception that will be handled by the method.

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

In the above example, the handleBadRequestException() method will be invoked when a BadRequestException is thrown by any controller in the application. The exception handling logic can be defined in this method.

It is also possible to define a @RestControllerAdvice instead of a @ControllerAdvice. This will enable the exception handler to return a response body instead of just a status code.

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

In the above example, the handleBadRequestException() method will return a response body with an error message when a BadRequestException is thrown by any controller in the application.

## Exception Handling for System Exceptions

System exceptions are those that are thrown by the underlying system or framework. These are usually unexpected errors that can not be anticipated by the application.

For example, consider a spring boot application that is using a JDBC database. If the database is unavailable, the application will throw a DataAccessException.

To handle this exception, we can use a @ControllerAdvice and a @ExceptionHandler.

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

In the above example, the handleDataAccessException() method will be invoked when a DataAccessException is thrown by any controller in the application. The exception handling logic can be defined in this method.

It is also possible to use a @RestControllerAdvice instead of a @ControllerAdvice. This will enable the exception handler to return a response body instead of just a status code.

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

In the above example, the handleDataAccessException() method will return a response body with an error message when a DataAccessException is thrown by any controller in the application.