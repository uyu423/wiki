---
title: 006：使用 Spring Security 实现安全性
description: 
published: true
date: 2023-02-03T07:45:38.019Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:45:36.282Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [006: Implementing security with Spring Security***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/006-implementing-security-with-spring-security)
{.links-list}


# 使用 Spring Security 实现安全性

Spring Security 是一个在 Java 应用程序中提供身份验证和授权服务的框架。它是一个广泛使用的框架，提供了许多开箱即用的功能。在这篇文章中，我们将看看如何使用 Spring Security 在 Spring 应用程序中实现安全性。

## 配置 Spring 安全

第一步是将 Spring Security 依赖项添加到您的项目中。如果您使用的是 Maven，则可以将以下依赖项添加到您的 `pom.xml` 文件中：

```xml
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-core</artifactId>
    <version>5.0.0.RELEASE</version>
</dependency>
```

如果您使用的是 Gradle，则可以将以下依赖项添加到 `build.gradle` 文件中：

```groovy
dependencies {
    compile 'org.springframework.security:spring-security-core:5.0.0.RELEASE'
}
```

添加依赖项后，您可以通过添加“SecurityConfig”类并使用“@EnableWebSecurity”对其进行注释来配置 Spring Security。 `SecurityConfig` 类可以配置为使用内存中身份验证或 LDAP 身份验证。在此示例中，我们将使用内存中身份验证。

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
}
```

在 `configure` 方法中，我们使用用户名 `user` 和密码 `password` 的用户配置内存中身份验证。该用户还具有“USER”角色。

## 保护 URL

配置 Spring Security 后，您可以使用“@Secured”注释来保护 URL。 `@Secured` 注解既可以用在方法上，也可以用在类上。在以下示例中，我们正在保护 `/admin` URL，以便只有具有 `ADMIN` 角色的用户才能访问它。

```java
@Controller
public class AdminController {

    @Secured("ROLE_ADMIN")
    @RequestMapping("/admin")
    public String admin() {
        return "admin";
    }
}
```

如果您尝试在未经身份验证的情况下访问“/admin”URL，您将收到“403 Forbidden”错误。

## 实现登录页面

为了对用户进行身份验证，您需要实现一个登录页面。登录页面可以使用标准的 HTML 表单来实现。在下面的例子中，我们使用了一个带有用户名和密码字段的简单 HTML 表单。

```html
<form action="/login" method="POST">
    <input type="text" name="username" />
    <input type="password" name="password" />
    <input type="submit" value="Login" />
</form>
```

提交表单时，调用 `/login` URL。 `/login` URL 由 Spring Security 处理，用户已通过身份验证。如果身份验证成功，用户将被重定向到最初请求的 URL。如果身份验证不成功，用户将被重定向到登录页面。

为了实现登录页面，您需要添加一个 `WebSecurityConfigurerAdapter` 并覆盖 `configure` 方法。在`configure`方法中，需要添加`formLogin`方法，并指定登录页面和登录成功页面。

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .formLogin()
                .loginPage("/login")
                .defaultSuccessUrl("/");
    }
}
```

在 `formLogin` 方法中，我们将 `/login` URL 指定为登录页面，将 `/` URL 指定为登录成功页面。

## 登出

Spring Security 还提供了对注销的支持。为了实现注销，你需要在 configure 方法中添加 logout 方法。 `logout` 方法将 `logoutSuccessUrl` 作为参数。 `logoutSuccessUrl` 是用户在成功注销后被重定向到的 URL。

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .logout()
                .logoutSuccessUrl("/login?logout");
    }
}
```

在 `logout` 方法中，我们将 `/login?logout` URL 指定为注销成功 URL。 `logout` URL 由 Spring Security 处理并且用户被注销。

## 结论

在本文中，我们了解了如何使用 Spring Security 在 Spring 应用程序中实现安全性。 Spring Security 是一个强大的框架，提供了许多开箱即用的功能。