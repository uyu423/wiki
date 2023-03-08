---
title: 보안 및 인증을 위한 Spring Boot 및 LDAP
description: 
published: true
date: 2023-02-08T04:32:47.358Z
tags: 
editor: markdown
dateCreated: 2023-02-08T04:32:45.752Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot and LDAP for Security and Authentication***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-ldap-for-security-and-authentication)
{.links-list}


# 보안 및 인증을 위한 Spring Boot 및 LDAP

## 소개

이 기사에서는 보안 및 인증을 위해 Spring Boot 및 LDAP를 사용하는 방법을 살펴보겠습니다. 인증에 LDAP를 사용하도록 Spring Boot를 구성하는 세 가지 방법을 살펴보겠습니다.

- `spring-boot-starter-security-ldap` 종속성 사용
- 스프링 시큐리티 설정
- ApacheDS 구성

또한 Spring Boot의 자동 구성 기능을 사용하여 임베디드 LDAP 서버를 구성하는 방법도 살펴보겠습니다.

## LDAP를 사용하도록 Spring Boot 구성

인증에 LDAP를 사용하도록 Spring Boot를 구성하는 세 가지 방법이 있습니다.

### `spring-boot-starter-security-ldap` 종속성 사용

인증에 LDAP를 사용하도록 Spring Boot를 구성하는 가장 쉬운 방법은 `spring-boot-starter-security-ldap` 종속성을 사용하는 것입니다. 이 종속성은 내장된 LDAP 서버를 사용하도록 Spring Security를 자동으로 구성합니다.

`spring-boot-starter-security-ldap` 종속성을 사용하려면 `pom.xml` 파일에 다음 종속성을 추가합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security-ldap</artifactId>
</dependency>
```

### 스프링 보안 설정

LDAP 서버 구성을 더 많이 제어하려면 LDAP 서버를 사용하도록 Spring Security를 구성할 수 있습니다. 이렇게 하려면 `pom.xml` 파일에 다음 종속성을 추가해야 합니다.

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

또한 `UserDetailsService` 빈을 구성해야 합니다. `UserDetailsService` 빈은 LDAP 서버에서 사용자의 세부 정보를 로드하는 역할을 합니다.

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

위의 코드 예제에서는 `ou=people` LDAP 그룹에서 사용자를 검색하고 `ou=groups` LDAP 그룹에서 그룹을 검색하도록 `UserDetailsService`를 구성했습니다. 또한 `LdapShaPasswordEncoder` 인코더를 사용하도록 암호 인코더를 구성했습니다.

### ApacheDS 구성

더 완전한 기능을 갖춘 LDAP 서버를 사용하려는 경우 ApacheDS를 구성할 수 있습니다. 이렇게 하려면 `pom.xml` 파일에 다음 종속성을 추가해야 합니다.

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

또한 `UserDetailsService` 빈을 구성해야 합니다. `UserDetailsService` 빈은 LDAP 서버에서 사용자의 세부 정보를 로드하는 역할을 합니다.

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

위의 코드 예제에서는 `ou=people` LDAP 그룹에서 사용자를 검색하고 `ou=groups` LDAP 그룹에서 그룹을 검색하도록 `UserDetailsService`를 구성했습니다. 또한 `LdapShaPasswordEncoder` 인코더를 사용하도록 암호 인코더를 구성했습니다.

## Spring Boot의 자동 구성 기능 사용

Spring Boot의 자동 구성 기능을 사용하여 임베디드 LDAP 서버를 구성할 수 있습니다. 자동 구성 기능을 사용하려면 `pom.xml` 파일에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-autoconfigure</artifactId>
</dependency>
```

또한 `UserDetailsService` 빈을 구성해야 합니다. `UserDetailsService` 빈은 LDAP 서버에서 사용자의 세부 정보를 로드하는 역할을 합니다.

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

위의 코드 예제에서는 `ou=people` LDAP 그룹에서 사용자를 검색하고 `ou=groups` LDAP 그룹에서 그룹을 검색하도록 `UserDetailsService`를 구성했습니다. 또한 `LdapShaPasswordEncoder` 인코더를 사용하도록 암호 인코더를 구성했습니다.

## 결론

이 기사에서는 인증에 LDAP를 사용하도록 Spring Boot를 구성하는 세 가지 방법을 살펴보았습니다. 또한 Spring Boot의 자동 구성 기능을 사용하여 임베디드 LDAP 서버를 구성하는 방법도 살펴보았습니다.