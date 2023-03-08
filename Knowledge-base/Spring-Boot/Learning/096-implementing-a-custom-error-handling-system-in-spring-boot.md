---
title: 096: Spring Boot에서 사용자 지정 오류 처리 시스템 구현
description: 
published: true
date: 2023-02-06T01:32:35.380Z
tags: 
editor: markdown
dateCreated: 2023-02-06T01:32:33.706Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [096: Implementing a Custom Error Handling System in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/096-implementing-a-custom-error-handling-system-in-spring-boot)
{.links-list}


# Spring Boot에서 사용자 지정 오류 처리 시스템 구현

모든 웹 응용 프로그램에 대해 잘 정의되고 포괄적인 오류 처리 시스템을 갖추는 것이 중요합니다. Spring Boot 프레임워크를 사용하여 빌드된 애플리케이션의 경우 특히 그렇습니다.

이번 포스팅에서는 Spring Boot에서 커스텀 에러 처리 시스템을 구현하는 방법에 대해 알아보겠습니다. 다음 주제를 다룰 것입니다.

1. 스프링부트란?
2. Spring Boot를 사용하면 어떤 이점이 있습니까?
3. Spring Boot 프레임워크의 기능은 무엇입니까?
4. Spring Boot에서 사용자 지정 오류 처리 시스템을 구현하는 방법은 무엇입니까?

## 스프링부트란?

Spring Boot는 마이크로 서비스 및 웹 애플리케이션을 만드는 데 사용되는 Java 기반 프레임워크입니다. Pivotal Software에서 개발했으며 Spring 프레임워크 제품군의 구성원입니다.

Spring Boot는 Spring 기반 애플리케이션을 만들고 배포하는 프로세스를 단순화하도록 설계되었습니다. 자동 구성 및 시작 템플릿과 같은 다양한 기능을 제공하여 Spring을 보다 쉽게 시작할 수 있습니다.

## Spring Boot를 사용하면 어떤 이점이 있나요?

Spring Boot를 사용하면 다음과 같은 많은 이점이 있습니다.

- Spring Boot를 사용하면 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다.
- Spring Boot는 자동 구성 및 스타터 템플릿과 같은 다양한 기능을 제공하여 Spring을 보다 쉽게 시작할 수 있습니다.
- Spring Boot는 독단적입니다. 즉, 대부분의 애플리케이션에 적합한 기본값 세트를 제공합니다. 이렇게 하면 모든 것을 직접 구성하는 것에 대해 걱정할 필요가 없으므로 Spring Boot를 더 쉽게 시작할 수 있습니다.

## Spring Boot 프레임워크의 기능은 무엇인가요?

Spring Boot는 마이크로서비스 및 웹 애플리케이션 구축을 위한 매력적인 선택이 되도록 하는 여러 기능을 제공합니다. 이러한 기능에는 다음이 포함됩니다.

- 자동 구성: Spring Boot는 클래스 경로에서 찾은 종속성을 기반으로 빈과 속성을 자동 구성합니다. 이렇게 하면 모든 것을 직접 구성하는 것에 대해 걱정할 필요가 없으므로 Spring Boot를 더 쉽게 시작할 수 있습니다.
- 시작 템플릿: Spring Boot는 새 프로젝트를 만드는 데 사용할 수 있는 여러 시작 템플릿을 제공합니다. 이러한 스타터 템플릿에는 종속성 및 빌드 스크립트와 같이 시작하는 데 필요한 모든 것이 포함되어 있습니다.
- 명령줄 인터페이스: Spring Boot에는 애플리케이션 시작 및 중지와 같은 명령을 실행하는 데 사용할 수 있는 명령줄 인터페이스가 포함되어 있습니다.
- 액추에이터: Spring Boot에는 애플리케이션을 모니터링하고 관리하는 데 사용할 수 있는 액추에이터가 포함되어 있습니다.

## Spring Boot에서 사용자 지정 오류 처리 시스템을 구현하는 방법은 무엇입니까?

Spring Boot에서 사용자 지정 오류 처리 시스템을 구현하는 방법에는 여러 가지가 있습니다. 이 섹션에서는 가장 일반적인 두 가지 접근 방식을 살펴보겠습니다.

- @ControllerAdvice 주석 사용
- 사용자 지정 오류 컨트롤러 만들기

### @ControllerAdvice 주석 사용

Spring Boot에서 사용자 지정 오류 처리 시스템을 구현하는 한 가지 방법은 @ControllerAdvice 주석을 사용하는 것입니다. 이 주석은 응용 프로그램의 모든 컨트롤러에 대한 전역 오류 처리기를 정의하는 데 사용할 수 있습니다.

다음은 @ControllerAdvice 주석을 사용하는 방법의 예입니다.

```java
@ControllerAdvice
public class GlobalExceptionHandler {
 
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleException(Exception ex) {
 
        ErrorResponse error = new ErrorResponse();
        error.setMessage(ex.getMessage());
        error.setStatusCode(HttpStatus.INTERNAL_SERVER_ERROR.value());
 
        return new ResponseEntity<>(error, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

위의 예에서 모든 예외에 대해 호출되는 전역 오류 처리기를 정의했습니다. 이 처리기는 ErrorResponse 클래스의 인스턴스를 생성하고 클라이언트에 반환합니다.

### 사용자 지정 오류 컨트롤러 만들기

Spring Boot에서 사용자 지정 오류 처리 시스템을 구현하는 또 다른 방법은 사용자 지정 오류 컨트롤러를 만드는 것입니다. 이 컨트롤러는 애플리케이션의 특정 컨트롤러에 대한 오류를 처리하는 데 사용할 수 있습니다.

다음은 사용자 지정 오류 컨트롤러를 만드는 방법의 예입니다.

```java
@RestController
public class ErrorController extends AbstractErrorController {
 
    @Override
    public String getErrorPath() {
        return "/error";
    }
 
    @RequestMapping("/error")
    public ResponseEntity<ErrorResponse> error(HttpServletRequest request) {
 
        ErrorResponse error = new ErrorResponse();
        error.setMessage(request.getAttribute("javax.servlet.error.message").toString());
        error.setStatusCode(Integer.valueOf(request.getAttribute("javax.servlet.error.status_code").toString()));
 
        return new ResponseEntity<>(error, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

위의 예에서 오류가 발생하는 모든 요청에 대해 호출되는 사용자 지정 오류 컨트롤러를 정의했습니다. 이 컨트롤러는 ErrorResponse 클래스의 인스턴스를 생성하고 클라이언트에 반환합니다.

## 결론

이번 포스트에서는 Spring Boot에서 커스텀 에러 핸들링 시스템을 구현하는 방법에 대해 살펴보았습니다. 우리는 다음 주제를 다루었습니다.

1. 스프링부트란?
2. Spring Boot를 사용하면 어떤 이점이 있습니까?
3. Spring Boot 프레임워크의 기능은 무엇입니까?
4. Spring Boot에서 사용자 지정 오류 처리 시스템을 구현하는 방법은 무엇입니까?