---
title: 用于安全和身份验证的 Spring Boot 和 LDAP
description: 
published: true
date: 2023-02-08T04:32:47.379Z
tags: 
editor: markdown
dateCreated: 2023-02-08T04:32:45.753Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot and LDAP for Security and Authentication***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-ldap-for-security-and-authentication)
{.links-list}


# 用于安全和身份验证的 Spring Boot 和 LDAP

## 介绍

在本文中，我们将了解如何使用 Spring Boot 和 LDAP 进行安全和身份验证。我们将探索三种不同的方式来配置 Spring Boot 以使用 LDAP 进行身份验证：

- 通过使用 `spring-boot-starter-security-ldap` 依赖
- 通过配置 Spring Security
- 通过配置 ApacheDS

我们还将了解如何使用 Spring Boot 的自动配置功能来配置嵌入式 LDAP 服务器。

## 配置 Spring Boot 以使用 LDAP

可以通过三种不同的方式将 Spring Boot 配置为使用 LDAP 进行身份验证。

### 使用 `spring-boot-starter-security-ldap` 依赖

将 Spring Boot 配置为使用 LDAP 进行身份验证的最简单方法是使用 spring-boot-starter-security-ldap 依赖项。此依赖项将自动配置 Spring Security 以使用嵌入式 LDAP 服务器。

要使用 `spring-boot-starter-security-ldap` 依赖项，请将以下依赖项添加到您的 `pom.xml` 文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security-ldap</artifactId>
</dependency>
```

### 配置 Spring 安全

如果你想更多地控制 LDAP 服务器的配置，你可以将 Spring Security 配置为使用 LDAP 服务器。为此，您需要将以下依赖项添加到 `pom.xml` 文件中：

```xml
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-ldap</artifactId>
</dependency>
<dependency>
    <groupId>org.apache.directory.server</groupId>
    <artifactId>apacheds-all</artifactId>
</dependency>
```

您还需要配置 UserDetailsService bean。 `UserDetailsService` bean 负责从 LDAP 服务器加载用户的详细信息。

```java
@Configuration
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .anyRequest().fullyAuthenticated()
                .and()
            .formLogin();
    }

    @Override
    public void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth
            .ldapAuthentication()
                .userDnPatterns("uid={0},ou=people")
                .groupSearchBase("ou=groups")
                .contextSource()
                    .url("ldap://localhost:10389/dc=springframework,dc=org")
                    .and()
                .passwordCompare()
                    .passwordEncoder(new LdapShaPasswordEncoder())
                    .passwordAttribute("userPassword");
    }
}
```

在上面的代码示例中，我们配置了 `UserDetailsService` 以在 `ou=people` LDAP 组中搜索用户，并在 `ou=groups` LDAP 组中搜索组。我们还配置了密码编码器以使用“LdapShaPasswordEncoder”编码器。

### 配置 ApacheDS

如果你想使用功能更全的 LDAP 服务器，你可以配置 ApacheDS。为此，您需要将以下依赖项添加到 `pom.xml` 文件中：

```xml
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-ldap</artifactId>
</dependency>
<dependency>
    <groupId>org.apache.directory.server</groupId>
    <artifactId>apacheds-all</artifactId>
</dependency>
```

您还需要配置 UserDetailsService bean。 `UserDetailsService` bean 负责从 LDAP 服务器加载用户的详细信息。

```java
@Configuration
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .anyRequest().fullyAuthenticated()
                .and()
            .formLogin();
    }

    @Override
    public void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth
            .ldapAuthentication()
                .userDnPatterns("uid={0},ou=people")
                .groupSearchBase("ou=groups")
                .contextSource()
                    .url("ldap://localhost:10389/dc=springframework,dc=org")
                    .and()
                .passwordCompare()
                    .passwordEncoder(new LdapShaPasswordEncoder())
                    .passwordAttribute("userPassword");
    }
}
```

在上面的代码示例中，我们配置了 `UserDetailsService` 以在 `ou=people` LDAP 组中搜索用户，并在 `ou=groups` LDAP 组中搜索组。我们还配置了密码编码器以使用“LdapShaPasswordEncoder”编码器。

## 使用 Spring Boot 的自动配置功能

Spring Boot 的自动配置功能可用于配置嵌入式 LDAP 服务器。要使用自动配置功能，您需要将以下依赖项添加到您的 `pom.xml` 文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-autoconfigure</artifactId>
</dependency>
```

您还需要配置 UserDetailsService bean。 `UserDetailsService` bean 负责从 LDAP 服务器加载用户的详细信息。

```java
@Configuration
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .anyRequest().fullyAuthenticated()
                .and()
            .formLogin();
    }

    @Override
    public void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth
            .ldapAuthentication()
                .userDnPatterns("uid={0},ou=people")
                .groupSearchBase("ou=groups")
                .contextSource()
                    .url("ldap://localhost:10389/dc=springframework,dc=org")
                    .and()
                .passwordCompare()
                    .passwordEncoder(new LdapShaPasswordEncoder())
                    .passwordAttribute("userPassword");
    }
}
```

在上面的代码示例中，我们配置了 `UserDetailsService` 以在 `ou=people` LDAP 组中搜索用户，并在 `ou=groups` LDAP 组中搜索组。我们还配置了密码编码器以使用“LdapShaPasswordEncoder”编码器。

## 结论

在本文中，我们探索了三种不同的方法来配置 Spring Boot 以使用 LDAP 进行身份验证。我们还了解了如何使用 Spring Boot 的自动配置功能来配置嵌入式 LDAP 服务器。