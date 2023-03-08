---
title: 087: Integrating Spring Boot with Spring Security for Authorization and Authentication
description: 
published: true
date: 2023-02-05T17:32:17.891Z
tags: 
editor: markdown
dateCreated: 2023-02-05T17:32:16.207Z
---

- [087: Integración de Spring Boot con Spring Security para autorización y autenticación***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/087-integrating-spring-boot-with-spring-security-for-authorization-and-authentication)
{.links-list}
- [087：将 Spring Boot 与 Spring Security 集成以进行授权和身份验证***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/087-integrating-spring-boot-with-spring-security-for-authorization-and-authentication)
{.links-list}
- [087: 권한 부여 및 인증을 위해 Spring Boot와 Spring Security 통합***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/087-integrating-spring-boot-with-spring-security-for-authorization-and-authentication)
{.links-list}


# 087: Integrating Spring Boot with Spring Security for Authorization and Authentication

In this post, we'll learn how to integrate Spring Boot with Spring Security for authorization and authentication.

## Why Spring Security?

Spring Security is a powerful and highly customizable authentication and authorization framework. It's the de-facto standard for securing Spring-based applications.

## What You'll Need

- A text editor or IDE
- JDK 8 or later
- Maven 3.0+

## How to Integrate Spring Boot with Spring Security

1. Add the Spring Security dependencies to your `pom.xml` file:

```xml
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-security</artifactId>
	</dependency>
</dependencies>
```

2. Create a `SecurityConfig.java` file and annotate it with `@EnableWebSecurity`:

```java
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

}
```

3. Configure the `SecurityConfig` class to suit your needs. For example, you might want to add a `@Configuration` annotation:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

}
```

4. You can also add `@EnableGlobalMethodSecurity` to enable method-level security:

```java
@Configuration
@EnableWebSecurity
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class SecurityConfig extends WebSecurityConfigurerAdapter {

}
```

5. In the `SecurityConfig` class, override the `configure(HttpSecurity)` method to configure security settings:

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

6. You can also configure Spring Security to use an in-memory authentication store:

```java
@Override
protected void configure(AuthenticationManagerBuilder auth) throws Exception {
	auth
		.inMemoryAuthentication()
			.withUser("user").password("password").roles("USER");
}
```

## Testing the Integration

1. To test the integration, start the application and navigate to `http://localhost:8080/login`. You should see the login page:

![Spring Security Login Page](https://i.imgur.com/zFw8YxG.png)

2. Enter the username and password from the `configure(AuthenticationManagerBuilder)` method and click "Login". You should see the "Welcome" page:

![Spring Security Welcome Page](https://i.imgur.com/ZUwLNcu.png)

## Congratulations!

You've successfully integrated Spring Boot with Spring Security.