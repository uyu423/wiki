---
title: Spring Boot의 예외 처리
description: 
published: true
date: 2023-01-31T05:17:23.704Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:17:22.155Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Exception Handling in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/exception-handling-in-spring-boot)
{.links-list}




# Spring Boot의 예외 처리

스프링 부트 애플리케이션을 개발할 때 강력한 예외 처리 메커니즘을 갖추는 것이 중요합니다. 이렇게 하면 응용 프로그램이 런타임 중에 발생할 수 있는 예기치 않은 오류를 정상적으로 처리할 수 있습니다.

스프링 부트 애플리케이션에서 발생할 수 있는 두 가지 유형의 오류가 있습니다.
- 응용 프로그램 자체에서 발생하는 예외입니다.
- 기본 시스템 또는 프레임워크에서 발생하는 예외입니다.

스프링 부트 애플리케이션에서 두 가지 유형의 예외를 모두 처리하는 것이 중요합니다.

## 애플리케이션 예외에 대한 예외 처리

애플리케이션 예외는 애플리케이션 자체에서 발생하는 예외입니다. 이러한 오류는 일반적으로 응용 프로그램에서 예상하고 적절하게 처리할 수 있는 오류입니다.

예를 들어 사용자 계정을 생성하기 위한 RestController 엔드포인트가 있는 스프링 부트 애플리케이션을 고려하십시오. 애플리케이션이 유효하지 않은 이메일 주소로 사용자 계정을 생성하라는 요청을 받으면 BadRequestException이 발생해야 합니다.

```java
@RestController
public class UserController {

    @PostMapping("/users")
    public User createUser(@Valid @RequestBody User user) {
        // logic to create user
    }
}
```

위의 예에서 요청 본문에 제공된 이메일 주소가 유효하지 않은 경우 애플리케이션에서 BadRequestException이 발생합니다.

 이 예외를 처리하기 위해 @ControllerAdvice 및 @ExceptionHandler를 사용할 수 있습니다. @ControllerAdvice 주석은 애플리케이션의 모든 컨트롤러에 대한 전역 예외 처리기를 정의하는 데 사용됩니다. @ExceptionHandler 어노테이션은 메소드에 의해 처리될 예외 유형을 지정하는 데 사용됩니다.

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

위의 예에서 handleBadRequestException() 메서드는 응용 프로그램의 컨트롤러에서 BadRequestException이 발생할 때 호출됩니다. 이 메서드에서 예외 처리 논리를 정의할 수 있습니다.

@ControllerAdvice 대신 @RestControllerAdvice를 정의하는 것도 가능합니다. 이렇게 하면 예외 처리기가 상태 코드 대신 응답 본문을 반환할 수 있습니다.

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

위의 예에서 handleBadRequestException() 메서드는 응용 프로그램의 컨트롤러에서 BadRequestException이 발생하면 오류 메시지와 함께 응답 본문을 반환합니다.

## 시스템 예외에 대한 예외 처리

시스템 예외는 기본 시스템 또는 프레임워크에서 발생하는 예외입니다. 이는 일반적으로 응용 프로그램에서 예상할 수 없는 예기치 않은 오류입니다.

예를 들어 JDBC 데이터베이스를 사용하는 스프링 부트 애플리케이션을 생각해 보십시오. 데이터베이스를 사용할 수 없는 경우 애플리케이션에서 DataAccessException이 발생합니다.

이 예외를 처리하기 위해 @ControllerAdvice 및 @ExceptionHandler를 사용할 수 있습니다.

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

위의 예에서 handleDataAccessException() 메서드는 애플리케이션의 컨트롤러에서 DataAccessException이 발생할 때 호출됩니다. 이 메서드에서 예외 처리 논리를 정의할 수 있습니다.

@ControllerAdvice 대신 @RestControllerAdvice를 사용하는 것도 가능합니다. 이렇게 하면 예외 처리기가 상태 코드 대신 응답 본문을 반환할 수 있습니다.

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

위의 예에서 handleDataAccessException() 메서드는 응용 프로그램의 컨트롤러에서 DataAccessException이 발생할 때 오류 메시지와 함께 응답 본문을 반환합니다.