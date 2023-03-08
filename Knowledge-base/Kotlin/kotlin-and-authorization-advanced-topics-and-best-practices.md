---
title: Kotlin 및 권한 부여: 고급 주제 및 모범 사례
description: 
published: true
date: 2023-02-18T07:06:38.220Z
tags: 
editor: markdown
dateCreated: 2023-02-18T07:06:36.823Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and Authorization: Advanced Topics and Best Practices***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-authorization-advanced-topics-and-best-practices)
{.links-list}


# Kotlin 및 Authorization: 고급 주제 및 모범 사례

권한 부여는 모든 애플리케이션의 중요한 부분입니다. 이 문서에서는 Kotlin 및 승인에 대한 몇 가지 고급 주제와 모범 사례를 살펴보겠습니다.

## 목차

* [소개](# 소개)
* [역할 및 권한 정의](# defining-roles-and-permissions)
* [권한 컨텍스트 작업](# working-with-the-authorization-context)
* [권한 부여](# enforcing-authorization)
* [결론](# 결론)

## 소개

권한 부여는 사용자가 작업을 수행하거나 리소스에 액세스할 수 있는지 여부를 결정하는 프로세스입니다. 대부분의 애플리케이션에서 권한 부여는 사용자의 역할과 권한을 확인하여 적용됩니다.

이 문서에서는 Kotlin 및 승인에 대한 몇 가지 고급 주제를 살펴보겠습니다. 역할과 권한을 정의하는 방법부터 살펴보겠습니다. 그런 다음 권한 부여 컨텍스트로 작업하는 방법을 살펴보겠습니다. 마지막으로 인증을 적용하는 방법을 살펴보겠습니다.

## 역할 및 권한 정의

권한 설정의 첫 번째 단계 중 하나는 사용자가 가질 수 있는 역할과 권한을 정의하는 것입니다. 이를 수행하는 방법에는 여러 가지가 있지만 한 가지 접근 방식은 열거형을 사용하는 것입니다.

```kotlin
enum class Role {
    USER,
    ADMIN
}

enum class Permission {
    READ,
    WRITE,
    DELETE
}
```

이 예에서는 `USER` 및 `ADMIN`의 두 가지 역할을 정의했습니다. 또한 `READ`, `WRITE` 및 `DELETE`의 세 가지 권한을 정의했습니다.

역할과 권한을 정의한 후에는 사용자에게 할당하는 방법을 결정해야 합니다. 한 가지 접근 방식은 지도를 사용하는 것입니다.

```kotlin
val roles: Map<String, Set<Role>> = mapOf(
    "alice" to setOf(Role.USER),
    "bob" to setOf(Role.USER, Role.ADMIN)
)

val permissions: Map<Role, Set<Permission>> = mapOf(
    Role.USER to setOf(Permission.READ),
    Role.ADMIN to setOf(Permission.READ, Permission.WRITE, Permission.DELETE)
)
```

이 예에서는 `roles` 및 `permissions`라는 두 개의 맵을 정의했습니다. `역할` 맵은 사용자 이름을 역할 집합에 매핑합니다. `permissions` 맵은 역할을 권한 집합에 매핑합니다.

## 인증 컨텍스트 작업

대부분의 애플리케이션에서 권한 부여 컨텍스트는 스레드 로컬 변수입니다. 즉, 각 스레드에는 자체 권한 부여 컨텍스트가 있습니다.

권한 부여 컨텍스트에는 일반적으로 현재 로그인한 사용자에 대한 정보가 포함됩니다. Kotlin에서는 이를 데이터 클래스로 나타낼 수 있습니다.

```kotlin
data class AuthorizationContext(
    val user: String,
    val roles: Set<Role>
)
```

이 예에서 권한 부여 컨텍스트에는 `user` 속성과 `roles` 속성이 포함되어 있습니다. `user` 속성에는 현재 로그인한 사용자의 이름이 포함됩니다. `roles` 속성에는 사용자가 가진 역할 집합이 포함됩니다.

인증 컨텍스트는 `getContext()` 함수를 사용하여 액세스할 수 있습니다.

```kotlin
val context: AuthorizationContext? = getContext()
```

`getContext()` 함수는 `AuthorizationContext?`(즉, nullable `AuthorizationContext`)를 반환합니다. 이는 컨텍스트를 사용할 수 없음을 의미합니다.

컨텍스트를 사용할 수 있는 경우 `withContext()` 함수를 사용하여 특정 컨텍스트로 코드 블록을 실행할 수 있습니다.

```kotlin
withContext(context) {
    // Code that needs the context goes here
}
```

`withContext()` 함수는 `AuthorizationContext`와 코드 블록을 사용합니다. 주어진 컨텍스트로 코드 블록을 실행합니다.

## 승인 시행

이제 역할 및 권한을 설정하는 방법과 권한 부여 컨텍스트로 작업하는 방법을 살펴보았으므로 권한 부여를 적용하는 방법을 살펴보겠습니다.

인증을 시행하는 가장 쉬운 방법은 `require()` 함수를 사용하는 것입니다:

```kotlin
require(context != null) { "No authorization context available." }

require(context.user == "alice") { "Unauthorized user." }

require(context.roles.contains(Role.USER)) { "Unauthorized role." }

require(permissions[Role.USER]!!.contains(Permission.READ)) { "Unauthorized permission." }
```

이 예에서는 `require()` 함수를 사용하여 사용자의 역할과 권한을 확인합니다. 사용자에게 `READ` 권한이 없으면 `IllegalArgumentException`이 발생합니다.

인증을 시행하는 또 다른 방법은 `check()` 함수를 사용하는 것입니다:

```kotlin
check(context != null) { "No authorization context available." }

check(context.user == "alice") { "Unauthorized user." }

check(context.roles.contains(Role.USER)) { "Unauthorized role." }

check(permissions[Role.USER]!!.contains(Permission.READ)) { "Unauthorized permission." }
```

이 예에서는 `check()` 함수를 사용하여 사용자의 역할과 권한을 확인합니다. 사용자에게 `READ` 권한이 없으면 `IllegalStateException`이 발생합니다.

## 결론

이 문서에서는 Kotlin 및 승인에 대한 몇 가지 고급 주제와 모범 사례를 살펴보았습니다. 역할 및 권한을 정의하는 방법, 권한 부여 컨텍스트로 작업하는 방법 및 권한 부여를 시행하는 방법을 살펴보았습니다.

권한 부여는 모든 애플리케이션의 중요한 부분입니다. 이 문서의 팁과 요령을 따르면 응용 프로그램이 안전한지 확인할 수 있습니다.