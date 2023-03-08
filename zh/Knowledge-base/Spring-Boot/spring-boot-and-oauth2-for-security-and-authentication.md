---
title: 用于安全和身份验证的 Spring Boot 和 OAuth2
description: 
published: true
date: 2023-02-08T03:32:23.024Z
tags: 
editor: markdown
dateCreated: 2023-02-08T03:32:21.476Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot and OAuth2 for Security and Authentication***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-oauth2-for-security-and-authentication)
{.links-list}


# 用于安全和身份验证的 Spring Boot 和 OAuth2

Spring Boot Security OAuth2 Stack 提供了一种向 Spring Boot 应用程序添加 OAuth2 保护的便捷方法。在本文中，我们将探索使用 Spring Boot 和 OAuth2 来保护简单的 REST API。我们还将使用 Spring Security 和 JWT 为我们的 REST API 添加一层安全性。

## 什么是 OAuth2？

OAuth2 是一个授权框架，它使应用程序能够获得对 HTTP 服务上的用户帐户的有限访问权限。它的工作原理是将用户身份验证委托给托管用户帐户的服务，并授权第三方应用程序访问用户帐户。 OAuth2 提供单一授权端点和单一令牌端点。

## 什么是 Spring Boot？

Spring Boot 是一个基于 Java 的框架，用于创建独立的、生产级的基于 Spring 的应用程序。它是一个约定优于配置的框架，提供了广泛的非功能性特性，例如嵌入式服务器、安全性、指标、健康检查等。

## 什么是Spring Security？

Spring Security 是一个提供身份验证、授权和针对常见攻击的保护的框架。它提供了广泛的身份验证机制，例如基于表单的身份验证、HTTP 基本身份验证等。

## 什么是智威汤逊？

JWT（JSON Web 令牌）是一种紧凑的 URL 安全方式，用于表示要在两方之间传输的声明。 JWT 中的声明被编码为 JSON 对象，用作 JSON Web 签名 (JWS) 结构的有效负载或作为 JSON Web 加密 (JWE) 结构的纯文本，使声明能够进行数字签名或完整性受消息验证码 (MAC) 保护和/或加密。

## 设置项目

我们将从使用以下依赖项设置一个简单的 Spring Boot 项目开始：

- 春季启动网站
- 春季启动安全
- Spring Boot OAuth2 安全
- 春季安全智威汤逊

可以使用具有上述依赖项的 Spring Initializr 创建项目。

## 配置 OAuth2

我们将配置我们的应用程序以使用 OAuth2 进行身份验证。 OAuth2 是一个授权框架，它使应用程序能够获得对 HTTP 服务上的用户帐户的有限访问权限。

我们需要创建一个 OAuth2ClientProperties bean 并使用我们的 OAuth2 客户端的属性对其进行配置。我们还需要创建一个 ResourceServerProperties bean 并使用我们的资源服务器的属性配置它。

## 配置 Spring 安全

我们将配置 Spring Security 来保护我们的 REST API。我们需要创建一个 WebSecurityConfigurerAdapter 并覆盖 configure(HttpSecurity) 方法。在这种方法中，我们将为我们的应用程序配置安全规则。

我们还需要创建一个 JwtAuthenticationFilter 并将其配置为执行 JWT 身份验证。

## 测试应用程序

我们可以通过使用有效的用户名和密码向 /login 端点发送 POST 请求来测试我们的应用程序。如果身份验证成功，我们应该会收到带有 JWT 令牌的 JSON 响应。

我们可以使用此令牌访问我们应用程序的受保护资源，方法是将 GET 请求发送到 /userinfo 端点，并在 Authorization 标头中包含令牌。

## 结论

在本文中，我们了解了如何使用 Spring Boot 和 OAuth2 来保护简单的 REST API。我们还了解了如何使用 Spring Security 和 JWT 为我们的 REST API 添加一层安全性。