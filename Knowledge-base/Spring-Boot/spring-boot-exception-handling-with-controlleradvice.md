---
title: ControllerAdvice를 사용한 스프링 부트 예외 처리
description: 
published: true
date: 2023-02-07T17:32:29.200Z
tags: 
editor: markdown
dateCreated: 2023-02-07T17:32:27.533Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Exception Handling with ControllerAdvice***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-exception-handling-with-controlleradvice)
{.links-list}



# 소개

개발자는 애플리케이션을 구축할 때 다양한 유형의 오류에 직면합니다. 이러한 오류는 사용자 입력, 코드 문제 또는 서버 또는 데이터베이스 문제로 인해 발생할 수 있습니다.

이 기사에서는 Spring Boot에서 오류를 처리하는 방법을 살펴보겠습니다. 발생할 수 있는 다양한 유형의 오류에 대한 간략한 개요부터 시작한 다음 @ControllerAdvice 주석을 사용하여 오류를 처리하는 방법에 대해 설명합니다.

# 오류 유형

Spring Boot 애플리케이션을 빌드할 때 발생할 수 있는 세 가지 주요 유형의 오류가 있습니다.

* **유효성 검사 오류:** 사용자 입력이 예상 형식과 일치하지 않을 때 발생합니다. 예를 들어 사용자가 잘못된 이메일 주소로 양식을 제출하려고 하면 유효성 검사 오류가 발생합니다.

* **바인딩 오류:** 데이터 바인딩 프로세스가 실패할 때 발생합니다. 이는 사용자 입력이 잘못된 형식이거나 입력과 대상 개체 간에 유형 불일치가 있는 경우에 발생할 수 있습니다.

* **기타 오류:** 여기에는 데이터베이스 오류, 서버 오류 등과 같은 다른 모든 유형의 오류가 포함됩니다.

# 오류 처리

Spring Boot에서는 @ControllerAdvice 주석을 사용하여 오류를 처리할 수 있습니다. 이 주석은 모든 컨트롤러에 대한 전역 오류 처리기를 정의하는 데 사용할 수 있습니다.

@ControllerAdvice 주석은 유효성 검사 및 바인딩 오류를 모두 처리하는 데 사용할 수 있습니다. 다른 유형의 오류를 처리하려면 @ExceptionHandler 주석을 사용할 수 있습니다.

# 유효성 검사 오류

유효성 검사 오류는 @ControllerAdvice 주석을 사용하여 처리할 수 있습니다. 다음 예제에서는 @ControllerAdvice 주석을 사용하여 유효성 검사 오류를 처리합니다.

```java
@ControllerAdvice
public class ValidationErrorHandler {

    @InitBinder
    public void initBinder(WebDataBinder binder) {
        binder.addValidators(new UserValidator());
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<?> handleValidationErrors(MethodArgumentNotValidException ex) {
        // ...
    }

}
```

위의 예에서는 @InitBinder 주석을 사용하여 User 클래스에 대한 유효성 검사기를 등록합니다. 또한 유효성 검사 오류를 처리하기 위해 @ExceptionHandler 주석을 사용하고 있습니다.

# 바인딩 오류

바인딩 오류는 @ControllerAdvice 주석을 사용하여 처리할 수 있습니다. 다음 예제에서는 바인딩 오류를 처리하기 위해 @ControllerAdvice 주석을 사용하고 있습니다.

```java
@ControllerAdvice
public class BindingErrorHandler {

    @ExceptionHandler(BindException.class)
    public ResponseEntity<?> handleBindingErrors(BindException ex) {
        // ...
    }

}
```

위의 예에서 바인딩 오류를 처리하기 위해 @ExceptionHandler 주석을 사용하고 있습니다.

# 기타 오류

다른 유형의 오류는 @ExceptionHandler 주석을 사용하여 처리할 수 있습니다. 다음 예제에서는 @ExceptionHandler 주석을 사용하여 데이터베이스 오류를 처리합니다.

```java
@ControllerAdvice
public class DatabaseErrorHandler {

    @ExceptionHandler(DataAccessException.class)
    public ResponseEntity<?> handleDatabaseErrors(DataAccessException ex) {
        // ...
    }

}
```

위의 예에서 데이터베이스 오류를 처리하기 위해 @ExceptionHandler 주석을 사용하고 있습니다.

# 결론

이 기사에서는 Spring Boot에서 오류를 처리하는 방법을 살펴보았습니다. 발생할 수 있는 다양한 유형의 오류에 대한 간략한 개요부터 시작한 다음 @ControllerAdvice 주석을 사용하여 오류를 처리하는 방법에 대해 논의했습니다.