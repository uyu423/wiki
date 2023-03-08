---
title: Kotlin 安全：实施 OAuth 和 JWT
description: 
published: true
date: 2023-02-09T01:17:53.595Z
tags: 
editor: markdown
dateCreated: 2023-02-09T01:17:51.921Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kotlin Security: Implementing OAuth and JWT***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-security-implementing-oauth-and-jwt)
{.links-list}


# Kotlin 安全：实施 OAuth 和 JWT

在本文中，我们将了解如何使用 OAuth 和 JSON Web 令牌 (JWT) 在 Kotlin 应用程序中实现安全性。我们还将探索这样做的一些最佳实践。

## 什么是 OAuth？

OAuth 是授权的开放标准，它使第三方应用程序无需存储和管理用户凭据即可访问资源。它通过将授权委托给资源所有者（即用户）来做到这一点。

Web 应用程序通常使用 OAuth 来允许用户使用来自其他服务（例如 Facebook 或 Google）的现有凭据登录。这被称为“第三方认证”。

## 什么是智威汤逊？

JSON Web Token (JWT) 是一种开放标准，它定义了一种紧凑且独立的方式来在各方之间将数据传输为 JSON 对象。该数据可以被验证和信任，因为它是经过数字签名的。

JWT 通常用于身份验证和授权场景，因为它们可用于安全地传输有关用户的信息。

## 在 Kotlin 中实现 OAuth

让我们来看看如何在 Kotlin 应用程序中实现 OAuth。我们将使用 [ScribeJava](https://github.com/scribejava/scribejava) 库来简化该过程。

首先，我们需要将 ScribeJava 库添加到我们的项目依赖项中：

```kotlin
// build.gradle

repositories {
    mavenCentral()
}

dependencies {
    implementation("com.github.scribejava:scribejava-core:2.5.3")
}
```

接下来，我们需要创建一个代表我们的 OAuth 服务的类。此类将负责配置 OAuth 流程并处理与 OAuth 提供程序的交互。

对于此示例，我们将使用 Facebook OAuth API：

```kotlin
// FacebookOAuthService.kt

import com.github.scribejava.apis.FacebookApi
import com.github.scribejava.core.builder.ServiceBuilder
import com.github.scribejava.core.model.OAuth2AccessToken
import com.github.scribejava.core.model.OAuthRequest
import com.github.scribejava.core.model.Verb
import com.github.scribejava.core.oauth.OAuth20Service

class FacebookOAuthService(
    private val clientId: String,
    private val clientSecret: String,
    private val callbackUrl: String
) {
    private val service: OAuth20Service = ServiceBuilder(clientId)
        .apiSecret(clientSecret)
        .callback(callbackUrl)
        .build(FacebookApi.instance())

    fun getAuthorizationUrl(): String {
        return service.getAuthorizationUrl()
    }

    fun getAccessToken(code: String): OAuth2AccessToken {
        return service.getAccessToken(code)
    }

    fun getUserProfile(accessToken: OAuth2AccessToken): String {
        val request = OAuthRequest(Verb.GET, "https://graph.facebook.com/me")
        service.signRequest(accessToken, request)

        return service.execute(request).body
    }
}
```

在 getUserProfile 方法中，我们使用 Facebook Graph API 来获取当前用户的个人资料。

现在我们有了 OAuth 服务类，让我们看看如何在 Kotlin 应用程序中使用它。

首先，我们需要创建一个路由，将用户重定向到 OAuth 提供者的登录页面：

```kotlin
// OAuthController.kt

import org.springframework.stereotype.Controller
import org.springframework.web.bind.annotation.GetMapping
import org.springframework.web.bind.annotation.RequestMapping
import org.springframework.web.bind.annotation.RequestParam
import org.springframework.web.servlet.view.RedirectView

@Controller
@RequestMapping("/oauth")
class OAuthController(
    private val facebookOAuthService: FacebookOAuthService
) {
    @GetMapping("/login")
    fun login(): RedirectView {
        val authorizationUrl = facebookOAuthService.getAuthorizationUrl()
        return RedirectView(authorizationUrl)
    }
}
```

`login` 路由将用户重定向到 Facebook 登录页面。用户登录后，他们将被重定向回“回调”路由。

接下来，我们需要创建“回调”路由。此路由负责从 OAuth 提供程序获取访问令牌，然后获取用户的配置文件：

```kotlin
// OAuthController.kt (continued)

@GetMapping("/callback")
fun callback(@RequestParam("code") code: String): String {
    val accessToken = facebookOAuthService.getAccessToken(code)
    val userProfile = facebookOAuthService.getUserProfile(accessToken)

    // ...

    return "redirect:/"
}
```

## 在 Kotlin 中实现 JWT

现在我们已经了解了如何实现 OAuth，让我们来看看如何在 Kotlin 中实现 JWT。我们将使用 [Kotlin-JWT](https://github.com/kittinunf/kotlin-jwt) 库来简化流程。

首先，我们需要将 Kotlin-JWT 库添加到我们的项目依赖项中：

```kotlin
// build.gradle

repositories {
    mavenCentral()
}

dependencies {
    implementation("com.auth0:kotlin-jwt:3.3.0")
}
```

接下来，我们需要创建一个代表 JWT 服务的类。此类将负责创建和验证 JWT 令牌。

对于这个例子，我们将使用 HS256 算法：

```kotlin
// JWTService.kt

import com.auth0.jwt.JWT
import com.auth0.jwt.algorithms.Algorithm
import com.auth0.jwt.exceptions.JWTVerificationException
import java.util.*

class JWTService(private val secret: String) {
    private val algorithm = Algorithm.HMAC256(secret)

    fun generateToken(claims: Map<String, Any>): String {
        return JWT.create()
            .withClaim("iss", "kotlin-jwt-demo")
            .withClaim("iat", Date())
            .withClaim("exp", Date(Date().time + 60 * 60 * 1000)) // 1 hour
            .withClaim("sub", "user@example.com")
            .withClaim("aud", "https://example.com")
            .withClaim("nbf", Date())
            .withClaim("jti", UUID.randomUUID().toString())
            .withClaim("foo", "bar")
            .withClaim("foo2", "baz")
            .withClaim("qaz", "wsx")
            .sign(algorithm)
    }

    fun verifyToken(token: String): Boolean {
        return try {
            JWT.require(algorithm).build().verify(token)
            true
        } catch (e: JWTVerificationException) {
            false
        }
    }
}
```

在 `generateToken` 方法中，我们使用 `withClaim` 方法来指定我们想要包含在令牌中的声明。

现在我们有了 JWT 服务类，让我们看看如何在 Kotlin 应用程序中使用它。

首先，我们需要创建一个生成 JWT 令牌的路由：

```kotlin
// JWTController.kt

import org.springframework.web.bind.annotation.GetMapping
import org.springframework.web.bind.annotation.RequestMapping
import org.springframework.web.bind.annotation.RestController

@RestController
@RequestMapping("/jwt")
class JWTController(
    private val jwtService: JWTService
) {
    @GetMapping("/generate")
    fun generateToken(): String {
        return jwtService.generateToken(emptyMap())
    }
}
```

`generateToken` 路由生成一个没有声明的 JWT 令牌。

接下来，我们需要创建一个验证 JWT 令牌的路由：

```kotlin
// JWTController.kt (continued)

@GetMapping("/verify")
fun verifyToken(@RequestParam("token") token: String): Boolean {
    return jwtService.verifyToken(token)
}
```

`verifyToken` 路由验证 JWT 令牌是否有效。

## 最佳实践

在 Kotlin 应用程序中实现安全性时，需要牢记一些最佳实践：

- **使用 OAuth 进行身份验证，而不是授权。** OAuth 是一种用于授权而非身份验证的开放标准。虽然它可以用于这两个目的，但最好将它用于授权（即将授权委托给资源所有者）并使用其他方法（例如 JWT）进行身份验证。

- **使用 JWT 进行身份验证，而不是授权。** 虽然 JWT 可以用于两种目的，但最好将其用于身份验证（即传输有关用户的信息）并使用其他方法（例如 OAuth）进行授权。

- **不要在 JWT 声明中存储敏感数据。** JWT 声明是公开的，任何人都可以阅读。因此，重要的是不要在 JWT 声明中存储敏感数据，例如用户密码。

- **使用安全密钥对 JWT 令牌进行签名。**用于对 JWT 令牌进行签名的密钥应保密，不得在应用程序中进行硬编码。执行此操作的一个好方法是使用环境变量。

- **验证 JWT 令牌时验证 `iss` 声明。** `iss`（发行者）声明用于标识 JWT 令牌的来源。验证 JWT 令牌时，重要的是要验证 `iss` 声明是否与预期值匹配。

- **在验证 JWT 令牌时验证 `aud` 声明。** `aud`（受众）声明用于标识 JWT 令牌的预期接收者。验证 JWT 令牌时，验证 `aud` 声明是否与预期值匹配非常重要。

- **在验证 JWT 令牌时验证 `exp` 声明。** `exp`（到期）声明用于指定 JWT 令牌的到期日期。验证 JWT 令牌时，验证当前日期是否在到期日期之前很重要。

- **在验证 JWT 令牌时验证 `nbf` 声明。** `nbf`（不早于）声明用于指定不得接受 JWT 令牌进行处理的日期。验证 JWT 令牌时，重要的是要验证当前日期是否在不早于日期之后。

- **在验证 JWT 令牌时验证 `jti` 声明。** `jti` (JWT ID) 声明用于为 JWT 令牌提供唯一标识符。验证 JWT 令牌时，重要的是要验证 `jti` 声明是否存在并且它的值是唯一的。

- **不要使用基本身份验证。** 虽然基本身份验证实施起来很简单，但它不是很安全。最好使用更安全的方法，例如 OAuth 或 JWT。

- **不要使用相同的秘密来签署 JWT 令牌和加密数据。**虽然为这两个目的使用相同的秘密很方便，但它不是很安全。最好为每个目的使用不同的秘密。

- **定期轮换秘密。**秘密应该定期轮换以减少它们被泄露的风险。一个好的经验法则是每 90 天轮换一次秘密。

## 结论

在本文中，我们了解了如何使用 OAuth 和 JWT 在 Kotlin 应用程序中实现安全性。我们还看到了一些这样做的最佳实践。