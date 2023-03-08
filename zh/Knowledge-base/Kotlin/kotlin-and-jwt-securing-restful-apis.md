---
title: Kotlin 和 JWT：保护 RESTful API
description: 
published: true
date: 2023-02-13T15:17:46.821Z
tags: 
editor: markdown
dateCreated: 2023-02-13T15:17:44.946Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kotlin and JWT: Securing RESTful APIs***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-jwt-securing-restful-apis)
{.links-list}


# Kotlin 和 JWT：保护 RESTful API

随着 Kotlin 作为开发 Android 应用程序的一流语言的崛起，越来越多的开发人员也对使用 Kotlin 进行服务器端开发感兴趣也就不足为奇了。在本文中，我们将了解如何使用 Kotlin 和 Java Web Tokens (JWT) 框架来保护 RESTful API。

JWT 是一种创建访问令牌的标准，允许服务器验证客户端的身份。这在 RESTful API 中尤为重要，其中客户端可以是从移动应用程序到浏览器扩展的任何东西。通过使用 JWT，我们可以确保只有授权的客户端才能访问我们的 API。

要将 JWT 与 Kotlin 结合使用，我们需要安装 kotlin-jwt 库。该库提供了一组用于创建和验证 JWT 令牌的函数。

一旦我们安装了 kotlin-jwt 库，我们就可以使用它来创建一个 JWT 令牌，如下所示：

```kotlin
val jwt = JWT.create()
    .withSubject("user@example.com")
    .withExpiresAt(Date())
    .sign(algorithm)
```

其中“algorithm”是“Algorithm”的一个实例，它指定要使用的签名算法。例如，我们可以像这样使用“HMAC256”算法：

```kotlin
val algorithm = Algorithm.HMAC256("secret")
```

然后我们可以使用 `jwt` 变量来生成一个令牌：

```kotlin
val token = jwt.generate()
```

现在我们有了一个令牌，我们可以用它来保护我们的 API。例如，我们可以将它添加到 HTTP 请求的“授权”标头中：

```kotlin
val request = Request.Builder()
    .url("https://example.com/api/v1/users")
    .header("Authorization", "Bearer $token")
    .build()
```

然后服务器可以使用 `verify` 函数来验证令牌：

```kotlin
val jwt = JWT.require(algorithm)
    .build()

val verifiedToken = jwt.verify(token)
```

如果令牌有效，`verifiedToken` 变量将包含解码后的令牌。然后我们可以使用 `getSubject` 函数来获取用户的电子邮件地址：

```kotlin
val userEmail = verifiedToken.getSubject()
```

现在我们知道如何使用 Kotlin 和 JWT 来保护 RESTful API，让我们看一些资源以进一步阅读。

## 资源

- [JSON 网络令牌](https://jwt.io/)
- [kotlin-jwt](https://github.com/kotlinc-es/kotlin-jwt)
- [Kotlin 安全](https://kotlinlang.org/docs/reference/security.html)