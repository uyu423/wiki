---
title: Kotlin 및 OAuth 2.0: 인증 및 승인
description: 
published: true
date: 2023-02-18T07:32:39.805Z
tags: 
editor: markdown
dateCreated: 2023-02-18T07:32:31.919Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and OAuth 2.0: Authentication and Authorization***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-oauth-2-0-authentication-and-authorization)
{.links-list}


# Kotlin 및 OAuth 2.0: 인증 및 승인

## 소개

[Kotlin](https://kotlinlang.org/)은 Java Virtual Machine에서 실행되고 JavaScript로 컴파일할 수도 있는 최신 프로그래밍 언어입니다. Kotlin은 Java와 완벽하게 상호 운용되므로 Android 애플리케이션 개발을 위한 매력적인 옵션입니다.

OAuth 2.0은 사용자가 자신의 자격 증명을 공유하지 않고도 애플리케이션이 리소스에 안전하게 액세스할 수 있도록 하는 인증을 위한 개방형 표준입니다. OAuth 2.0은 사용자 인증 및 권한 부여를 위한 다양한 메커니즘을 제공하며 Kotlin을 사용하면 애플리케이션에서 이러한 메커니즘을 쉽게 활용할 수 있습니다.

이 기사에서는 Kotlin과 OAuth 2.0이 함께 작동하여 애플리케이션에서 인증 및 권한 부여를 활성화하는 방법을 살펴보겠습니다. 또한 Kotlin에서 OAuth 2.0으로 쉽게 작업할 수 있게 해주는 일부 라이브러리와 프레임워크를 살펴봅니다.

## 코틀린과 OAuth 2.0

Kotlin을 사용하면 애플리케이션에서 OAuth 2.0을 쉽게 사용할 수 있습니다. [kotlin-oauth](https://github.com/kittinunf/kotlin-oauth) 라이브러리는 OAuth 2.0과 [spring-security-oauth2-kotlin](https:// github.com/spring-projects-experimental/spring-security-oauth2-kotlin) 라이브러리를 사용하면 OAuth 2.0을 [Spring Security](https://spring.io/projects/spring-security) 프레임워크와 쉽게 통합할 수 있습니다.

시작하려면 프로젝트의 종속 항목에 kotlin-oauth 라이브러리를 추가하세요.

```kotlin
dependencies {
    implementation("com.github.kittinunf.kotlin-oauth:kotlin-oauth:2.1.0")
}
```

그런 다음 kotlin-oauth 라이브러리를 사용하여 Kotlin 애플리케이션에 OAuth 2.0 지원을 쉽게 추가할 수 있습니다. 예를 들어 다음 코드는 kotlin-oauth를 사용하여 GitHub API에서 액세스 토큰을 요청하는 방법을 보여줍니다.

```kotlin
import com.github.kittinunf.kotlin_oauth.oauth2.*

val client = HttpClient()

val request = client.request(
    "https://github.com/login/oauth/access_token",
    GitHubAccessTokenRequest(
        "YOUR_CLIENT_ID",
        "YOUR_CLIENT_SECRET",
        "YOUR_REDIRECT_URI",
        "YOUR_AUTHORIZATION_CODE"
    )
)

val response = request.responseObject<GitHubAccessTokenResponse>()

if (response.isSuccess) {
    val accessToken = response.value.accessToken
    // Use the access token to access the GitHub API
} else {
    // Handle the error
}
```

kotlin-oauth 라이브러리를 사용하면 다른 OAuth 2.0 공급자에 대한 지원을 쉽게 추가할 수도 있습니다. 지원되는 공급자의 전체 목록은 [kotlin-oauth README](https://github.com/kittinunf/kotlin-oauth# supported-providers)를 참조하세요.

## 라이브러리 및 프레임워크

kotlin-oauth 라이브러리 외에도 Kotlin에서 OAuth 2.0을 쉽게 사용할 수 있게 해주는 여러 다른 라이브러리와 프레임워크가 있습니다.

[spring-security-oauth2-kotlin](https://github.com/spring-projects-experimental/spring-security-oauth2-kotlin) 라이브러리는 [Spring Security OAuth 2.0](https:// spring.io/projects/spring-security-oauth2) 프로젝트. 라이브러리를 사용하면 [Spring Security](https://spring.io/projects/spring-security) 프레임워크를 사용하여 Kotlin 애플리케이션에 OAuth 2.0 지원을 쉽게 추가할 수 있습니다.

[pac4j-kotlin](https://github.com/pac4j/pac4j-kotlin) 라이브러리는 [Pac4j](https://www.pac4j.org/) 보안 라이브러리에 대한 Kotlin 지원을 제공합니다. Pac4j는 OAuth 2.0을 비롯한 다양한 인증 메커니즘을 지원하는 Java 보안 라이브러리입니다.

## 결론

이 기사에서는 Kotlin과 OAuth 2.0이 함께 작동하여 애플리케이션에서 인증 및 승인을 활성화하는 방법을 살펴보았습니다. 또한 Kotlin에서 OAuth 2.0으로 쉽게 작업할 수 있게 해주는 일부 라이브러리와 프레임워크를 살펴보았습니다.

Kotlin 및 OAuth 2.0에 대해 자세히 알아보려면 다음 리소스를 확인하세요.

- [kotlin-oauth](https://github.com/kittinunf/kotlin-oauth)
- [spring-security-oauth2-kotlin](https://github.com/spring-projects-experimental/spring-security-oauth2-kotlin)
- [pac4j-kotlin](https://github.com/pac4j/pac4j-kotlin)
- [Kotlin 및 OAuth 2.0](https://developer.okta.com/blog/2017/06/21/kotlin-oauth2)