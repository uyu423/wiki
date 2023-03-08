---
title: 031: Kotlin의 범위: 값 범위를 표현하고 반복하기
description: 
published: true
date: 2023-02-10T17:55:15.961Z
tags: 
editor: markdown
dateCreated: 2023-02-10T17:55:14.333Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [031: Ranges in Kotlin: Representing and Iterating Over Ranges of Values***English** document is available*](/en/Knowledge-base/Kotlin/Learning/031-ranges-in-kotlin-representing-and-iterating-over-ranges-of-values)
{.links-list}


# Kotlin의 범위: 값 범위를 표현하고 반복하기

범위는 일련의 값을 나타낼 수 있도록 하는 Kotlin의 기본 개념입니다. 이 게시물에서는 Kotlin에서 범위를 만들고 반복하는 방법을 살펴보겠습니다.

## 범위 만들기

Kotlin에서 범위를 만드는 방법에는 `..` 연산자를 사용하거나 `rangeTo()` 함수를 사용하는 두 가지 방법이 있습니다.

`..` 연산자는 시작 값과 끝 값을 모두 포함하는 범위를 만드는 데 사용됩니다. 예를 들어 다음 코드는 1에서 5까지의 범위를 만듭니다.

```kotlin
val range1 = 1..5
```

반면 `rangeTo()` 함수는 끝 값을 제외하는 범위를 만드는 데 사용됩니다. 예를 들어 다음 코드는 1에서 5까지의 범위를 만듭니다.

```kotlin
val range2 = 1.rangeTo(5)
```

이 두 범위는 모두 *포괄적*이며 시작 값과 끝 값을 포함합니다. `..` 또는 `.rangeTo()` 대신 `until` 키워드를 사용하여 *독점* 범위를 만들 수도 있습니다. 예를 들어 다음 코드는 1에서 5까지의 범위를 만듭니다.

```kotlin
val range3 = 1 until 5
```

## 범위 반복

이제 범위를 만드는 방법을 알았으므로 범위를 반복하는 방법을 살펴보겠습니다. for 루프를 사용하여 이 작업을 수행할 수 있습니다.

```kotlin
for (i in 1..5) {
    println(i)
}
```

이 코드는 1에서 5까지의 숫자를 콘솔에 인쇄합니다. 또한 `downTo` 키워드를 사용하여 역방향으로 범위를 반복할 수 있습니다.

```kotlin
for (i in 5 downTo 1) {
    println(i)
}
```

이 코드는 5에서 1까지의 숫자를 콘솔에 인쇄합니다.

## 결론

이 게시물에서는 Kotlin에서 범위를 만들고 반복하는 방법을 살펴보았습니다. 범위는 다양한 상황에서 사용할 수 있는 강력한 도구입니다. 저처럼 유용하게 사용하시길 바랍니다!