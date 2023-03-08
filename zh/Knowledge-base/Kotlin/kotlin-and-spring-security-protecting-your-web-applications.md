---
title: Kotlin 和 Spring Security：保护您的 Web 应用程序
description: 
published: true
date: 2023-01-31T12:44:09.828Z
tags: 
editor: markdown
dateCreated: 2023-01-31T12:44:08.235Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Kotlin and Spring Security: Protecting Your Web Applications***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-spring-security-protecting-your-web-applications)
{.links-list}



# Kotlin 和 Spring Security：保护您的 Web 应用程序

开发人员越来越多地转向使用 Kotlin 进行 Web 开发。 Kotlin 是一种简洁、安全、可互操作且对工具友好的语言，运行在 Java 虚拟机上。

Spring Security 是一个功能强大且高度可定制的身份验证和访问控制框架。它是保护基于 Spring 的应用程序的事实标准。

在本文中，我们将探讨如何使用 Kotlin 和 Spring Security 来保护 Web 应用程序。我们将了解如何配置 Spring Security 并编写 Kotlin 代码来实现身份验证、授权和密码加密等常见安全功能。

## 配置 Spring 安全

 可以使用 Java 或 Kotlin 代码配置 Spring Security。在本节中，我们将了解如何使用 Kotlin 配置 Spring Security。

### 添加 Spring Security 依赖

要将 Spring Security 添加到您的项目，请将以下依赖项添加到您的 `build.gradle.kts` 文件中：

```kotlin
implementation("org.springframework.boot:spring-boot-starter-security")
implementation("org.springframework.security.oauth.boot:spring-security-oauth2-autoconfigure")
```

### 创建一个 SecurityConfig 类

接下来，我们将创建一个“SecurityConfig”类来配置 Spring Security。此类将扩展 `WebSecurityConfigurerAdapter` 并覆盖其 `configure` 方法：

```kotlin
@Configuration
@EnableWebSecurity
class SecurityConfig : WebSecurityConfigurerAdapter() {

    override fun configure(http: HttpSecurity) {
        // ...
    }
}
```

在 configure 方法中，我们可以配置 Spring Security 的各个方面，例如身份验证、授权和会话管理。

### 配置身份验证

Spring Security 支持广泛的身份验证机制，从简单的用户名/密码身份验证到更复杂的机制，如 OAuth2 和 LDAP。

在此示例中，我们将配置 Spring Security 以使用用户名/密码身份验证。我们将使用 UserDetailsService 接口将用户名和密码存储在数据库中：

```kotlin
@Configuration
@EnableWebSecurity
class SecurityConfig : WebSecurityConfigurerAdapter() {

    override fun configure(http: HttpSecurity) {
        http.authorizeRequests()
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .and()
            .httpBasic()
                .and()
            .logout()
    }

    @Autowired
    fun configureGlobal(auth: AuthenticationManagerBuilder) {
        auth.inMemoryAuthentication()
                .withUser("user").password("{noop}password").roles("USER")
    }
}
```

在上面的代码中，我们将 Spring Security 配置为使用用户名/密码身份验证。我们还配置了一个 UserDetailsService 来将用户名和密码存储在内存中。

### 配置授权

用户通过身份验证后，我们需要配置授权来控制他们可以在应用程序中执行的操作。

Spring Security 支持两种类型的授权：

* 基于角色的授权：用户的角色决定了他们可以在应用程序中做什么。
* 基于资源的授权：用户的权限决定了他们可以在应用程序中做什么。

在此示例中，我们将配置基于角色的授权。我们将配置两个角色：`USER` 和 `ADMIN`。具有“USER”角色的用户将能够访问“/user”端点，而具有“ADMIN”角色的用户将能够访问“/admin”端点：

```kotlin
@Configuration
@EnableWebSecurity
class SecurityConfig : WebSecurityConfigurerAdapter() {

    override fun configure(http: HttpSecurity) {
        http.authorizeRequests()
                .antMatchers("/user").hasRole("USER")
                .antMatchers("/admin").hasRole("ADMIN")
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .and()
            .httpBasic()
                .and()
            .logout()
    }

    @Autowired
    fun configureGlobal(auth: AuthenticationManagerBuilder) {
        auth.inMemoryAuthentication()
                .withUser("user").password("{noop}password").roles("USER")
                .and()
                .withUser("admin").password("{noop}password").roles("ADMIN")
    }
}
```

在上面的代码中，我们使用 `hasRole` 方法配置了基于角色的授权。我们还配置了一个 UserDetailsService 来将用户名和密码存储在内存中。

### 配置密码加密

Spring Security 支持多种密码加密算法。在此示例中，我们将配置 Spring Security 以使用 `bcrypt` 算法：

```kotlin
@Configuration
@EnableWebSecurity
class SecurityConfig : WebSecurityConfigurerAdapter() {

    override fun configure(http: HttpSecurity) {
        http.authorizeRequests()
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .and()
            .httpBasic()
                .and()
            .logout()
                .and()
            .apply {
                passwordEncoder(BCryptPasswordEncoder())
            }
    }

    @Autowired
    fun configureGlobal(auth: AuthenticationManagerBuilder) {
        auth.inMemoryAuthentication()
                .withUser("user").password("{noop}password").roles("USER")
                .and()
                .withUser("admin").password("{noop}password").roles("ADMIN")
    }
}
```

在上面的代码中，我们将 Spring Security 配置为使用 BCryptPasswordEncoder 来加密密码。我们还配置了一个 UserDetailsService 来将用户名和密码存储在内存中。

## 编写 Kotlin 代码

在本节中，我们将了解如何编写 Kotlin 代码来实现身份验证、授权和密码加密等常见安全功能。

### 验证用户

要对用户进行身份验证，我们将使用“authenticationManager.authenticate”方法：

```kotlin
@Configuration
@EnableWebSecurity
class SecurityConfig : WebSecurityConfigurerAdapter() {

    override fun configure(http: HttpSecurity) {
        http.authorizeRequests()
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .and()
            .httpBasic()
                .and()
            .logout()
    }

    @Autowired
    fun configureGlobal(auth: AuthenticationManagerBuilder) {
        auth.inMemoryAuthentication()
                .withUser("user").password("{noop}password").roles("USER")
                .and()
                .withUser("admin").password("{noop}password").roles("ADMIN")
    }

    @Autowired
    fun authenticationManager(): AuthenticationManager {
        return authenticationManager()
    }
}
```

在上面的代码中，我们将 `AuthenticationManager` 注入到我们的 `SecurityConfig` 类中。然后我们可以使用 `authenticationManager.authenticate` 方法来验证用户。

### 授权用户

要授权用户，我们将使用 `hasRole` 方法：

```kotlin
@Configuration
@EnableWebSecurity
class SecurityConfig : WebSecurityConfigurerAdapter() {

    override fun configure(http: HttpSecurity) {
        http.authorizeRequests()
                .antMatchers("/user").hasRole("USER")
                .antMatchers("/admin").hasRole("ADMIN")
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .and()
            .httpBasic()
                .and()
            .logout()
    }

    @Autowired
    fun configureGlobal(auth: AuthenticationManagerBuilder) {
        auth.inMemoryAuthentication()
                .withUser("user").password("{noop}password").roles("USER")
                .and()
                .withUser("admin").password("{noop}password").roles("ADMIN")
    }
}
```

在上面的代码中，我们使用了 `hasRole` 方法来授权用户。我们还配置了一个 UserDetailsService 来将用户名和密码存储在内存中。

### 加密密码

要加密密码，我们将使用 passwordEncoder 方法：

```kotlin
@Configuration
@EnableWebSecurity
class SecurityConfig : WebSecurityConfigurerAdapter() {

    override fun configure(http: HttpSecurity) {
        http.authorizeRequests()
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .and()
            .httpBasic()
                .and()
            .logout()
                .and()
            .apply {
                passwordEncoder(BCryptPasswordEncoder())
            }
    }

    @Autowired
    fun configureGlobal(auth: AuthenticationManagerBuilder) {
        auth.inMemoryAuthentication()
                .withUser("user").password("{noop}password").roles("USER")
                .and()
                .withUser("admin").password("{noop}password").roles("ADMIN")
    }
}
```

在上面的代码中，我们使用了 passwordEncoder 方法来加密密码。我们还配置了一个 UserDetailsService 来将用户名和密码存储在内存中。

## 结论

在本文中，我们探讨了如何使用 Kotlin 和 Spring Security 来保护 Web 应用程序。我们已经了解了如何配置 Spring Security 和编写 Kotlin 代码来实现常见的安全功能，例如身份验证、授权和密码加密。