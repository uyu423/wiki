---
title: Kotlin 보안: OAuth 및 JWT 구현
description: 
published: true
date: 2023-02-09T01:17:53.554Z
tags: 
editor: markdown
dateCreated: 2023-02-09T01:17:51.920Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin Security: Implementing OAuth and JWT***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-security-implementing-oauth-and-jwt)
{.links-list}


# Kotlin 보안: OAuth 및 JWT 구현

이 기사에서는 OAuth 및 JSON 웹 토큰(JWT)을 사용하여 Kotlin 애플리케이션에서 보안을 구현하는 방법을 살펴보겠습니다. 또한 그렇게 하기 위한 몇 가지 모범 사례를 살펴보겠습니다.

## OAuth란?

OAuth는 타사 애플리케이션이 사용자 자격 증명을 저장하고 관리하지 않고도 리소스에 액세스할 수 있도록 하는 인증을 위한 개방형 표준입니다. 리소스 소유자(즉, 사용자)에게 권한을 위임하여 이를 수행합니다.

OAuth는 일반적으로 사용자가 Facebook 또는 Google과 같은 다른 서비스에서 기존 자격 증명으로 로그인할 수 있도록 웹 애플리케이션에서 사용됩니다. 이를 "타사 인증"이라고 합니다.

## JWT란?

JWT(JSON Web Token)는 당사자 간에 데이터를 JSON 객체로 전송하는 간결하고 독립적인 방식을 정의하는 개방형 표준입니다. 이 데이터는 디지털 서명이 되어 있으므로 확인하고 신뢰할 수 있습니다.

JWT는 사용자에 대한 정보를 안전하게 전송하는 데 사용할 수 있으므로 인증 및 권한 부여 시나리오에서 자주 사용됩니다.

## Kotlin에서 OAuth 구현

Kotlin 애플리케이션에서 OAuth를 구현하는 방법을 살펴보겠습니다. 프로세스를 단순화하기 위해 [ScribeJava](https://github.com/scribejava/scribejava) 라이브러리를 사용할 것입니다.

먼저 ScribeJava 라이브러리를 프로젝트 종속성에 추가해야 합니다.

```kotlin
// build.gradle

repositories {
    mavenCentral()
}

dependencies {
    implementation("com.github.scribejava:scribejava-core:2.5.3")
}
```

다음으로 OAuth 서비스를 나타내는 클래스를 만들어야 합니다. 이 클래스는 OAuth 흐름을 구성하고 OAuth 공급자와의 상호 작용을 처리합니다.

이 예에서는 Facebook OAuth API를 사용합니다.

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

`getUserProfile` 메서드에서 Facebook Graph API를 사용하여 현재 사용자의 프로필을 가져옵니다.

이제 OAuth 서비스 클래스가 있으므로 Kotlin 애플리케이션에서 이를 사용하는 방법을 살펴보겠습니다.

먼저 사용자를 OAuth 공급자의 로그인 페이지로 리디렉션하는 경로를 만들어야 합니다.

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

'login' 경로는 사용자를 Facebook 로그인 페이지로 리디렉션합니다. 사용자가 로그인하면 '콜백' 경로로 다시 리디렉션됩니다.

다음으로 '콜백' 경로를 만들어야 합니다. 이 경로는 OAuth 공급자로부터 액세스 토큰을 가져온 다음 사용자 프로필을 가져오는 일을 담당합니다.

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

## Kotlin에서 JWT 구현

OAuth를 구현하는 방법을 살펴보았으니 이제 Kotlin에서 JWT를 구현하는 방법을 살펴보겠습니다. 프로세스를 단순화하기 위해 [Kotlin-JWT](https://github.com/kittinunf/kotlin-jwt) 라이브러리를 사용할 것입니다.

먼저 Kotlin-JWT 라이브러리를 프로젝트 종속 항목에 추가해야 합니다.

```kotlin
// build.gradle

repositories {
    mavenCentral()
}

dependencies {
    implementation("com.auth0:kotlin-jwt:3.3.0")
}
```

다음으로 JWT 서비스를 나타내는 클래스를 만들어야 합니다. 이 클래스는 JWT 토큰 생성 및 확인을 담당합니다.

이 예에서는 HS256 알고리즘을 사용합니다.

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

`generateToken` 메서드에서 `withClaim` 메서드를 사용하여 토큰에 포함하려는 클레임을 지정합니다.

이제 JWT 서비스 클래스가 있으므로 Kotlin 애플리케이션에서 이를 사용하는 방법을 살펴보겠습니다.

먼저 JWT 토큰을 생성하는 경로를 만들어야 합니다.

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

'generateToken' 경로는 클레임 없이 JWT 토큰을 생성합니다.

다음으로 JWT 토큰을 확인하는 경로를 만들어야 합니다.

```kotlin
// JWTController.kt (continued)

@GetMapping("/verify")
fun verifyToken(@RequestParam("token") token: String): Boolean {
    return jwtService.verifyToken(token)
}
```

'verifyToken' 경로는 JWT 토큰이 유효한지 확인합니다.

## 모범 사례

Kotlin 애플리케이션에서 보안을 구현할 때 염두에 두어야 할 몇 가지 모범 사례가 있습니다.

- **승인이 아닌 인증에 OAuth를 사용합니다.** OAuth는 인증이 아닌 승인에 대한 개방형 표준입니다. 두 가지 목적으로 모두 사용할 수 있지만 인증(예: 리소스 소유자에게 권한 위임)에 사용하고 인증에 JWT와 같은 다른 방법을 사용하는 것이 가장 좋습니다.

- **인증이 아닌 인증에 JWT를 사용하세요.** JWT는 두 가지 용도로 모두 사용할 수 있지만 인증(예: 사용자에 대한 정보 전송)에 사용하고 인증에는 OAuth와 같은 다른 방법을 사용하는 것이 가장 좋습니다.

- **JWT 클레임에 민감한 데이터를 저장하지 마세요.** JWT 클레임은 공개되며 누구나 읽을 수 있습니다. 따라서 사용자 비밀번호와 같은 민감한 데이터를 JWT 클레임에 저장하지 않는 것이 중요합니다.

- **JWT 토큰 서명에 안전한 비밀을 사용합니다.** JWT 토큰 서명에 사용되는 비밀은 기밀로 유지되어야 하며 애플리케이션에 하드 코딩되지 않아야 합니다. 이를 수행하는 좋은 방법은 환경 변수를 사용하는 것입니다.

- **JWT 토큰을 검증할 때 `iss` 클레임을 확인하십시오.** `iss`(발행자) 클레임은 JWT 토큰의 소스를 식별하는 데 사용됩니다. JWT 토큰을 검증할 때 'iss' 클레임이 예상 값과 일치하는지 확인하는 것이 중요합니다.

- **JWT 토큰을 확인할 때 `aud` 클레임을 확인합니다.** `aud`(청중) 클레임은 JWT 토큰의 의도된 수신자를 식별하는 데 사용됩니다. JWT 토큰을 검증할 때 `aud` 클레임이 예상 값과 일치하는지 확인하는 것이 중요합니다.

- **JWT 토큰을 확인할 때 `exp` 클레임을 확인하십시오.** `exp`(만료) 클레임은 JWT 토큰의 만료 날짜를 지정하는 데 사용됩니다. JWT 토큰을 검증할 때 현재 날짜가 만료 날짜 이전인지 확인하는 것이 중요합니다.

- **JWT 토큰을 검증할 때 `nbf` 클레임을 확인하십시오.** `nbf`(이전 아님) 클레임은 처리를 위해 JWT 토큰이 허용되지 않아야 하는 날짜를 지정하는 데 사용됩니다. JWT 토큰의 유효성을 검사할 때 현재 날짜가 이전이 아닌 날짜 이후인지 확인하는 것이 중요합니다.

- **JWT 토큰을 확인할 때 `jti` 클레임을 확인하십시오.** `jti`(JWT ID) 클레임은 JWT 토큰에 대한 고유 식별자를 제공하는 데 사용됩니다. JWT 토큰의 유효성을 검사할 때 `jti` 클레임이 존재하고 그 값이 고유한지 확인하는 것이 중요합니다.

- **기본 인증을 사용하지 마십시오.** 기본 인증은 구현이 간단하지만 그다지 안전하지 않습니다. OAuth 또는 JWT와 같은 보다 안전한 방법을 사용하는 것이 가장 좋습니다.

- **JWT 토큰 서명과 데이터 암호화에 동일한 암호를 사용하지 마십시오.** 동일한 암호를 두 가지 용도로 사용하는 것이 편리하지만 그다지 안전하지는 않습니다. 각각의 목적에 대해 다른 암호를 사용하는 것이 가장 좋습니다.

- **비밀을 정기적으로 교체합니다.** 보안이 손상될 위험을 줄이려면 비밀을 정기적으로 교체해야 합니다. 좋은 경험 법칙은 비밀을 90일마다 교체하는 것입니다.

## 결론

이 기사에서는 OAuth 및 JWT를 사용하여 Kotlin 애플리케이션에서 보안을 구현하는 방법을 살펴보았습니다. 우리는 또한 그렇게 하기 위한 몇 가지 모범 사례를 보았습니다.