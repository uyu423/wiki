---
title: 006: Spring Security로 보안 구현
description: 
published: true
date: 2023-02-03T07:45:38.200Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:45:36.281Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [006: Implementing security with Spring Security***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/006-implementing-security-with-spring-security)
{.links-list}


# 스프링 시큐리티로 보안 구현하기

Spring Security는 Java 애플리케이션에서 인증 및 권한 부여 서비스를 제공하는 프레임워크입니다. 널리 사용되는 프레임워크이며 즉시 사용할 수 있는 많은 기능을 제공합니다. 이번 포스팅에서는 스프링 시큐리티를 이용하여 스프링 애플리케이션에서 보안을 구현하는 방법에 대해 알아보도록 하겠습니다.

## 스프링 보안 설정

첫 번째 단계는 Spring Security 종속성을 프로젝트에 추가하는 것입니다. Maven을 사용하는 경우 `pom.xml` 파일에 다음 종속성을 추가할 수 있습니다.

```xml
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-core</artifactId>
    <version>5.0.0.RELEASE</version>
</dependency>
```

Gradle을 사용하는 경우 `build.gradle` 파일에 다음 종속성을 추가할 수 있습니다.

```groovy
dependencies {
    compile 'org.springframework.security:spring-security-core:5.0.0.RELEASE'
}
```

종속성이 추가되면 `SecurityConfig` 클래스를 추가하고 `@EnableWebSecurity`로 주석을 달아 Spring Security를 구성할 수 있습니다. 메모리 내 인증 또는 LDAP 인증을 사용하도록 `SecurityConfig` 클래스를 구성할 수 있습니다. 이 예에서는 메모리 내 인증을 사용합니다.

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

`configure` 메소드에서는 사용자 이름이 `user`이고 암호가 `password`인 사용자로 메모리 내 인증을 구성합니다. 사용자에게는 'USER' 역할도 있습니다.

## URL 보안

Spring Security를 구성한 후에는 `@Secured` 주석을 사용하여 URL을 보호할 수 있습니다. `@Secured` 주석은 클래스뿐만 아니라 메서드에서도 사용할 수 있습니다. 다음 예에서는 `ADMIN` 역할을 가진 사용자만 액세스할 수 있도록 `/admin` URL을 보호합니다.

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

인증 없이 `/admin` URL에 액세스하려고 하면 `403 Forbidden` 오류가 발생합니다.

## 로그인 페이지 구현

사용자를 인증하기 위해서는 로그인 페이지를 구현해야 합니다. 로그인 페이지는 표준 HTML 양식을 사용하여 구현할 수 있습니다. 다음 예에서는 사용자 이름과 암호 필드가 있는 간단한 HTML 양식을 사용하고 있습니다.

```html
<form action="/login" method="POST">
    <input type="text" name="username" />
    <input type="password" name="password" />
    <input type="submit" value="Login" />
</form>
```

양식이 제출되면 `/login` URL이 호출됩니다. `/login` URL은 Spring Security에 의해 처리되며 사용자는 인증됩니다. 인증에 성공하면 사용자는 원래 요청한 URL로 리디렉션됩니다. 인증에 실패하면 사용자는 로그인 페이지로 리디렉션됩니다.

로그인 페이지를 구현하려면 `WebSecurityConfigurerAdapter`를 추가하고 `configure` 메서드를 재정의해야 합니다. `configure` 메소드에서 `formLogin` 메소드를 추가하고 로그인 페이지와 로그인 성공 페이지를 지정해야 합니다.

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

`formLogin` 메소드에서 `/login` URL을 로그인 페이지로 지정하고 `/` URL을 로그인 성공 페이지로 지정합니다.

## 로그 아웃

Spring Security는 로그아웃도 지원합니다. 로그아웃을 구현하기 위해서는 `configure` 메소드에 `logout` 메소드를 추가해야 합니다. `logout` 메서드는 `logoutSuccessUrl`을 매개변수로 사용합니다. `logoutSuccessUrl`은 성공적인 로그아웃 후 사용자가 리디렉션되는 URL입니다.

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

`logout` 메소드에서 `/login?logout` URL을 로그아웃 성공 URL로 지정합니다. `logout` URL은 Spring Security에 의해 처리되며 사용자는 로그아웃됩니다.

## 결론

이번 포스팅에서는 스프링 시큐리티를 이용하여 스프링 애플리케이션에서 보안을 구현하는 방법에 대해 알아보았습니다. Spring Security는 즉시 사용할 수 있는 많은 기능을 제공하는 강력한 프레임워크입니다.