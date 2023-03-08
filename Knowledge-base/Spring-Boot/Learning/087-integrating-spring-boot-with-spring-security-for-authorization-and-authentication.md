---
title: 087: 권한 부여 및 인증을 위해 Spring Boot와 Spring Security 통합
description: 
published: true
date: 2023-02-05T17:32:21.517Z
tags: 
editor: markdown
dateCreated: 2023-02-05T17:32:16.203Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [087: Integrating Spring Boot with Spring Security for Authorization and Authentication***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/087-integrating-spring-boot-with-spring-security-for-authorization-and-authentication)
{.links-list}


# 087: 권한 부여 및 인증을 위해 Spring Boot와 Spring Security 통합

이 게시물에서는 권한 부여 및 인증을 위해 Spring Boot를 Spring Security와 통합하는 방법을 알아봅니다.

## 왜 스프링 시큐리티인가?

Spring Security는 강력하고 사용자 정의가 가능한 인증 및 권한 부여 프레임워크입니다. 이는 Spring 기반 애플리케이션 보안을 위한 사실상의 표준입니다.

## 필요한 것

- 텍스트 편집기 또는 IDE
- JDK 8 이상
- 메이븐 3.0+

## 스프링 시큐리티와 스프링 부트를 통합하는 방법

1. `pom.xml` 파일에 Spring Security 종속성을 추가합니다.

```xml
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-security</artifactId>
	</dependency>
</dependencies>
```

2. `SecurityConfig.java` 파일을 만들고 `@EnableWebSecurity`로 주석을 답니다.

```java
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

}
```

3. 필요에 맞게 `SecurityConfig` 클래스를 구성합니다. 예를 들어 `@Configuration` 주석을 추가할 수 있습니다.

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

}
```

4. '@EnableGlobalMethodSecurity'를 추가하여 메서드 수준 보안을 활성화할 수도 있습니다.

```java
@Configuration
@EnableWebSecurity
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class SecurityConfig extends WebSecurityConfigurerAdapter {

}
```

5. `SecurityConfig` 클래스에서 `configure(HttpSecurity)` 메서드를 재정의하여 보안 설정을 구성합니다.

```java
@Override
protected void configure(HttpSecurity http) throws Exception {
	http
		.authorizeRequests()
			.anyRequest().authenticated()
			.and()
		.formLogin()
			.loginPage("/login")
			.permitAll()
			.and()
		.logout()
			.permitAll();
}
```

6. 메모리 내 인증 저장소를 사용하도록 Spring Security를 구성할 수도 있습니다.

```java
@Override
protected void configure(AuthenticationManagerBuilder auth) throws Exception {
	auth
		.inMemoryAuthentication()
			.withUser("user").password("password").roles("USER");
}
```

## 통합 테스트

1. 통합을 테스트하려면 애플리케이션을 시작하고 `http://localhost:8080/login`으로 이동합니다. 로그인 페이지가 표시됩니다.

![스프링시큐리티 로그인 페이지](https://i.imgur.com/zFw8YxG.png)

2. `configure(AuthenticationManagerBuilder)` 메서드에서 사용자 이름과 비밀번호를 입력하고 "로그인"을 클릭합니다. "환영" 페이지가 표시됩니다.

![스프링 시큐리티 환영 페이지](https://i.imgur.com/ZUwLNcu.png)

## 축하해요!

Spring Security와 Spring Boot를 성공적으로 통합했습니다.