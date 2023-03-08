---
title: Spring Security로 RESTful 서비스 보호
description: 
published: true
date: 2023-02-06T23:32:27.571Z
tags: 
editor: markdown
dateCreated: 2023-02-06T23:32:21.937Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Securing RESTful Services with Spring Security***English** document is available*](/en/Knowledge-base/Spring-Boot/securing-restful-services-with-spring-security)
{.links-list}


# Spring Security로 RESTful 서비스 보호

웹 애플리케이션의 보안 필요성은 잘 알려져 있고 잘 이해되어 있습니다. 최근 몇 년 동안 RESTful 웹 서비스의 등장으로 민감한 데이터를 보호하고 무단 액세스를 방지하기 위해 이러한 서비스를 보호해야 할 필요성이 생겼습니다.

Spring Security는 웹 애플리케이션과 RESTful 웹 서비스 모두를 보호하기 위한 강력하고 유연한 프레임워크입니다. 이 기사에서는 Spring Security를 사용하여 RESTful 웹 서비스를 보호하는 방법을 살펴보겠습니다. 또한 RESTful 서비스의 가장 일반적인 보안 취약점과 Spring Security가 이러한 위험을 완화하는 데 어떻게 도움이 되는지 살펴보겠습니다.

## 스프링 시큐리티란?

Spring Security는 웹 애플리케이션과 RESTful 웹 서비스 모두에 대한 인증 및 권한 부여 서비스를 제공하는 프레임워크입니다. Spring Framework 위에 구축되었으며 웹 애플리케이션 보안을 위한 가장 인기 있는 프레임워크 중 하나입니다.

Spring Security는 고도로 구성 가능하며 기존 웹 애플리케이션과 RESTful 웹 서비스 모두를 보호하는 데 사용할 수 있습니다. 다음을 포함하되 이에 국한되지 않는 다양한 기능을 제공합니다.

- 인증(여러 인증 공급자 지원 포함)
- 인증(역할 기반 액세스 제어 지원 포함)
- 세션 관리
- 암호화
- 액세스 제어
- 감사
- 그리고 더

## RESTful 서비스를 위한 스프링 보안 구성

RESTful 웹 서비스에 대한 Spring Security 구성은 비교적 간단합니다. 첫 번째 단계는 Spring Security 종속성을 프로젝트에 추가하는 것입니다. 예를 들어 Maven을 사용하는 경우 pom.xml 파일에 다음 종속성을 추가합니다.

```xml
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-core</artifactId>
    <version>5.1.5.RELEASE</version>
</dependency>
```

종속성이 추가되면 프로젝트에 보안 구성 파일을 추가하여 Spring Security를 구성할 수 있습니다. 이 파일의 이름은 원하는 대로 지정할 수 있지만 src/main/resources 디렉토리에 있어야 합니다.

다음은 Spring Security 구성 파일의 간단한 예입니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans:beans xmlns="http://www.springframework.org/schema/security"
    xmlns:beans="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
    http://www.springframework.org/schema/security
    http://www.springframework.org/schema/security/spring-security-4.0.xsd">

    <!-- Configure Spring Security -->

</beans:beans>
```

이 예제에서는 /api/로 시작하는 모든 URL을 보호하도록 Spring Security를 구성했습니다. 또한 HTTP 기본 인증을 사용하도록 Spring Security를 구성했습니다.

## 일반적인 REST 보안 취약점

RESTful 웹 서비스에 대해 Spring Security를 구성하는 방법을 살펴보았으므로 이제 RESTful 서비스에서 가장 일반적인 보안 취약점 중 일부를 살펴보겠습니다.

### SQL 인젝션

SQL 주입은 승인되지 않은 SQL 쿼리를 실행하기 위해 웹 애플리케이션에 악성 SQL 코드를 주입하는 공격 유형입니다. 이는 보안 제어를 우회하거나 중요한 데이터를 보거나 데이터를 삭제하는 데 사용할 수 있습니다.

SQL 인젝션 공격은 비교적 실행하기 쉽고 파괴적인 결과를 초래할 수 있습니다. 다행스럽게도 Spring Security는 SQL 주입 공격에 대한 기본 제공 보호 기능을 제공합니다.

### 교차 사이트 요청 위조(CSRF)

CSRF는 악의적인 사용자가 피해자를 속여 웹 애플리케이션에 악의적인 요청을 제출하도록 하는 공격 유형입니다. 이것은 사용자의 암호를 변경하거나 은행 계좌에서 돈을 이체하는 것과 같은 승인되지 않은 작업을 수행하는 데 사용될 수 있습니다.

CSRF 공격은 상대적으로 수행하기 쉽고 감지하기가 매우 어려울 수 있습니다. Spring Security는 CSRF 공격에 대한 기본 보호 기능을 제공합니다.

### 교차 사이트 스크립팅(XSS)

XSS는 악성 JavaScript 코드가 웹 페이지에 삽입되는 공격 유형입니다. 이 코드는 피해자의 브라우저에서 실행되어 승인되지 않은 코드가 실행됩니다.

XSS 공격은 상대적으로 수행하기 쉽고 감지하기가 매우 어려울 수 있습니다. Spring Security는 XSS 공격에 대한 기본 제공 보호 기능을 제공합니다.

## 결론

이 기사에서는 Spring Security를 사용하여 RESTful 웹 서비스를 보호하는 방법을 살펴보았습니다. 또한 RESTful 서비스의 가장 일반적인 보안 취약점과 Spring Security가 이러한 위험을 완화하는 데 어떻게 도움이 되는지 살펴보았습니다.