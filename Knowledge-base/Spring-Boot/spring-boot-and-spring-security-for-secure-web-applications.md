---
title: 안전한 웹 애플리케이션을 위한 Spring Boot 및 Spring Security
description: 
published: true
date: 2023-02-06T03:17:41.935Z
tags: 
editor: markdown
dateCreated: 2023-02-06T03:17:40.310Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot and Spring Security for Secure Web Applications***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-spring-security-for-secure-web-applications)
{.links-list}


# 보안 웹 애플리케이션을 위한 스프링 부트 및 스프링 보안

보안 웹 애플리케이션 개발은 모든 조직의 최우선 과제입니다. 이 기사에서는 Spring Boot 및 Spring Security를 사용하여 간단하고 안전한 웹 애플리케이션을 만드는 방법을 살펴보겠습니다.

먼저 기본 보안 구성으로 Spring Boot 애플리케이션을 생성합니다. 그런 다음 몇 가지 Spring Security 기능을 추가하여 애플리케이션을 보호합니다.

## 스프링 부트 애플리케이션 만들기

Spring Boot 애플리케이션을 만드는 것부터 시작하겠습니다. Spring Boot를 사용하면 "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다.

[Spring Initializr](https://start.spring.io/)를 사용하여 프로젝트를 생성합니다. 다음 종속성을 선택합니다.

- 웹
- 보안

프로젝트 이름을 `secure-web-app`으로 지정합니다.

프로젝트가 생성되면 선호하는 IDE로 가져와서 Spring Boot 애플리케이션으로 실행할 수 있습니다.

## 기본 보안 구성

Spring Security는 일반적인 공격에 대한 인증, 권한 부여 및 보호를 제공하는 프레임워크입니다.

기본적으로 Spring Security는 구성되지 않습니다. `application.properties` 파일에 다음을 추가하여 기본 구성을 추가할 수 있습니다.

```
spring.security.user.name=user
spring.security.user.password=password
```

이렇게 하면 사용자 이름이 `user`이고 비밀번호가 `password`인 사용자가 생성됩니다.

`SecurityConfig.java` 파일을 생성하여 보다 포괄적인 구성을 추가할 수도 있습니다.

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .and()
            .httpBasic();
    }
}
```

이것은 모든 요청에 대한 인증을 요구하고 양식 로그인 및 HTTP 기본 인증을 사용하도록 Spring Security를 구성합니다.

## 스프링 보안 기능 추가

이제 기본 Spring Security 구성이 준비되었으므로 몇 가지 추가 기능을 추가할 수 있습니다.

### CSRF 보호

CSRF(Cross-Site Request Forgery)는 악의적인 사용자가 피해자가 로그인한 웹 애플리케이션에 요청을 제출하도록 속일 때 발생하는 공격 유형입니다.

Spring Security는 기본적으로 CSRF 보호를 제공합니다. `SecurityConfig.java` 파일에 다음을 추가하여 구성할 수 있습니다.

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .csrf().disable()
            ...
    }
}
```

이렇게 하면 CSRF 보호가 비활성화됩니다.

### 보안 헤더

일반적인 공격으로부터 보호하기 위해 응답에 보안 헤더를 추가할 수도 있습니다.

`SecurityConfig.java` 파일에 다음을 추가할 수 있습니다.

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .headers()
                .contentSecurityPolicy("script-src 'self'");
    }
}
```

이렇게 하면 응답에 `Content-Security-Policy` 헤더가 추가됩니다.

HTTPS를 적용하기 위해 `Strict-Transport-Security` 헤더를 추가할 수도 있습니다.

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .requiresChannel()
                .requestMatchers(r -> r.getHeader("X-Forwarded-Proto") != null)
                .requiresSecure();
    }
}
```

이렇게 하려면 `X-Forwarded-Proto` 헤더가 포함된 모든 요청에 대해 HTTPS가 필요합니다.

### 인증 공급자

Spring Security는 여러 인증 공급자를 지원합니다. `configure(AuthenticationManagerBuilder)` 메서드를 재정의하여 추가 공급자에 대한 지원을 추가할 수 있습니다.

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth
            .inMemoryAuthentication()
                .withUser("user").password("password").roles("USER");
    }

    ...
}
```

이렇게 하면 단일 사용자로 메모리 내 인증 공급자가 구성됩니다.

[JDBC 기반 인증](https://docs.spring.io/spring-security/site/docs/current/reference/html5/# jc-authentication-jdbc)에 대한 지원도 추가할 수 있습니다.

## 결론

이 기사에서는 Spring Boot 및 Spring Security를 사용하여 간단하고 안전한 웹 애플리케이션을 만드는 방법을 살펴보았습니다. 또한 애플리케이션을 보호하는 데 도움이 되는 몇 가지 추가 보안 기능을 추가했습니다.