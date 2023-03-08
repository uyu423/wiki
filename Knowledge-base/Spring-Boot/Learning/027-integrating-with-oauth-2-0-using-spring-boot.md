---
title: 027: Spring Boot를 사용하여 OAuth 2.0과 통합
description: 
published: true
date: 2023-02-03T19:32:37.031Z
tags: 
editor: markdown
dateCreated: 2023-02-03T19:32:35.437Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [027: Integrating with OAuth 2.0 using Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/027-integrating-with-oauth-2-0-using-spring-boot)
{.links-list}


# OAuth 2.0 및 스프링 부트

이 게시물에서는 Spring Boot를 사용하여 OAuth 2.0과 통합하는 방법을 살펴보겠습니다.

OAuth 2.0은 널리 사용되는 인증 표준입니다. Google, Facebook 및 Twitter를 비롯한 많은 대기업에서 사용합니다.

Spring Boot는 웹 애플리케이션 구축에 널리 사용되는 Java 프레임워크입니다.

## OAuth 2.0이란?

OAuth 2.0은 인증 표준입니다. 이를 통해 사용자는 암호를 공유하지 않고도 데이터에 대한 타사 응용 프로그램 액세스 권한을 부여할 수 있습니다.

예를 들어 Google을 사용하여 타사 웹사이트에 로그인하는 경우 OAuth 2.0을 사용하고 있는 것입니다. 타사 웹사이트에는 Google 비밀번호가 필요하지 않습니다. 데이터에 액세스할 수 있는 권한만 있으면 됩니다.

## OAuth 2.0은 어떻게 작동하나요?

OAuth 2.0은 토큰을 사용하여 작동합니다. 토큰은 데이터에 액세스할 수 있는 사용자의 권한을 나타내는 데이터 조각입니다.

토큰은 인증 서버에서 생성됩니다. 사용자가 자신의 데이터에 대한 타사 애플리케이션 액세스 권한을 부여하면 인증 서버가 토큰을 생성합니다. 그런 다음 토큰이 타사 애플리케이션으로 전송됩니다.

그런 다음 타사 애플리케이션은 토큰을 사용하여 사용자 데이터에 액세스할 수 있습니다.

## 왜 OAuth 2.0을 사용하나요?

OAuth 2.0을 사용하면 다음과 같은 몇 가지 이점이 있습니다.

- 표준: OAuth 2.0은 널리 사용되는 표준이므로 사용할 수 있는 라이브러리와 도구가 많습니다.

- 안전함: OAuth 2.0은 안전하도록 설계되었습니다. 토큰은 인증 서버에서 생성되므로 타사 애플리케이션에서 추측할 수 없습니다.

- 사용하기 쉬움: OAuth 2.0은 사용하기 쉽게 설계되었습니다. 사용자는 사용하는 모든 애플리케이션의 비밀번호를 기억할 필요가 없습니다.

## Spring Boot에서 OAuth 2.0을 사용하는 방법

Spring Boot를 사용하면 OAuth 2.0을 쉽게 사용할 수 있습니다.

먼저 Spring Security OAuth 종속성을 프로젝트에 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.security.oauth</groupId>
    <artifactId>spring-security-oauth2</artifactId>
    <version>2.3.4.RELEASE</version>
</dependency>
```

다음으로 인증 서버를 구성해야 합니다. 인증 서버는 토큰 생성을 담당합니다.

Spring Boot는 인증 서버를 자동으로 구성할 수 있습니다. application.properties 파일에 다음 속성을 추가하기만 하면 됩니다.

```properties
spring.security.oauth2.client.registration.client-id=<your-client-id>
spring.security.oauth2.client.registration.client-secret=<your-client-secret>
spring.security.oauth2.client.provider.oauth2.authorization-uri=https://<your-authorization-server>/oauth2/authorize
spring.security.oauth2.client.provider.oauth2.token-uri=https://<your-authorization-server>/oauth2/token
spring.security.oauth2.client.provider.oauth2.user-info-uri=https://<your-authorization-server>/oauth2/userinfo
```

<your-client-id>를 애플리케이션의 클라이언트 ID로 바꾸고 <your-client-secret>을 애플리케이션의 클라이언트 암호로 바꿉니다.

<your-authorization-server>를 인증 서버의 URL로 바꿉니다.

Spring Boot는 제공한 클라이언트 ID와 클라이언트 시크릿으로 인증 서버를 자동으로 구성합니다.

인증 서버가 구성되었으므로 이제 사용을 시작할 수 있습니다.

먼저 액세스 토큰을 받아야 합니다. 액세스 토큰은 사용자의 데이터에 액세스할 수 있도록 하는 토큰입니다.

액세스 토큰을 얻으려면 인증 서버에 POST 요청을 보내야 합니다. 요청에는 다음 매개변수가 포함되어야 합니다.

- client_id: 애플리케이션의 클라이언트 ID
- client_secret: 애플리케이션의 클라이언트 암호
- grant_type: 요청하는 보조금 유형입니다. OAuth 2.0의 경우 "authorization_code"여야 합니다.
- 코드: Authorization Server로부터 받은 코드
- redirect_uri: 애플리케이션의 리디렉션 URI

인증 서버는 액세스 토큰으로 응답합니다.

액세스 토큰이 있으면 이를 사용하여 사용자의 데이터에 액세스할 수 있습니다.

이렇게 하려면 리소스 서버에 GET 요청을 보내야 합니다. 요청에는 다음 매개변수가 포함되어야 합니다.

- access_token: Authorization Server로부터 받은 액세스 토큰

리소스 서버는 사용자의 데이터로 응답합니다.

## 추가 정보

- OAuth 2.0은 인증기준이 아닌 인증기준입니다. OAuth 2.0은 인증에 사용할 수 있지만 이를 위해 설계되지는 않았습니다.

- Spring Boot는 기본적으로 OAuth 2.0을 지원하지 않습니다. Spring Security OAuth 종속성을 프로젝트에 추가해야 합니다.

- Spring Boot는 인증 서버를 자동으로 구성할 수 있습니다. application.properties 파일에 클라이언트 ID와 클라이언트 암호를 추가하기만 하면 됩니다.