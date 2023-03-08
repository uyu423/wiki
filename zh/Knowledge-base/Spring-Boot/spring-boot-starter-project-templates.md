---
title: Spring Boot 入门项目模板
description: 
published: true
date: 2023-02-01T18:57:52.715Z
tags: 
editor: markdown
dateCreated: 2023-02-01T18:57:48.592Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Spring Boot Starter Project Templates***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-starter-project-templates)
{.links-list}


# Spring Boot 入门项目模板

开发 Spring Boot 应用程序可能是一项艰巨的任务。有许多活动部件，可能很难知道从哪里开始。这就是 Spring Boot 入门项目模板的用武之地。

入门项目模板是一个预配置的 Spring Boot 应用程序，您可以将其用作您自己的应用程序的起点。这些模板是快速启动和运行的好方法，而且不会大惊小怪。

在本文中，我们将了解一些最流行的入门项目模板，看看它们如何帮助您启动 Spring Boot 应用程序。

## Spring Boot Web 启动器

Spring Boot Web Starter 是最流行的入门项目模板。它提供了启动和运行基本 Spring Boot Web 应用程序所需的一切。

Web Starter 包括以下依赖项：

- spring-boot-starter-web
- spring-boot-starter-tomcat
- spring-boot-starter-thymeleaf

它还包括以下主要功能：

- 嵌入式Tomcat
- 支持 Thymeleaf 模板
- Spring MVC 的自动配置

Web Starter 的入门很简单。您可以使用 Spring Initializr 并从启动器列表中选择 Web Starter 创建一个新项目。

设置项目后，您可以添加一个控制器来处理对应用程序的请求。例如，以下控制器会将请求映射到名为“index.html”的 Thymeleaf 模板的“/”路径：

```java
@Controller
public class IndexController {

    @RequestMapping("/")
    public String index() {
        return "index";
    }

}
```

然后，您可以将“index.html”模板添加到“src/main/resources/templates”目录中。 Web Starter 将自动配置 Thymeleaf，您将能够通过“http://localhost:8080/”访问您的模板。

## Spring Boot 数据 JPA 启动器

Spring Boot Data JPA Starter 是另一个流行的入门项目模板。它提供了开始使用 Spring Data JPA 所需的一切。

Data JPA Starter 包括以下依赖项：

- spring-boot-starter-data-jpa
- spring-boot-starter-aop
- spring-boot-starter-jdbc

它还包括以下主要功能：

- Spring Data JPA 的自动配置
- 支持交易
- 支持审计

Data JPA Starter 的入门与 Web Starter 一样简单。您可以使用 Spring Initializr 并从启动器列表中选择 Data JPA Starter 创建一个新项目。

设置项目后，您可以添加一个 JPA 实体来表示您的数据。例如，以下实体表示用户：

```java
@Entity
public class User {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    private String email;

    // Getters and setters...

}
```

然后，您可以添加一个存储库接口来访问您的数据。以下存储库将提供通过 ID 或电子邮件查找用户的方法：

```java
public interface UserRepository extends JpaRepository<User, Long> {

    User findById(Long id);

    User findByEmail(String email);

}
```

Spring Data JPA 会自动为你实现这个接口。然后您可以将存储库注入您的控制器并使用它来访问您的数据。

## Spring Boot 安全入门

对于需要提供身份验证和授权的应用程序，Spring Boot Security Starter 是一个很好的起点。

Security Starter 包括以下依赖项：

- spring-boot-starter-security
- 弹簧安全配置

它还包括以下主要功能：

- Spring Security 的自动配置
- 支持基于表单的身份验证
- 静态资源的安全性

Security Starter 的入门与其他入门工具一样简单。您可以使用 Spring Initializr 并从启动器列表中选择 Security Starter 创建一个新项目。

设置项目后，您可以向应用程序添加安全配置。例如，以下配置将保护所有具有 `/admin` 路径的 URL：

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/admin/**").hasRole("ADMIN")
                .anyRequest().permitAll()
            .and()
            .formLogin()
                .loginPage("/login")
                .permitAll();
    }

}
```

此配置将保护所有具有“/admin”路径的 URL，并要求用户使用“ADMIN”角色进行身份验证。它还会在“/login”处提供一个登录页面，允许用户进行身份验证。

## Spring Boot 执行器启动器

对于需要提供监控和管理功能的应用程序来说，Spring Boot Actuator Starter 是一个很好的起点。

Actuator Starter 包括以下依赖项：

- 弹簧启动启动器执行器

它还包括以下主要功能：

- Spring Boot Actuator 的自动配置
- 应用程序监控和管理端点

Actuator 启动器的入门与其他启动器一样简单。您可以使用 Spring Initializr 并从启动器列表中选择 Actuator Starter 创建一个新项目。

设置项目后，您可以将执行器端点添加到您的应用程序。例如，以下配置将启用 `info` 和 `health` 端点：

```java
@Configuration
@EnableWebSecurity
public class ActuatorConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/actuator/**").permitAll()
                .anyRequest().authenticated()
            .and()
            .httpBasic();
    }

}
```

此配置将启用“信息”和“健康”端点。这些端点提供有关应用程序及其运行状况的信息。

## 结论

入门项目模板是快速启动和运行的好方法，而且不会大惊小怪。它们可以为您的应用程序提供一个很好的起点，并可以为您节省大量时间和精力。

在本文中，我们研究了一些最流行的入门项目模板，并了解了它们如何帮助您启动 Spring Boot 应用程序。