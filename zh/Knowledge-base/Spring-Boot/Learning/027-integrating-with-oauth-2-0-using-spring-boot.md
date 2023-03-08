---
title: 027：使用 Spring Boot 与 OAuth 2.0 集成
description: 
published: true
date: 2023-02-03T19:32:37.059Z
tags: 
editor: markdown
dateCreated: 2023-02-03T19:32:35.437Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [027: Integrating with OAuth 2.0 using Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/027-integrating-with-oauth-2-0-using-spring-boot)
{.links-list}


# OAuth 2.0 和 Spring Boot

在本文中，我们将了解如何使用 Spring Boot 与 OAuth 2.0 集成。

OAuth 2.0 是一种流行的授权标准。许多大公司都在使用它，包括 Google、Facebook 和 Twitter。

Spring Boot 是一种用于构建 Web 应用程序的流行 Java 框架。

## 什么是 OAuth 2.0？

OAuth 2.0 是一种授权标准。它允许用户授权第三方应用程序访问他们的数据，而无需共享他们的密码。

例如，如果您使用 Google 登录第三方网站，则您使用的是 OAuth 2.0。第三方网站不需要您的 Google 密码；它只需要访问您的数据的权限。

## OAuth 2.0 是如何工作的？

OAuth 2.0 通过使用令牌来工作。令牌是代表用户访问其数据的权限的一段数据。

令牌由授权服务器生成。当用户授予第三方应用程序访问其数据的权限时，授权服务器会生成一个令牌。然后将令牌发送到第三方应用程序。

然后第三方应用程序可以使用令牌访问用户的数据。

## 为什么要使用 OAuth 2.0？

使用 OAuth 2.0 有几个好处：

- 这是一个标准：OAuth 2.0 是一个广泛使用的标准，因此有许多库和工具可用于它。

- 安全：OAuth 2.0 旨在确保安全。令牌由授权服务器生成，因此第三方应用程序无法猜到它们。

- 易于使用：OAuth 2.0 旨在易于使用。用户不需要记住他们使用的每个应用程序的密码。

## 如何在 Spring Boot 中使用 OAuth 2.0

Spring Boot 使使用 OAuth 2.0 变得容易。

首先，您需要将 Spring Security OAuth 依赖项添加到您的项目中：

```xml
<dependency>
    <groupId>org.springframework.security.oauth</groupId>
    <artifactId>spring-security-oauth2</artifactId>
    <version>2.3.4.RELEASE</version>
</dependency>
```

接下来，您需要配置授权服务器。授权服务器负责生成令牌。

Spring Boot 可以自动配置授权服务器。您需要做的就是将以下属性添加到您的 application.properties 文件中：

```properties
spring.security.oauth2.client.registration.client-id=<your-client-id>
spring.security.oauth2.client.registration.client-secret=<your-client-secret>
spring.security.oauth2.client.provider.oauth2.authorization-uri=https://<your-authorization-server>/oauth2/authorize
spring.security.oauth2.client.provider.oauth2.token-uri=https://<your-authorization-server>/oauth2/token
spring.security.oauth2.client.provider.oauth2.user-info-uri=https://<your-authorization-server>/oauth2/userinfo
```

将 <your-client-id> 替换为您应用程序的客户端 ID，将 <your-client-secret> 替换为您应用程序的客户端密码。

将 <your-authorization-server> 替换为您的授权服务器的 URL。

Spring Boot 将使用您提供的客户端 ID 和客户端密码自动配置授权服务器。

现在授权服务器已经配置好了，您可以开始使用它了。

首先，您需要获取访问令牌。访问令牌是允许您访问用户数据的令牌。

要获取访问令牌，您需要向授权服务器发送 POST 请求。该请求应包含以下参数：

- client_id：您的应用程序的客户端 ID
- client_secret：您的应用程序的客户端密码
- grant_type：您请求的资助类型。对于 OAuth 2.0，这应该是“authorization_code”
- 代码：您从授权服务器收到的代码
- redirect_uri：您的应用程序的重定向 URI

授权服务器将使用访问令牌进行响应。

获得访问令牌后，您可以使用它来访问用户的数据。

为此，您需要向资源服务器发送 GET 请求。该请求应包含以下参数：

- access_token：您从授权服务器收到的访问令牌

资源服务器将响应用户的数据。

## 附加信息

- OAuth 2.0 是授权标准，不是认证标准。 OAuth 2.0 可用于身份验证，但并非为此而设计。

- Spring Boot 不支持开箱即用的 OAuth 2.0。您需要将 Spring Security OAuth 依赖项添加到您的项目中。

- Spring Boot 可以自动配置授权服务器。您需要做的就是将客户端 ID 和客户端密码添加到您的 application.properties 文件中。