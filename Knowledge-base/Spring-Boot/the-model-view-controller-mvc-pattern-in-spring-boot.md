---
title: Spring Boot의 MVC(Model-View-Controller) 패턴
description: 
published: true
date: 2023-02-01T06:57:43.309Z
tags: 
editor: markdown
dateCreated: 2023-02-01T06:57:41.712Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [The Model-View-Controller (MVC) Pattern in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-model-view-controller-mvc-pattern-in-spring-boot)
{.links-list}



# Spring Boot의 Model-View-Controller(MVC) 패턴

MVC(Model-View-Controller)는 애플리케이션을 모델, 뷰 및 컨트롤러의 세 가지 주요 논리적 구성 요소로 분리하는 아키텍처 소프트웨어 디자인 패턴입니다.

MVC 패턴은 일반적으로 비즈니스 로직(모델) 및 제어 흐름(컨트롤러)에서 프리젠테이션 계층(뷰)을 분리하기 위해 웹 애플리케이션에서 사용됩니다. 이러한 관심사의 분리는 코드베이스를 깨끗하고 유지 관리 가능하게 유지하고 애플리케이션을 더 쉽게 테스트하고 확장할 수 있도록 합니다.

Spring MVC 애플리케이션에서 컨트롤러는 사용자 요청을 처리하고 적절한 응답을 생성하는 역할을 합니다. 뷰는 사용자에게 응답을 렌더링하는 역할을 합니다. 모델은 뷰에 표시할 데이터를 저장하는 데이터 구조입니다.

MVC 패턴은 웹 애플리케이션에만 국한되지 않습니다. 데스크탑, 모바일, 웹 등 모든 유형의 애플리케이션에서 사용할 수 있습니다.

## MVC 패턴은 어떻게 작동합니까?

사용자 요청이 애플리케이션에 들어오면 컨트롤러가 이를 처리할 책임이 있습니다. 컨트롤러는 렌더링할 뷰를 결정하고 뷰에 표시할 데이터를 뷰에 전달합니다. 그런 다음 뷰는 사용자에게 응답을 렌더링합니다.

MVC 패턴에는 다음과 같은 이점이 있습니다.

- 애플리케이션의 문제를 분리하여 코드베이스를 유지 관리하고 테스트하기 쉽게 만듭니다.
- 응용 프로그램을 쉽게 확장할 수 있습니다.
- 애플리케이션에 새로운 기능을 더 쉽게 추가할 수 있습니다.

## Spring Boot에서 MVC 패턴 구현

Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있는 인기 있는 Java 웹 애플리케이션 프레임워크입니다.

Spring Boot MVC 애플리케이션은 일반적으로 다음 세 계층으로 구성됩니다.

- 컨트롤러 레이어
- 서비스 레이어
- 리포지토리 레이어

컨트롤러 계층은 사용자 요청을 처리하고 적절한 응답을 생성하는 역할을 합니다. 서비스 계층은 비즈니스 로직을 담당합니다. 저장소 계층은 데이터 액세스를 담당합니다.

다음 다이어그램은 세 계층 간의 관계를 보여줍니다.

![스프링 부트 MVC](https://miro.medium.com/max/875/1*tYH4i0zAj7zQLxB7-tscKg.png)

Spring Boot MVC 애플리케이션에서 컨트롤러는 일반적으로 Spring @RestController입니다. 서비스 계층은 일반적으로 Spring @Service입니다. 리포지토리 계층은 일반적으로 Spring @Repository입니다.

다음 코드 스니펫은 컨트롤러, 서비스 및 리포지토리에 주석을 추가하는 방법을 보여줍니다.

```java
@RestController
public class HelloController {

    @RequestMapping("/hello")
    public String hello() {
        return "Hello, world!";
    }
}
```

```java
@Service
public class HelloService {

    public String getHelloMessage() {
        return "Hello, world!";
    }
}
```

```java
@Repository
public class HelloRepository {

    public String getHelloMessage() {
        return "Hello, world!";
    }
}
```

## 결론

MVC 패턴은 응용 프로그램을 모델, 뷰 및 컨트롤러의 세 가지 주요 논리적 구성 요소로 분리하는 널리 사용되는 소프트웨어 디자인 패턴입니다.

Spring MVC 애플리케이션에서 컨트롤러는 사용자 요청을 처리하고 적절한 응답을 생성하는 역할을 합니다. 뷰는 사용자에게 응답을 렌더링하는 역할을 합니다. 모델은 뷰에 표시할 데이터를 저장하는 데이터 구조입니다.

MVC 패턴에는 다음과 같은 이점이 있습니다.

- 애플리케이션의 문제를 분리하여 코드베이스를 유지 관리하고 테스트하기 쉽게 만듭니다.
- 응용 프로그램을 쉽게 확장할 수 있습니다.
- 애플리케이션에 새로운 기능을 더 쉽게 추가할 수 있습니다.

## 참조

- [모델 뷰 컨트롤러](https://en.wikipedia.org/wiki/Model–view–controller)
- [스프링 MVC](https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc)
- [스프링 부트 MVC](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-spring-mvc.html)