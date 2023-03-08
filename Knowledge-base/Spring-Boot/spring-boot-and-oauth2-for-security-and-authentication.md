---
title: 보안 및 인증을 위한 Spring Boot 및 OAuth2
description: 
published: true
date: 2023-02-08T03:32:23.030Z
tags: 
editor: markdown
dateCreated: 2023-02-08T03:32:21.472Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot and OAuth2 for Security and Authentication***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-oauth2-for-security-and-authentication)
{.links-list}


# 보안 및 인증을 위한 Spring Boot 및 OAuth2

Spring Boot 보안 OAuth2 스택은 Spring Boot 애플리케이션에 OAuth2 보호를 추가하는 편리한 방법을 제공합니다. 이 기사에서는 Spring Boot 및 OAuth2를 사용하여 간단한 REST API를 보호하는 방법을 살펴봅니다. 또한 Spring Security 및 JWT를 사용하여 REST API에 보안 계층을 추가합니다.

## OAuth2란?

OAuth2는 애플리케이션이 HTTP 서비스의 사용자 계정에 대한 제한된 액세스 권한을 얻을 수 있도록 하는 권한 부여 프레임워크입니다. 사용자 계정을 호스팅하는 서비스에 사용자 인증을 위임하고 타사 응용 프로그램이 사용자 계정에 액세스할 수 있도록 권한을 부여하는 방식으로 작동합니다. OAuth2는 단일 인증 엔드포인트와 단일 토큰 엔드포인트를 제공합니다.

## 스프링부트란?

Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 만드는 데 사용되는 Java 기반 프레임워크입니다. 내장형 서버, 보안, 메트릭, 상태 확인 등과 같은 광범위한 비기능 기능을 제공하는 구성보다 관례적인 프레임워크입니다.

## 스프링 시큐리티란?

Spring Security는 일반적인 공격에 대한 인증, 권한 부여 및 보호를 제공하는 프레임워크입니다. 양식 기반 인증, HTTP 기본 인증 등과 같은 광범위한 인증 메커니즘을 제공합니다.

## JWT란?

JWT(JSON 웹 토큰)는 두 당사자 간에 전송될 클레임을 나타내는 소형 URL 안전 수단입니다. JWT의 클레임은 JWS(JSON 웹 서명) 구조의 페이로드 또는 JWE(JSON 웹 암호화) 구조의 일반 텍스트로 사용되는 JSON 객체로 인코딩되어 클레임을 디지털 서명 또는 무결성으로 사용할 수 있습니다. 메시지 인증 코드(MAC)로 보호 및/또는 암호화됩니다.

## 프로젝트 설정

다음 종속성을 사용하여 간단한 Spring Boot 프로젝트를 설정하는 것으로 시작하겠습니다.

- 스프링 부트 웹
- 스프링 부트 보안
- 스프링 부트 OAuth2 보안
- 스프링 시큐리티 JWT

프로젝트는 앞서 언급한 종속성과 함께 Spring Initializr를 사용하여 생성할 수 있습니다.

## OAuth2 구성

인증에 OAuth2를 사용하도록 애플리케이션을 구성합니다. OAuth2는 애플리케이션이 HTTP 서비스의 사용자 계정에 대한 제한된 액세스 권한을 얻을 수 있도록 하는 권한 부여 프레임워크입니다.

OAuth2ClientProperties 빈을 만들고 OAuth2 클라이언트의 속성으로 구성해야 합니다. 또한 ResourceServerProperties 빈을 생성하고 리소스 서버의 속성으로 구성해야 합니다.

## 스프링 보안 설정

REST API를 보호하기 위해 Spring Security를 구성합니다. WebSecurityConfigurerAdapter를 만들고 configure(HttpSecurity) 메서드를 재정의해야 합니다. 이 방법에서는 애플리케이션에 대한 보안 규칙을 구성합니다.

또한 JwtAuthenticationFilter를 만들고 JWT 인증을 수행하도록 구성해야 합니다.

## 애플리케이션 테스트

유효한 사용자 이름과 암호를 사용하여 POST 요청을 /login 엔드포인트로 전송하여 애플리케이션을 테스트할 수 있습니다. 인증에 성공하면 JWT 토큰과 함께 JSON 응답을 받아야 합니다.

이 토큰을 사용하여 Authorization 헤더의 토큰과 함께 /userinfo 끝점에 GET 요청을 보내 애플리케이션의 보호된 리소스에 액세스할 수 있습니다.

## 결론

이 기사에서는 Spring Boot 및 OAuth2를 사용하여 간단한 REST API를 보호하는 방법을 살펴보았습니다. 또한 Spring Security 및 JWT를 사용하여 REST API에 보안 계층을 추가하는 방법도 살펴보았습니다.