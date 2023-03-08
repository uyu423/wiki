---
title: 084: Spring Boot에서 사용자 지정 인증 제공자 구현
description: 
published: true
date: 2023-02-05T14:32:26.126Z
tags: 
editor: markdown
dateCreated: 2023-02-05T14:32:24.486Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [084: Implementing a Custom Authentication Provider in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/084-implementing-a-custom-authentication-provider-in-spring-boot)
{.links-list}


# Spring Boot에서 사용자 지정 인증 제공자 구현

Spring Boot의 인증과 관련하여 몇 가지 다른 방법이 있습니다. 이 게시물에서는 사용자 지정 인증 공급자를 구현하는 방법을 살펴보겠습니다.

## 인증 공급자란?

인증 공급자는 사용자 인증 프로세스를 처리하는 소프트웨어입니다. 웹 애플리케이션의 맥락에서 이것은 일반적으로 사용자가 올바른 자격 증명(사용자 이름 및 비밀번호)을 제공했는지 확인하고, 그렇다면 애플리케이션에 대한 액세스를 허용하는 것을 의미합니다.

## 사용자 지정 인증 공급자를 사용하는 이유는 무엇입니까?

사용자 지정 인증 공급자를 사용하려는 몇 가지 이유가 있습니다.

* Spring Boot에서 기본적으로 제공하는 것과 다른 인증 방법을 사용하려는 경우(예: 데이터베이스 대신 LDAP를 사용하려는 경우).
* 인증 프로세스에 추가 기능을 추가하려는 경우(예: 실패한 모든 로그인 시도를 기록하려는 경우).
* 인증 프로세스가 작동하는 방식에 대해 더 많은 제어를 원합니다(예: 사용자에게 표시되는 오류 메시지를 사용자 정의할 수 있기를 원함).

## 사용자 지정 인증 공급자를 구현하는 방법

사용자 지정 인증 공급자를 구현하는 것은 실제로 매우 간단합니다. org.springframework.security.authentication.AuthenticationProvider 인터페이스를 구현하는 클래스를 생성하기만 하면 됩니다.

다음은 간단한 예입니다.

```java
public class MyAuthenticationProvider implements AuthenticationProvider {

    @Override
    public Authentication authenticate(Authentication authentication) throws AuthenticationException {
        // TODO: Implement authentication logic here
        return null;
    }

    @Override
    public boolean supports(Class<?> authentication) {
        // TODO: Implement authentication support logic here
        return false;
    }
}
```

구현해야 하는 두 가지 방법이 있습니다.

* `authenticate()`: 실제 인증 로직이 들어가는 곳입니다. 이 메서드는 `Authentication` 객체를 매개변수로 사용하고 `Authentication` 객체를 반환합니다.
* `supports()`: 이 메서드는 `AuthenticationProvider`가 주어진 `Authentication` 개체를 지원하는지 확인하는 데 사용됩니다.

## 인증 공급자 구성

`AuthenticationProvider`가 구현되면 다음 단계는 Spring Boot에서 구성하는 것입니다. 이는 `application.properties` 파일에 다음을 추가하여 수행할 수 있습니다.

```properties
spring.security.authentication-provider.class=com.example.MyAuthenticationProvider
```

## 인증 공급자 테스트

인증 공급자를 테스트하려면 테스트 메서드에서 `@WithMockUser` 주석을 사용할 수 있습니다. 이렇게 하면 인증 공급자에 대해 인증하는 데 사용할 수 있는 지정된 사용자 이름과 암호를 사용하여 모의 사용자가 생성됩니다.

다음은 간단한 예입니다.

```java
@Test
@WithMockUser(username="test", password="test")
public void testAuthentication() {
    // TODO: Implement authentication test here
}
```

## 결론

이 게시물에서는 Spring Boot에서 사용자 지정 인증 공급자를 구현하는 방법을 살펴보았습니다. 또한 구성 방법과 테스트 방법도 살펴보았습니다.