---
title: 058: Spring Boot 애플리케이션에서 보안 구현
description: 
published: true
date: 2023-02-04T21:32:30.237Z
tags: 
editor: markdown
dateCreated: 2023-02-04T21:32:24.983Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [058: Implementing Security in a Spring Boot Application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/058-implementing-security-in-a-spring-boot-application)
{.links-list}


# Spring Boot 애플리케이션에서 보안 구현

Java 개발자라면 Spring 프레임워크에 익숙할 것입니다. Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 응용 프로그램을 쉽게 만들 수 있는 Spring 프레임워크의 확장입니다.

이 게시물에서는 Spring Boot 애플리케이션에서 보안을 구현하는 방법을 살펴보겠습니다. Spring Boot 애플리케이션에서 구현할 수 있는 다양한 유형의 보안을 살펴보는 것으로 시작하겠습니다. 그런 다음 Spring Security 프레임워크를 구성하고 사용하여 애플리케이션을 보호하는 방법을 살펴보겠습니다.

## 보안 유형

Spring Boot 애플리케이션에서 구현할 수 있는 두 가지 주요 보안 유형은 인증과 권한 부여입니다.

인증은 사용자가 자신이 주장하는 사람인지 확인하는 프로세스입니다. 권한 부여는 사용자가 특정 리소스에 액세스할 수 있는지 여부를 확인하는 프로세스입니다.

Spring Boot 애플리케이션에서 인증은 일반적으로 로그인 양식으로 처리됩니다. 사용자는 사용자 이름과 비밀번호를 입력하고 Spring Security는 자격 증명이 유효한지 확인합니다.

권한 부여는 일반적으로 사용자에게 역할을 할당하여 처리됩니다. 예를 들어 관리자 역할과 일반 사용자 역할이 있을 수 있습니다. 관리자는 일반 사용자보다 더 많은 리소스에 액세스할 수 있습니다.

## 스프링 보안 설정

Spring Security는 인증 및 권한 부여 서비스를 제공하는 프레임워크입니다. Spring Boot 애플리케이션에서 쉽게 구성하고 사용할 수 있습니다.

애플리케이션에 Spring Security를 추가하려면 빌드 파일에 다음 종속성을 추가합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

종속성을 추가하면 Spring Security가 기본적으로 활성화됩니다. 기본적으로 Spring Security는 메모리 내 인증을 사용합니다. 이는 데이터베이스 또는 기타 외부 서비스를 구성할 필요가 없음을 의미합니다.

Spring Security를 구성하기 위해 애플리케이션에 @Configuration 클래스를 추가할 수 있습니다. 이 클래스는 애플리케이션에 액세스할 수 있는 사용자 및 사용자가 가진 역할과 같은 Spring Security의 다양한 측면을 구성하는 데 사용할 수 있습니다.

## 사용자 인증

사용자가 보호된 리소스에 액세스하려고 하면 로그인 페이지로 리디렉션됩니다. 이 페이지에서 사용자 이름과 비밀번호를 입력합니다.

그런 다음 Spring Security는 사용자를 인증합니다. 자격 증명이 유효한 경우 사용자는 액세스를 시도했던 리소스로 리디렉션됩니다. 자격 증명이 유효하지 않으면 사용자는 오류 페이지로 리디렉션됩니다.

## 사용자 인증

사용자가 인증되면 Spring Security는 보호된 리소스에 액세스하기 전에 사용자를 인증해야 합니다.

승인은 일반적으로 사용자에게 역할을 할당하여 수행됩니다. 예를 들어 관리자 역할과 일반 사용자 역할이 있을 수 있습니다. 관리자는 일반 사용자보다 더 많은 리소스에 액세스할 수 있습니다.

컨트롤러 또는 서비스 메서드에 @RolesAllowed 주석을 추가하여 사용자가 가진 역할을 구성할 수 있습니다. 예를 들어:

```java
@Service
public class MyService {

    @RolesAllowed("ADMIN")
    public void doSomething() {
        // ...
    }
}
```

이 예에서 doSomething() 메서드는 ADMIN 역할을 가진 사용자만 액세스할 수 있습니다.

## 결론

이 게시물에서는 Spring Boot 애플리케이션에서 보안을 구현하는 방법을 살펴보았습니다. 구현할 수 있는 다양한 유형의 보안을 살펴보고 Spring Security 프레임워크를 구성하고 사용하는 방법을 살펴보았습니다.