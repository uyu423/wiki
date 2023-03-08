---
title: 코틀린 해싱: PBKDF2 및 Bcrypt
description: 
published: true
date: 2023-02-18T02:06:22.956Z
tags: 
editor: markdown
dateCreated: 2023-02-18T02:06:21.602Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin Hashing: PBKDF2 and Bcrypt***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-hashing-pbkdf2-and-bcrypt)
{.links-list}


# 코틀린 해싱

Kotlin은 보안 애플리케이션 개발을 위한 많은 기능을 제공하는 강력한 프로그래밍 언어입니다. 가장 중요한 보안 기능 중 하나는 해싱입니다. 해싱은 데이터를 반전하기 어려운 고정 길이 값으로 변환하는 프로세스입니다. 따라서 암호와 같은 민감한 데이터를 저장하고 데이터 무결성을 확인하는 데 이상적입니다.

Kotlin은 PBKDF2 및 bcrypt라는 두 가지 해싱 알고리즘을 제공합니다.

## PBKDF2

PBKDF2는 암호 해싱을 위한 표준 알고리즘입니다. [RFC 2898](https://tools.ietf.org/html/rfc2898)에 지정되어 있습니다. PBKDF2는 의사 난수 함수(PRF)와 솔트를 사용하여 해시를 생성합니다. PRF는 비밀 키와 일부 입력 데이터를 가져와 의사 난수 출력을 생성하는 암호화 기능입니다. PBKDF2는 연산 집약적이어서 무차별 대입 공격에 더 강합니다.

다음 예시는 Kotlin에서 PBKDF2를 사용하여 비밀번호를 해시하는 방법을 보여줍니다.

```kotlin
import java.security.spec.KeySpec
import javax.crypto.SecretKeyFactory
import javax.crypto.spec.PBEKeySpec

fun main(args: Array<String>) {
    // The password to hash
    val password = "secret"

    // The salt
    val salt = byteArrayOf(0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f)

    // The number of iterations
    val iterations = 10000

    // The size of the derived key in bits
    val keySize = 256

    try {
        // Get the instance of the SecretKeyFactory
        val keyFactory = SecretKeyFactory.getInstance("PBKDF2WithHmacSHA1")

        // Generate the key
        val keySpec = PBEKeySpec(password.toCharArray(), salt, iterations, keySize)
        val secretKey = keyFactory.generateSecret(keySpec)

        // Get the key bytes
        val keyBytes = secretKey.encoded

        // Print the key
        println(keyBytes.toHexString())
    } catch (e: Exception) {
        println(e)
    }
}
```

## bcrypt

bcrypt는 암호용으로 설계된 해싱 알고리즘입니다. 복어 암호를 기반으로 하며 소금을 사용하여 해시를 해독하기 더 어렵게 만듭니다. bcrypt는 PBKDF2보다 계산 집약적이어서 무차별 대입 공격에 훨씬 더 강합니다.

다음 예시는 Kotlin에서 bcrypt를 사용하여 비밀번호를 해시하는 방법을 보여줍니다.

```kotlin
import org.mindrot.jbcrypt.BCrypt

fun main(args: Array<String>) {
    // The password to hash
    val password = "secret"

    // The number of rounds
    val rounds = 10

    // The salt
    val salt = BCrypt.gensalt(rounds)

    // The hash
    val hash = BCrypt.hashpw(password, salt)

    // Print the hash
    println(hash)
}
```

## 외부 리소스

- [Kotlin 암호화 함수](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.crypto/-crypto-functions/)
- [코틀린 표준 라이브러리](https://kotlinlang.org/api/latest/jvm/stdlib/)
- [Kotlin PBKDF2WithHmacSHA1](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.security/-p-b-k-d-f-2-with-hmac-s-h-a-1/)
- [코틀린 bcrypt](https://kotlinlang.org/api/latest/jvm/stdlib/org.mindrot/-bcrypt/)
- [Bcrypt on Wikipedia](https://en.wikipedia.org/wiki/Bcrypt)
- [위키백과의 PBKDF2](https://en.wikipedia.org/wiki/PBKDF2)