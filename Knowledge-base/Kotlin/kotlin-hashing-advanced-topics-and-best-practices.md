---
title: Kotlin 해싱: 고급 주제 및 모범 사례
description: 
published: true
date: 2023-02-04T06:17:27.737Z
tags: 
editor: markdown
dateCreated: 2023-02-04T06:17:26.156Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin Hashing: Advanced Topics and Best Practices***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-hashing-advanced-topics-and-best-practices)
{.links-list}


# Kotlin 해싱: 고급 주제 및 모범 사례

이 문서에서는 컬렉션을 해시하는 방법, 모범 사례, 일반적인 함정을 포함하여 Kotlin의 해싱과 관련된 몇 가지 고급 주제를 살펴봅니다.

## 해싱 컬렉션

Kotlin에서 컬렉션으로 작업할 때 일관되고 반복 가능한 결과를 생성하기 위해 컬렉션을 해시해야 하는 경우가 많습니다. 필요에 따라 몇 가지 다른 방법이 있습니다.

해시 가능해야 하는 항목 목록이 있는 경우 `Any` 클래스에 정의된 `hashCode()` 함수를 사용할 수 있습니다. 이렇게 하면 컬렉션을 포함한 모든 개체에 대해 32비트 정수 해시 코드가 생성됩니다.

```kotlin
val list = listOf(1, 2, 3)
val hashCode = list.hashCode() // produces -1292745640
```

Java의 `Object.hashCode()` 메서드와 호환되는 해시 코드를 생성해야 하는 경우 Kotlin 표준 라이브러리에 정의된 `contentHashCode()` 함수를 사용할 수 있습니다.

```kotlin
val list = listOf(1, 2, 3)
val hashCode = list.contentHashCode() // produces 3
```

이 함수는 Java의 `Objects.hashCode(Object...)` 메서드와 동일하며 Java의 `hashCode()` 메서드와 호환되는 해시 코드를 생성합니다.

Kotlin 표준 라이브러리에 정의된 `hash()` 함수와 호환되는 해시 코드를 생성해야 하는 경우 `contentDeepHashCode()` 함수를 사용할 수 있습니다.

```kotlin
val list = listOf(1, 2, 3)
val hashCode = list.contentDeepHashCode() // produces -1548664399
```

이 함수는 Kotlin의 `hash(vararg objects: Any?)` 함수와 동일하며 Kotlin의 `hashCode()` 함수와 호환되는 해시 코드를 생성합니다.

## 모범 사례

해시로 작업할 때 염두에 두어야 할 몇 가지 모범 사례가 있습니다.

- 좋은 해시 함수 사용: 좋은 해시 함수는 해시 코드의 균일한 분포를 생성하여 공격자가 입력 데이터를 추측하기 어렵게 만듭니다.
- 솔트 사용: 솔트는 해싱 전에 입력 데이터에 추가되는 임의의 문자열입니다. 이로 인해 공격자가 사용 중인 해시 함수를 알고 있더라도 입력 데이터를 추측하기가 더 어려워집니다.
- 강력한 해시 함수 사용: 강력한 해시 함수는 충돌에 강합니다. 즉, 두 개의 서로 다른 입력이 동일한 해시 코드를 생성할 가능성이 매우 낮습니다.
- 보안 해시 함수 사용: 보안 해시 함수는 사전 이미지 공격에 강합니다. 즉, 주어진 해시 코드를 생성하는 입력을 찾기가 매우 어렵습니다.

## 일반적인 함정

해시로 작업할 때 피해야 할 몇 가지 일반적인 함정이 있습니다.

- 약한 해시 함수를 사용하지 마십시오. 약한 해시 함수는 추측하기 쉽고 보안 취약성을 유발할 수 있습니다.
- 모든 입력에 동일한 소금을 사용하지 마십시오. 공격자가 사용되는 소금을 알고 있으면 입력 데이터를 더 쉽게 추측할 수 있습니다.
- 해시와 같은 위치에 소금을 저장하지 마십시오. 공격자가 소금에 대한 액세스 권한을 얻으면 입력 데이터를 더 쉽게 추측할 수 있습니다.