---
title: Spring Boot로 예외 처리
description: 
published: true
date: 2023-02-17T18:04:29.037Z
tags: 
editor: markdown
dateCreated: 2023-01-30T12:32:23.126Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Exception Handling with Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/exception-handling-with-spring-boot)
{.links-list}

    
    
# Spring Boot로 예외 처리하기

Spring Boot는 예외 처리를 위한 여러 유틸리티를 제공합니다. 이 기사에서는 가장 일반적으로 사용되는 몇 가지 기술을 살펴보겠습니다.

## @ExceptionHandler로 예외 처리하기

SpringBoot에서 예외를 처리하는 가장 일반적인 방법은 @ExceptionHandler 주석을 사용하는 것입니다. 이 주석은 컨트롤러 메서드에 적용할 수 있으며 지정된 유형의 예외가 컨트롤러에 의해 throw될 때 메서드가 호출되도록 합니다.

예를 들어 다음 메서드를 가진 컨트롤러가 있다고 가정해 보겠습니다.

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

someMethod() 메서드에서 예외가 발생하면 handleException() 메서드가 호출됩니다. 이는 handleException() 메서드에 @ExceptionHandler가 주석으로 추가되어 있고 Exception 유형의 예외를 처리할 수 있기 때문입니다.

@ExceptionHandler로 컨트롤러 메서드에 주석을 달고 다음과 같이 여러 예외 유형을 지정할 수도 있습니다.

```java
@ExceptionHandler({IOException.class, MyCustomException.class})
public void handleException(Exception e) {
    // ...
}
```

이 경우 컨트롤러에서 IOException 또는 MyCustomException이 발생하면 handleException() 메서드가 호출됩니다.

## @ControllerAdvice로 예외 처리하기

모든 컨트롤러에 대해 전역적으로 예외를 처리하려면 @ControllerAdvice 주석을 사용할 수 있습니다. 이 주석은 클래스에 적용할 수 있으며 컨트롤러에서 예외가 발생할 때 클래스의 모든 메서드가 호출되도록 합니다.

예를 들어 다음과 같은 메서드가 있는 클래스가 있다고 가정해 보겠습니다.

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

이 경우 컨트롤러에서 예외가 발생할 때마다 handleException() 메서드가 호출됩니다. someMethod() 메서드도 호출되지만 예외 처리에는 영향을 미치지 않습니다.

## @RestControllerAdvice로 예외 처리하기

Spring의 REST 지원을 사용하는 경우 @RestControllerAdvice 주석을 사용하여 모든 REST 컨트롤러에 대한 예외를 전역적으로 처리할 수 있습니다. 이 주석은 @ControllerAdvice와 유사하지만 REST 컨트롤러에만 적용됩니다.

예를 들어 다음과 같은 메서드가 있는 클래스가 있다고 가정해 보겠습니다.

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

이 경우 REST 컨트롤러에서 예외가 발생할 때마다 handleException() 메서드가 호출됩니다. someMethod() 메서드도 호출되지만 예외 처리에는 영향을 미치지 않습니다.

## @ResponseStatus로 예외 처리하기

예외를 특정 HTTP 상태 코드에 매핑하려는 경우 @ResponseStatus 주석을 사용할 수 있습니다. 이 주석은 컨트롤러 메서드에 적용할 수 있으며 메서드가 예외를 throw할 때 지정된 HTTP 상태 코드가 반환되도록 합니다.

예를 들어 다음 메서드를 가진 컨트롤러가 있다고 가정해 보겠습니다.

```java
@ResponseStatus(HttpStatus.BAD_REQUEST)
public class MyController {
    
    public void someMethod() {
        throw new Exception("something went wrong");
    }
}
```

이 경우 someMethod() 메서드는 예외를 발생시키고 HTTP 상태 코드 400(잘못된 요청)이 클라이언트에 반환됩니다.

## 결론

예외 처리는 개발의 중요한 부분이며 Spring Boot는 예외 처리를 위한 여러 유틸리티를 제공합니다. 이 기사에서는 가장 일반적으로 사용되는 몇 가지 기술을 살펴보았습니다.