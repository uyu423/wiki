---
title: Kotlin 및 해싱: 암호 및 민감한 데이터 보호
description: 
published: true
date: 2023-02-06T14:17:39.236Z
tags: 
editor: markdown
dateCreated: 2023-02-06T14:17:33.592Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and Hashing: Securing Passwords and Sensitive Data***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-hashing-securing-passwords-and-sensitive-data)
{.links-list}


# Kotlin 및 해싱: 암호 및 민감한 데이터 보호

Kotlin이 Android 개발용 언어로 부상함에 따라 애플리케이션에서 비밀번호와 민감한 데이터를 적절하게 보호하는 방법을 아는 것이 중요합니다. 이 기사에서는 해싱을 사용하여 이 정보를 보호하는 방법에 대해 설명합니다.

## 해싱이란?

해싱은 임의의 크기의 데이터를 고정된 크기의 데이터에 매핑하는 프로세스입니다. 고정 크기 데이터는 해시 값, 해시 코드, 해시 다이제스트 또는 간단히 해시라고 합니다. 해시 값은 데이터 바이트 합산과 같은 간단한 알고리즘이거나 SHA-256과 같은 보다 복잡한 알고리즘일 수 있는 해싱 알고리즘을 사용하여 생성됩니다.

## 해싱을 사용하는 이유

해싱은 단방향 프로세스이므로 원본 데이터를 다시 가져오기 위해 프로세스를 되돌릴 수 없습니다. 이는 누군가가 해시 값을 확보하더라도 원본 데이터가 무엇인지 확인할 수 없기 때문에 보안상 중요합니다.

## Kotlin에서 해싱을 사용하는 방법

Kotlin은 `hashCode()`라는 내장 해싱 함수를 제공합니다. 이 함수는 임의의 객체를 받아서 `Int` 해시 값을 반환합니다. 예를 들어 다음과 같이 `String`을 해시할 수 있습니다.

```kotlin
val hashValue = "password".hashCode()
```

`hashCode()` 함수는 다른 데이터에 대해 동일한 해시 값을 생성할 수 있기 때문에 암호화 목적에 적합하지 않습니다. 예를 들어 문자열 "password"와 "PASSWORD"는 동일한 해시 값을 가집니다.

암호화 해시 값을 생성해야 하는 경우 JCE(Java Cryptography Extension) 라이브러리의 `MessageDigest` 클래스를 사용할 수 있습니다. Kotlin은 다음과 같이 사용하기 쉽게 하는 `digest()`라는 `MessageDigest`용 확장 함수를 제공합니다.

```kotlin
import java.security.MessageDigest

fun MessageDigest.digest(data: ByteArray): ByteArray {
    update(data)
    return digest()
}
```

이 함수를 사용하여 다음과 같이 SHA-256 해시를 계산할 수 있습니다.

```kotlin
val data = "password".toByteArray()
val sha256 = MessageDigest.getInstance("SHA-256")
val hashValue = sha256.digest(data)
```

## 해시 저장 방법

공격자가 원래 데이터가 무엇인지 확인할 수 없도록 안전한 방식으로 해시를 저장하는 것이 중요합니다. 이를 수행하는 한 가지 방법은 데이터가 해시되기 전에 데이터에 추가되는 임의의 문자열인 솔트를 사용하는 것입니다. 솔트는 해시 값과 함께 저장되며, 주어진 비밀번호가 맞는지 확인할 때 사용됩니다.

`MessageDigest` 클래스에는 해싱되기 전에 데이터에 솔트를 추가하는 데 사용할 수 있는 `update(salt: ByteArray)` 함수가 있습니다. 예를 들어:

```kotlin
val data = "password".toByteArray()
val salt = "somesalt".toByteArray()

val sha256 = MessageDigest.getInstance("SHA-256")
sha256.update(salt)
val hashValue = sha256.digest(data)
```

## 비밀번호가 맞는지 확인하는 방법

주어진 암호가 올바른지 확인하려면 암호의 해시를 계산하고 저장된 해시 값과 비교해야 합니다. 일치하면 암호가 올바른 것입니다.

이를 수행하는 한 가지 방법은 `MessageDigest` 클래스를 다시 사용하는 것입니다. 다음과 같이 암호의 해시를 계산할 수 있습니다.

```kotlin
val password = "password"
val hashValue = "hashValue".toByteArray()

val sha256 = MessageDigest.getInstance("SHA-256")
sha256.update(hashValue)
val passwordHash = sha256.digest(password.toByteArray())
```

그런 다음 `passwordHash`를 저장된 해시 값과 비교하여 일치하는지 확인할 수 있습니다.

이를 수행하는 또 다른 방법은 `hashCode()` 함수를 사용하는 것입니다. 다음과 같이 암호의 해시를 계산할 수 있습니다.

```kotlin
val password = "password"
val hashValue = "hashValue".toByteArray()

val passwordHash = password.hashCode()
```

그런 다음 `passwordHash`를 저장된 해시 값과 비교하여 일치하는지 확인할 수 있습니다.

## 결론

이 기사에서는 해싱을 사용하여 Kotlin 애플리케이션에서 비밀번호와 민감한 데이터를 보호하는 방법에 대해 설명했습니다. `hashCode()` 및 `MessageDigest` 함수를 사용하여 해시를 계산하는 방법과 솔트를 사용하여 해시를 저장하고 확인하는 방법을 살펴보았습니다.