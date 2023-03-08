---
title: Kotlin 및 Bcrypt: 단순 해싱에 대한 더 나은 대안
description: 
published: true
date: 2023-02-18T08:06:20.640Z
tags: 
editor: markdown
dateCreated: 2023-02-18T08:06:19.222Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and Bcrypt: A Better Alternative to Simple Hashing***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-bcrypt-a-better-alternative-to-simple-hashing)
{.links-list}


# Kotlin 및 Bcrypt: 단순 해싱에 대한 더 나은 대안

최근 Kotlin 1.3이 출시되면서 널리 사용되는 JVM 언어가 그 어느 때보다 널리 채택되었습니다. 많은 기능과 함께 Kotlin은 null 안전, 데이터 클래스 및 유형 추론을 제공합니다.

Kotlin의 가장 중요한 기능 중 하나는 Java와의 상호 운용성입니다. 이는 Kotlin을 백엔드 및 프런트엔드 개발 모두에 사용할 수 있음을 의미합니다. 이 기사에서는 백엔드 개발에 중점을 두고 안전한 암호 해싱을 위해 Kotlin 및 Bcrypt를 사용하는 방법을 살펴봅니다.

## 암호 해싱이란 무엇입니까?

암호 해싱은 암호를 수학적 알고리즘에서 생성된 문자열인 해시로 변환하는 프로세스입니다. 그런 다음 해시는 데이터베이스에 저장되며 사용자가 로그인을 시도하면 입력한 암호가 해시되어 데이터베이스의 해시와 비교됩니다. 두 해시가 일치하면 사용자에게 액세스 권한이 부여됩니다.

단순 암호화에 비해 암호 해싱의 주요 이점은 원래 암호를 얻기 위해 해싱 프로세스를 되돌릴 수 없다는 것입니다. 즉, 데이터베이스가 손상되고 해시가 유출되더라도 암호 자체는 안전하게 유지됩니다.

## Bcrypt가 단순 해싱보다 나은 이유는 무엇입니까?

Bcrypt는 보안을 위해 설계된 암호 해싱 알고리즘입니다. 무차별 대입 공격에 저항하도록 설계되었기 때문에 MD5 및 SHA-1과 같은 단순한 해싱 알고리즘보다 더 안전합니다.

Bcrypt는 임의의 문자열인 소금을 생성한 다음 해시할 암호와 결합하여 작동합니다. 솔트는 시도하는 각 암호에 대해 새 솔트를 생성해야 하므로 공격자가 해시를 무차별 대입하는 것을 더 어렵게 만듭니다.

## Kotlin 및 Bcrypt 사용 방법

Kotlin을 사용하면 암호 해싱에 Bcrypt를 쉽게 사용할 수 있습니다. kotlin.crypto 라이브러리의 내장 함수를 사용하여 솔트를 생성하고 암호를 해시할 수 있습니다.

먼저 소금을 생성해야 합니다. 우리는 이것을 generateSalt() 함수로 할 수 있습니다.

```kotlin
val salt = generateSalt()
```

다음으로 haspw() 함수를 사용하여 암호를 해시할 수 있습니다. 암호, 솔트 및 사용할 라운드 수를 지정해야 합니다. 라운드 수는 해싱 프로세스에 소요되는 시간을 결정하는 정수입니다. 더 많은 라운드를 사용할수록 해시가 더 안전해지지만 생성하는 데 더 오래 걸립니다.

```kotlin
val hash = hashpw(password, salt, 10)
```

암호를 확인하기 위해 checkpw() 함수를 사용할 수 있습니다. 이 함수는 확인할 암호, 솔트 및 해시를 사용하고 암호가 올바른지 여부를 나타내는 부울 값을 반환합니다.

```kotlin
val isValid = checkpw(password, salt, hash)
```

## Kotlin 및 Bcrypt: 단순 해싱에 대한 더 나은 대안

Kotlin은 null 안전, 데이터 클래스 및 유형 추론을 비롯한 많은 기능을 제공하는 강력한 JVM 언어입니다. Kotlin은 또한 Java와 상호 운용이 가능하므로 백엔드 개발에 적합합니다.

이 기사에서는 안전한 암호 해싱을 위해 Kotlin 및 Bcrypt를 사용하는 방법을 살펴보았습니다. Bcrypt는 보안을 위해 설계된 암호 해싱 알고리즘이며 단순한 해싱 알고리즘보다 무차별 대입 공격에 더 강합니다.

Kotlin을 사용하면 kotlin.crypto 라이브러리의 내장 함수와 함께 Bcrypt를 쉽게 사용할 수 있습니다. 이러한 함수를 사용하여 솔트를 생성하고 암호를 해시하고 암호를 확인할 수 있습니다.

암호를 해시하는 안전한 방법을 찾고 있다면 Kotlin과 Bcrypt가 탁월한 선택입니다.