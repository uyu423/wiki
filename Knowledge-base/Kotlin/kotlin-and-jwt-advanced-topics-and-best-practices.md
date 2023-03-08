---
title: Kotlin 및 JWT: 고급 주제 및 모범 사례
description: 
published: true
date: 2023-02-17T18:14:55.937Z
tags: 
editor: markdown
dateCreated: 2023-01-30T22:18:02.367Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kotlin and JWT: Advanced Topics and Best Practices***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-jwt-advanced-topics-and-best-practices)
{.links-list}



# Kotlin 및 JWT: 고급 주제 및 모범 사례

개발 학습 블로그는 또 다른 포괄적이고 실습 지향적인 기사에 오신 것을 환영합니다. 이번에는 Kotlin과 JWT에 대해 설명하겠습니다. 개발과 관련된 고급 주제와 모범 사례를 다룰 예정이므로 Kotlin 개발자는 자신의 기술을 다음 단계로 끌어올릴 수 있습니다.

항상 그렇듯이 독자들에게 블로그가 다른 언어로도 제공된다는 점을 상기시켜 드리고자 합니다. 이 기사를 독일어로 읽고 싶다면 [여기]()를 클릭하세요. 이 기사를 스페인어로 읽으려면 [여기]()를 클릭하십시오.

## 코틀린이란?

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어이며 JavaScript 소스 코드로 컴파일할 수도 있습니다. Kotlin은 IntelliJ IDEA IDE를 만든 회사인 JetBrains에서 개발했습니다.

Kotlin 프로젝트는 2010년에 시작되었고 첫 번째 안정적인 릴리스는 2016년 2월이었습니다. 그 이후로 Kotlin은 가장 인기 있는 프로그래밍 언어 중 하나가 되었으며 현재 Android 개발의 공식 언어입니다.

## JWT란?

JWT는 공개 표준([RFC 7519](https://www.rfc-editor.org/rfc/rfc7519.txt))으로 당사자 간에 정보를 JSON 객체로 전송하는 간결하고 독립적인 방법을 정의합니다. 이 정보는 디지털 서명되어 있으므로 확인하고 신뢰할 수 있습니다. JWT는 비밀 또는 공개/개인 키 쌍을 사용하여 서명할 수 있습니다.

JWT는 분산 시스템에서 당사자 간의 인증 및 정보 교환에 사용됩니다. 일반적인 시나리오에서 사용자는 타사 서비스로 인증되고 서비스는 사용자가 다른 리소스에 액세스하는 데 사용할 수 있는 JWT를 발급합니다.

## Kotlin을 JWT와 함께 사용하면 어떤 이점이 있나요?

Kotlin을 JWT와 함께 사용하면 많은 이점이 있습니다. 첫째, Kotlin은 매우 간결한 언어이며 JWT 형식도 간결합니다. 따라서 Kotlin에서 JWT 기반 애플리케이션을 쉽게 읽고 쓸 수 있습니다. 둘째, Kotlin은 JWT 클레임 및 페이로드 작업을 쉽게 해주는 다양한 JSON 라이브러리를 훌륭하게 지원합니다. 마지막으로 Kotlin의 유형 시스템 및 null 안전 기능은 JWT로 작업할 때 일반적인 오류를 방지하는 데 도움이 됩니다.

## Kotlin과 JWT를 시작하려면 어떻게 해야 하나요?

이 섹션에서는 Kotlin 및 JWT를 시작하는 방법을 보여줍니다. Kotlin 및 JSON의 기본 사항에 이미 익숙하다고 가정합니다.

### 종속성 설치

코딩을 시작하기 전에 Kotlin 컴파일러와 JSON 라이브러리를 설치해야 합니다. [Kotlin Compiler](https://kotlinlang.org/docs/tutorials/command-line.html) 및 [Jackson](https://github.com/FasterXML/jackson) 라이브러리를 사용할 것입니다.

Kotlin은 Maven 또는 Gradle과 같은 패키지 관리자를 사용하여 설치할 수 있습니다. Jackson의 경우 `build.gradle` 파일에 다음 종속성을 추가해야 합니다.

```groovy
implementation 'com.fasterxml.jackson.core:jackson-databind:2.11.+'
```

### 프로젝트 만들기

이제 모든 종속 항목이 설치되었으므로 새 Kotlin 프로젝트를 만들 수 있습니다. 프로젝트 이름을 'jwt-kotlin'으로 지정합니다.

### JWT 생성

이제 프로젝트가 설정되었으므로 일부 코드 작성을 시작할 수 있습니다. JWT를 생성하는 함수를 작성하는 것으로 시작하겠습니다. `jwk-set-pub` 라이브러리를 사용하여 JWT를 생성합니다.

```kotlin
import com.auth0.jwk.JwkSet
import com.auth0.jwk.Jwk

fun generateJwt(jwkSet: JwkSet, keyId: String): String {
    // Get the JWK for the given key ID
    val jwk: Jwk = jwkSet.getKey(keyId)

    // Create a JWT with the JWK
    val jwt = JWT(jwk)

    // Set the claims
    jwt.claims
        .setSubject("kotlin-jwt")
        .setIssuer("https://kotlin-jwt.com")
        .setExpiration(Date(Date().time + 5 * 60 * 1000)) // 5 minutes

    // Sign the JWT
    return jwt.sign()
}
```

위의 코드 스니펫에서 먼저 `jwk-set-pub` 라이브러리를 가져왔습니다. 그런 다음 `JwkSet` 및 `keyId`를 입력으로 사용하고 JWT를 포함하는 `String`을 반환하는 함수를 만들었습니다. 다음으로 `JwkSet`에서 지정된 `keyId`에 대한 JWK를 검색했습니다.

그런 다음 `JWK`를 사용하여 새 `JWT` 개체를 만들었습니다. 그런 다음 'JWT'에 대한 클레임을 설정합니다. 이 예에서는 `subject`, `issuer` 및 `expiration` 클레임을 설정합니다. 마지막으로 `sign()` 메서드로 `JWT`에 서명하고 서명된 `JWT`를 반환했습니다.

### JWT 확인

이제 JWT를 생성하는 방법을 알았으므로 JWT를 확인하는 함수를 작성해 보겠습니다. `jwk-set-pub` 라이브러리를 사용하여 JWT를 확인합니다.

```kotlin
import com.auth0.jwk.JwkSet
import com.auth0.jwk.Jwk

fun verifyJwt(jwkSet: JwkSet, jwt: String): Boolean {
    // Get the header from the JWT
    val header: Map<String, Any> = JWT.getHeader(jwt)

    // Get the kid from the header
    val kid: String? = header["kid"] as String?

    // Get the JWK for the given kid
    val jwk: Jwk = jwkSet.getKey(kid)

    // Verify the JWT
    return JWT.verify(jwt, jwk)
}
```

위의 코드 스니펫에서 먼저 `jwk-set-pub` 라이브러리를 가져왔습니다. 그런 다음 `JwkSet` 및 `jwt`를 입력으로 사용하고 `jwt`가 유효한지 나타내는 `Boolean`을 반환하는 함수를 만들었습니다.

다음으로 `getHeader()` 메서드를 사용하여 `jwt`에서 헤더를 검색했습니다. 그런 다음 헤더에서 'kid'를 검색했습니다. 그런 다음 `JwkSet`에서 주어진 `kid`에 대한 `JWK`를 검색했습니다. 마지막으로 `verify()` 메서드로 `jwt`를 확인하고 결과를 반환했습니다.

## 고급 주제

이 섹션에서는 Kotlin 및 JWT와 관련된 몇 가지 고급 주제에 대해 설명합니다.

### JWT 인코딩 및 디코딩

이전 섹션에서는 JWT를 생성하고 확인하는 방법을 살펴보았습니다. 이 섹션에서는 JWT를 인코딩하고 디코딩하는 방법을 살펴봅니다. 이를 위해 `jwt-kotlin` 라이브러리를 사용할 것입니다.

`jwt-kotlin` 라이브러리는 JWT 인코딩을 위한 `JWT.encode()` 메서드와 JWT 디코딩을 위한 `JWT.decode()` 메서드를 제공합니다.

`JWT.encode()` 메서드는 `JWT` 개체와 `Encoder` 개체를 입력으로 사용하고 `JWT`를 `String`으로 인코딩합니다. Encoder 개체는 사용할 인코딩 알고리즘을 정의합니다. `jwt-kotlin` 라이브러리는 이를 위해 `Base64Encoder` 클래스를 제공합니다.

`JWT.decode()` 메서드는 JWT 및 `Decoder` 개체를 포함하는 `String`을 입력으로 사용하고 `JWT`를 `JWT` 개체로 디코딩합니다. `Decoder` 개체는 사용할 디코딩 알고리즘을 정의합니다. `jwt-kotlin` 라이브러리는 이를 위해 `Base64Decoder` 클래스를 제공합니다.

### 웹 애플리케이션에서 JWT 사용

이 섹션에서는 웹 애플리케이션에서 JWT를 사용하는 방법을 살펴봅니다. 이를 위해 `jwt-kotlin` 및 `jwt-kotlin-web` 라이브러리를 사용할 것입니다.

`jwt-kotlin-web` 라이브러리는 `JwtCookie` 및 `JwtSession` 클래스를 제공하여 웹 애플리케이션에서 JWT로 쉽게 작업할 수 있도록 합니다.

'JwtCookie' 클래스는 쿠키에 저장된 JWT를 나타냅니다. `JwtCookie` 클래스는 쿠키에서 JWT를 가져오고 설정하기 위한 `get()` 및 `set()` 메소드를 제공합니다.

'JwtSession' 클래스는 세션에 저장된 JWT를 나타냅니다. `JwtSession` 클래스는 세션에서 JWT를 가져오고 설정하기 위한 `get()` 및 `set()` 메서드를 제공합니다.

## 모범 사례

이 섹션에서는 Kotlin 및 JWT 사용에 대한 몇 가지 모범 사례에 대해 설명합니다.

### JWT 라이브러리 사용

Kotlin에서 JWT로 작업할 때는 `jwt-kotlin`과 같은 라이브러리를 사용하는 것이 가장 좋습니다. `jwt-kotlin` 라이브러리는 JWT 작업에 유용한 여러 함수와 클래스를 제공합니다.

### JWT 비밀을 안전하게 유지

JWT로 작업할 때 비밀을 안전하게 유지하는 것이 중요합니다. 비밀은 일반 텍스트나 소스 코드에 저장하면 안 됩니다. 구성 파일이나 데이터베이스와 같은 안전한 위치에 저장해야 합니다.

### JWT 재사용 금지

JWT는 재사용하면 안 됩니다. JWT를 사용한 후에는 무효화하고 새 JWT를 생성해야 합니다.

### JWT 블랙리스트 사용

JWT로 작업할 때 무효화된 JWT의 블랙리스트를 유지 관리하는 것이 좋습니다. 이렇게 하면 재생 공격을 방지하는 데 도움이 됩니다.

## 결론

이 기사에서는 Kotlin과 JWT에 대해 설명했습니다. 개발과 관련된 고급 주제와 모범 사례를 다루었으므로 Kotlin 개발자는 자신의 기술을 다음 단계로 끌어올릴 수 있습니다.