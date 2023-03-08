---
title: 用于安全 Web 应用程序的 Spring Boot 和 Spring Security
description: 
published: true
date: 2023-02-06T03:17:41.946Z
tags: 
editor: markdown
dateCreated: 2023-02-06T03:17:40.309Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot and Spring Security for Secure Web Applications***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-spring-security-for-secure-web-applications)
{.links-list}


# 用于安全 Web 应用程序的 Spring Boot 和 Spring Security

开发安全的 Web 应用程序是任何组织的首要任务。在本文中，我们将了解如何使用 Spring Boot 和 Spring Security 来创建一个简单且安全的 Web 应用程序。

我们将首先创建一个具有基本安全配置的 Spring Boot 应用程序。然后我们将添加一些 Spring Security 功能来保护我们的应用程序。

## 创建一个 Spring Boot 应用程序

我们将从创建一个 Spring Boot 应用程序开始。 Spring Boot 可以轻松创建独立的、生产级的基于 Spring 的应用程序，您可以“直接运行”。

我们将使用 [Spring Initializr](https://start.spring.io/) 来创建我们的项目。我们将选择以下依赖项：

- 网络
- 安全

我们将我们的项目命名为“secure-web-app”。

项目生成后，我们可以将其导入我们最喜欢的 IDE 并将其作为 Spring Boot 应用程序运行。

## 基本安全配置

Spring Security 是一个提供身份验证、授权和针对常见攻击的保护的框架。

默认情况下，没有配置 Spring Security。我们可以通过将以下内容添加到我们的 application.properties 文件来添加基本配置：

```
spring.security.user.name=user
spring.security.user.password=password
```

这将使用用户名“user”和密码“password”创建一个用户。

我们还可以通过创建“SecurityConfig.java”文件来添加更全面的配置。

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

这会将 Spring Security 配置为要求对所有请求进行身份验证，并使用表单登录和 HTTP 基本身份验证。

## 添加 Spring 安全特性

现在我们已经有了一个基本的 Spring Security 配置，我们可以添加一些额外的功能。

### CSRF 保护

跨站点请求伪造 (CSRF) 是一种攻击，当恶意用户诱使受害者向他们登录的 Web 应用程序提交请求时，就会发生这种攻击。

Spring Security 默认提供 CSRF 保护。我们可以通过将以下内容添加到我们的“SecurityConfig.java”文件来配置它：

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

这将禁用 CSRF 保护。

### 安全标头

我们还可以将安全标头添加到我们的响应中，以帮助防止常见的攻击。

我们可以将以下内容添加到我们的“SecurityConfig.java”文件中：

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

这会将“Content-Security-Policy”标头添加到我们的响应中。

我们还可以添加“Strict-Transport-Security”标头来强制执行 HTTPS：

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

这将要求所有包含“X-Forwarded-Proto”标头的请求使用 HTTPS。

### 身份验证提供程序

Spring Security 支持多个身份验证提供程序。我们可以通过重写 configure(AuthenticationManagerBuilder) 方法来添加对其他提供者的支持：

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

这将为单个用户配置内存中的身份验证提供程序。

我们还可以添加对 [基于 JDBC 的身份验证](https://docs.spring.io/spring-security/site/docs/current/reference/html5/# jc-authentication-jdbc) 的支持。

## 结论

在本文中，我们了解了如何使用 Spring Boot 和 Spring Security 来创建简单且安全的 Web 应用程序。我们还添加了一些额外的安全功能来帮助保护我们的应用程序。