---
title: Spring Boot and LDAP for Security and Authentication
description: 
published: true
date: 2023-02-08T04:32:51.665Z
tags: 
editor: markdown
dateCreated: 2023-02-08T04:32:45.755Z
---

- [Spring Boot y LDAP para seguridad y autenticación***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-and-ldap-for-security-and-authentication)
{.links-list}
- [用于安全和身份验证的 Spring Boot 和 LDAP***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-and-ldap-for-security-and-authentication)
{.links-list}
- [보안 및 인증을 위한 Spring Boot 및 LDAP***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-and-ldap-for-security-and-authentication)
{.links-list}


# Spring Boot and LDAP for Security and Authentication

## Introduction

In this article, we'll take a look at how to use Spring Boot and LDAP for security and authentication. We'll explore three different ways to configure Spring Boot to use LDAP for authentication:

- by using the `spring-boot-starter-security-ldap` dependency
- by configuring Spring Security
- by configuring ApacheDS

We'll also look at how to use Spring Boot's auto-configuration feature to configure an embedded LDAP server.

## Configuring Spring Boot to Use LDAP

There are three different ways to configure Spring Boot to use LDAP for authentication.

### Using the `spring-boot-starter-security-ldap` Dependency

The easiest way to configure Spring Boot to use LDAP for authentication is to use the `spring-boot-starter-security-ldap` dependency. This dependency will automatically configure Spring Security to use an embedded LDAP server.

To use the `spring-boot-starter-security-ldap` dependency, add the following dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security-ldap</artifactId>
</dependency>
```

### Configuring Spring Security

If you want more control over the configuration of the LDAP server, you can configure Spring Security to use an LDAP server. To do this, you need to add the following dependencies to your `pom.xml` file:

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

You also need to configure the `UserDetailsService` bean. The `UserDetailsService` bean is responsible for loading the user's details from the LDAP server.

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

In the code example above, we've configured the `UserDetailsService` to search for users in the `ou=people` LDAP group and to search for groups in the `ou=groups` LDAP group. We've also configured the password encoder to use the `LdapShaPasswordEncoder` encoder.

### Configuring ApacheDS

If you want to use a more fully-featured LDAP server, you can configure ApacheDS. To do this, you need to add the following dependency to your `pom.xml` file:

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

You also need to configure the `UserDetailsService` bean. The `UserDetailsService` bean is responsible for loading the user's details from the LDAP server.

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

In the code example above, we've configured the `UserDetailsService` to search for users in the `ou=people` LDAP group and to search for groups in the `ou=groups` LDAP group. We've also configured the password encoder to use the `LdapShaPasswordEncoder` encoder.

## Using Spring Boot's Auto-Configuration Feature

Spring Boot's auto-configuration feature can be used to configure an embedded LDAP server. To use the auto-configuration feature, you need to add the following dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-autoconfigure</artifactId>
</dependency>
```

You also need to configure the `UserDetailsService` bean. The `UserDetailsService` bean is responsible for loading the user's details from the LDAP server.

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

In the code example above, we've configured the `UserDetailsService` to search for users in the `ou=people` LDAP group and to search for groups in the `ou=groups` LDAP group. We've also configured the password encoder to use the `LdapShaPasswordEncoder` encoder.

## Conclusion

In this article, we've explored three different ways to configure Spring Boot to use LDAP for authentication. We've also looked at how to use Spring Boot's auto-configuration feature to configure an embedded LDAP server.