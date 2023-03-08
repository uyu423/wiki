---
title: 006: Implementing security with Spring Security
description: 
published: true
date: 2023-02-03T07:45:41.230Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:45:36.286Z
---

- [006: Implementando seguridad con Spring Security***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/006-implementing-security-with-spring-security)
{.links-list}
- [006：使用 Spring Security 实现安全性***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/006-implementing-security-with-spring-security)
{.links-list}
- [006: Spring Security로 보안 구현***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/006-implementing-security-with-spring-security)
{.links-list}


# Implementing security with Spring Security

Spring Security is a framework that provides authentication and authorization services in Java applications. It is a widely used framework and provides a lot of features out of the box. In this post, we will take a look at how to implement security in a Spring application using Spring Security.

## Configuring Spring Security

The first step is to add the Spring Security dependency to your project. If you are using Maven, you can add the following dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-core</artifactId>
    <version>5.0.0.RELEASE</version>
</dependency>
```

If you are using Gradle, you can add the following dependency to your `build.gradle` file:

```groovy
dependencies {
    compile 'org.springframework.security:spring-security-core:5.0.0.RELEASE'
}
```

Once the dependency is added, you can configure Spring Security by adding a `SecurityConfig` class and annotating it with `@EnableWebSecurity`. The `SecurityConfig` class can be configured to use in-memory authentication or LDAP authentication. In this example, we will use in-memory authentication.

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

In the `configure` method, we are configuring an in-memory authentication with a user that has the username `user` and password `password`. The user also has the role `USER`.

## Securing URLs

Once you have configured Spring Security, you can secure URLs by using the `@Secured` annotation. The `@Secured` annotation can be used on methods as well as on classes. In the following example, we are securing the `/admin` URL so that only users with the `ADMIN` role can access it.

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

If you try to access the `/admin` URL without being authenticated, you will get a `403 Forbidden` error.

## Implementing a login page

In order to authenticate users, you need to implement a login page. The login page can be implemented using a standard HTML form. In the following example, we are using a simple HTML form with a username and password field.

```html
<form action="/login" method="POST">
    <input type="text" name="username" />
    <input type="password" name="password" />
    <input type="submit" value="Login" />
</form>
```

When the form is submitted, the `/login` URL is called. The `/login` URL is handled by Spring Security and the user is authenticated. If the authentication is successful, the user is redirected to the originally requested URL. If the authentication is unsuccessful, the user is redirected to the login page.

In order to implement the login page, you need to add a `WebSecurityConfigurerAdapter` and override the `configure` method. In the `configure` method, you need to add the `formLogin` method and specify the login page and the login success page.

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

In the `formLogin` method, we are specifying the `/login` URL as the login page and the `/` URL as the login success page.

## Logout

Spring Security also provides support for logging out. In order to implement logout, you need to add the `logout` method to the `configure` method. The `logout` method takes a `logoutSuccessUrl` as a parameter. The `logoutSuccessUrl` is the URL that the user is redirected to after a successful logout.

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

In the `logout` method, we are specifying the `/login?logout` URL as the logout success URL. The `logout` URL is handled by Spring Security and the user is logged out.

## Conclusion

In this post, we have seen how to implement security in a Spring application using Spring Security. Spring Security is a powerful framework that provides a lot of features out of the box.