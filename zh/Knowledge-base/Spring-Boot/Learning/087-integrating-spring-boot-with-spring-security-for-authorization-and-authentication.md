---
title: 087：将 Spring Boot 与 Spring Security 集成以进行授权和身份验证
description: 
published: true
date: 2023-02-05T17:32:21.517Z
tags: 
editor: markdown
dateCreated: 2023-02-05T17:32:16.203Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [087: Integrating Spring Boot with Spring Security for Authorization and Authentication***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/087-integrating-spring-boot-with-spring-security-for-authorization-and-authentication)
{.links-list}


# 087：将 Spring Boot 与 Spring Security 集成以进行授权和身份验证

在本文中，我们将学习如何将 Spring Boot 与 Spring Security 集成以进行授权和身份验证。

## 为什么选择 Spring Security？

Spring Security 是一个功能强大且高度可定制的身份验证和授权框架。它是保护基于 Spring 的应用程序的事实标准。

## 你需要什么

- 文本编辑器或 IDE
- JDK 8 或更高版本
- 行家 3.0+

## 如何将 Spring Boot 与 Spring Security 集成

1. 将 Spring Security 依赖项添加到您的 `pom.xml` 文件中：

```xml
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-security</artifactId>
	</dependency>
</dependencies>
```

2. 创建一个“SecurityConfig.java”文件并用“@EnableWebSecurity”注释：

```java
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

}
```

3. 配置“SecurityConfig”类以满足您的需要。例如，您可能想要添加一个“@Configuration”注解：

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

}
```

4. 你也可以添加`@EnableGlobalMethodSecurity`来启用方法级安全：

```java
@Configuration
@EnableWebSecurity
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class SecurityConfig extends WebSecurityConfigurerAdapter {

}
```

5. 在 `SecurityConfig` 类中，覆盖 `configure(HttpSecurity)` 方法来配置安全设置：

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

6. 您还可以配置 Spring Security 以使用内存中的身份验证存储：

```java
@Override
protected void configure(AuthenticationManagerBuilder auth) throws Exception {
	auth
		.inMemoryAuthentication()
			.withUser("user").password("password").roles("USER");
}
```

## 测试集成

1. 要测试集成，启动应用程序并导航到“http://localhost:8080/login”。您应该会看到登录页面：

![Spring Security 登录页面](https://i.imgur.com/zFw8YxG.png)

2. 从`configure(AuthenticationManagerBuilder)` 方法中输入用户名和密码，然后单击“登录”。您应该看到“欢迎”页面：

![Spring Security 欢迎页面](https://i.imgur.com/ZUwLNcu.png)

## 恭喜！

您已成功将 Spring Boot 与 Spring Security 集成。