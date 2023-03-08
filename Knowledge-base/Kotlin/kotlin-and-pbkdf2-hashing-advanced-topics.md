---
title: Kotlin 및 PBKDF2 해싱: 고급 주제
description: 
published: true
date: 2023-02-04T22:17:21.171Z
tags: 
editor: markdown
dateCreated: 2023-02-04T22:17:19.550Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and PBKDF2 Hashing: Advanced Topics***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-pbkdf2-hashing-advanced-topics)
{.links-list}


# Kotlin 및 PBKDF2 해싱: 고급 주제

이 기사에서는 Kotlin 및 PBKDF2 해싱에 대해 더 자세히 설명합니다. PBKDF2가 무엇인지, 어떻게 작동하는지, Kotlin에서 어떻게 사용하는지 등의 주제를 다룰 것입니다. 또한 이러한 개념을 설명하기 위해 몇 가지 코드 예제를 제공합니다.

## PBKDF2란?

PBKDF2(Password-Based Key Derivation Function 2)는 RSA Laboratories PKCS(Public-Key Cryptography Standards) 시리즈의 일부인 키 파생 함수입니다. 2000년에 PKCS # 5 v2.0으로 출판되었습니다.

PBKDF2는 암호에서 키를 추출하는 안전한 방법입니다. 암호, 솔트 및 반복 횟수를 입력으로 사용합니다. 그런 다음 SHA-256과 같은 해싱 함수를 통해 암호를 여러 번 실행합니다. 반복 횟수는 구성 가능하며 계산 비용이 더 많이 들고 따라서 더 안전하게 만들기 위해 늘릴 수 있습니다.

PBKDF2의 출력은 암호화 또는 기타 용도의 키로 사용할 수 있는 바이트 배열입니다.

## PBKDF2는 어떻게 작동하나요?

PBKDF2의 기본 아이디어는 해싱 기능을 통해 암호를 여러 번 실행하는 것입니다. 따라서 컴퓨팅 비용이 더 많이 들고 따라서 더 안전합니다.

 PBKDF2는 https://tools.ietf.org/html/rfc2898에서 찾을 수 있는 RFC 2898에 정의되어 있습니다.

알고리즘은 다음과 같습니다.

```
PBKDF2(P, S, c, dkLen)

Input:

P: The password, as a byte array.

S: A salt, as a byte array.

c: The number of iterations to perform.

dkLen: The length of the derived key, in bytes.

Output:

A derived key, as a byte array.

1. Initialize a byte array D with the dkLen bytes set to 0.

2. Set U0 = PRF(P, S || 0x00), where PRF is a pseudorandom function.

3. For i = 1, 2, ..., c:

   Set Ui = PRF(P, Ui-1).

   Set D = D || Ui.

4. Return D.
```

## Kotlin에서 PBKDF2를 사용하는 방법

Kotlin에는 PBKDF2용 내장 라이브러리가 없지만 사용할 수 있는 여러 타사 라이브러리가 있습니다. 이 예에서는 https://github.com/ajalt/kotlin-pbkdf2에서 찾을 수 있는 "KotlinPBKDF2" 라이브러리를 사용합니다.

이 라이브러리를 사용하려면 build.gradle 파일에 다음 종속성을 추가하세요.

```
compile 'com.github.ajalt:kotlin-pbkdf2:1.0.0'
```

그러면 다음과 같이 PBKDF2 기능을 사용할 수 있습니다.

```kotlin
val password = "password"
val salt = "salt"
val iterations = 1000
val keyLength = 32

val derivedKey = PBKDF2(password, salt, iterations, keyLength)
```

## 결론

이 기사에서는 Kotlin 및 PBKDF2 해싱에 대해 더 깊이 논의했습니다. PBKDF2가 무엇인지, 어떻게 작동하는지, Kotlin에서 사용하는 방법과 같은 주제를 다루었습니다. 또한 이러한 개념을 설명하기 위해 몇 가지 코드 예제를 제공했습니다.