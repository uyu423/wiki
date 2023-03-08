---
title: Kotlin 및 JWT: RESTful API 보안
description: 
published: true
date: 2023-02-13T15:17:46.729Z
tags: 
editor: markdown
dateCreated: 2023-02-13T15:17:44.938Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and JWT: Securing RESTful APIs***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-jwt-securing-restful-apis)
{.links-list}


# Kotlin 및 JWT: RESTful API 보안

Kotlin이 Android 앱 개발을 위한 일류 언어로 떠오르면서 점점 더 많은 개발자가 서버 측 개발에도 Kotlin을 사용하는 데 관심을 갖는 것은 놀라운 일이 아닙니다. 이 기사에서는 Kotlin 및 JWT(Java Web Tokens) 프레임워크를 사용하여 RESTful API를 보호하는 방법을 살펴보겠습니다.

JWT는 서버가 클라이언트의 신원을 확인할 수 있도록 액세스 토큰을 생성하기 위한 표준입니다. 이것은 클라이언트가 모바일 앱에서 브라우저 확장에 이르기까지 무엇이든 될 수 있는 RESTful API에서 특히 중요합니다. JWT를 사용하면 인증된 클라이언트만 API에 액세스할 수 있습니다.

Kotlin에서 JWT를 사용하려면 kotlin-jwt 라이브러리를 설치해야 합니다. 이 라이브러리는 JWT 토큰을 만들고 확인하기 위한 일련의 기능을 제공합니다.

kotlin-jwt 라이브러리가 설치되면 이를 사용하여 다음과 같이 JWT 토큰을 생성할 수 있습니다.

```kotlin
val jwt = JWT.create()
    .withSubject("user@example.com")
    .withExpiresAt(Date())
    .sign(algorithm)
```

여기서 'algorithm'은 사용할 서명 알고리즘을 지정하는 'Algorithm'의 인스턴스입니다. 예를 들어 `HMAC256` 알고리즘을 다음과 같이 사용할 수 있습니다.

```kotlin
val algorithm = Algorithm.HMAC256("secret")
```

그런 다음 `jwt` 변수를 사용하여 토큰을 생성할 수 있습니다.

```kotlin
val token = jwt.generate()
```

이제 토큰이 있으므로 이를 사용하여 API를 보호할 수 있습니다. 예를 들어 HTTP 요청의 `Authorization` 헤더에 추가할 수 있습니다.

```kotlin
val request = Request.Builder()
    .url("https://example.com/api/v1/users")
    .header("Authorization", "Bearer $token")
    .build()
```

그런 다음 서버는 `verify` 기능을 사용하여 토큰을 확인할 수 있습니다.

```kotlin
val jwt = JWT.require(algorithm)
    .build()

val verifiedToken = jwt.verify(token)
```

토큰이 유효하면 'verifiedToken' 변수에 디코딩된 토큰이 포함됩니다. 그런 다음 `getSubject` 함수를 사용하여 사용자의 이메일 주소를 얻을 수 있습니다.

```kotlin
val userEmail = verifiedToken.getSubject()
```

이제 Kotlin 및 JWT를 사용하여 RESTful API를 보호하는 방법을 알았으므로 더 읽을 수 있는 몇 가지 리소스를 살펴보겠습니다.

## 자원

- [JSON 웹 토큰](https://jwt.io/)
- [kotlin-jwt](https://github.com/kotlinc-es/kotlin-jwt)
- [코틀린 보안](https://kotlinlang.org/docs/reference/security.html)