---
title: 033: Kotlin의 기본 및 명명된 인수: 기본값 및 명명된 매개변수 제공
description: 
published: true
date: 2023-02-01T12:04:38.270Z
tags: 
editor: markdown
dateCreated: 2023-02-01T12:04:36.825Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [033: Default and Named Arguments in Kotlin: Providing Default Values and Named Parameters***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/033-default-and-named-arguments-in-kotlin-providing-default-values-and-named-parameters)
{.links-list}



# 033: Kotlin의 기본 및 명명된 인수: 기본값 및 명명된 매개변수 제공

기본 및 명명된 인수에 대한 Kotlin의 지원을 통해 함수 매개변수에 합리적인 기본값을 쉽게 제공하고 기본값과 다른 인수만 지정할 수 있습니다.

## 기본 인수

날짜와 시간으로 문자열 형식을 지정하는 함수를 고려하십시오.

```kotlin
fun formatDateTime(
    date: String,
    time: String,
    dateFormat: String = "yyyy-MM-dd",
    timeFormat: String = "HH:mm:ss"
): String {
    return "$date $time"
}
```

이 함수에는 네 개의 매개변수가 있으며 그 중 두 개는 기본값이 있습니다. 함수를 호출할 때 처음 두 매개변수에 대한 값을 제공할 수 있으며 기본값은 뒤의 두 매개변수에 사용됩니다.

```kotlin
formatDateTime("2019-01-01", "12:00:00") // "2019-01-01 12:00:00"
```

네 가지 매개변수 모두에 대한 값을 제공할 수도 있습니다.

```kotlin
formatDateTime(
    date = "2019-01-01",
    time = "12:00:00",
    dateFormat = "dd/MM/yy",
    timeFormat = "hh:mm a"
) // "01/01/19 12:00 PM"
```

## 명명된 인수

여러 매개변수가 있는 함수를 호출할 때 매개변수의 순서가 중요합니다. 이로 인해 특히 일부 매개 변수에 기본값이 있는 경우 코드를 읽기 어려울 수 있습니다.

명명된 인수에 대한 Kotlin의 지원을 통해 값과 함께 매개변수 이름을 지정할 수 있으므로 코드를 더 쉽게 읽을 수 있습니다.

```kotlin
fun formatDateTime(
    date: String,
    time: String,
    dateFormat: String = "yyyy-MM-dd",
    timeFormat: String = "HH:mm:ss"
): String {
    return "$date $time"
}
 
formatDateTime(
    time = "12:00:00",
    date = "2019-01-01",
    timeFormat = "hh:mm a",
    dateFormat = "dd/MM/yy"
) // "01/01/19 12:00 PM"
```

위의 예에서는 값과 함께 매개변수 이름을 지정했습니다. 이렇게 하면 특히 일부 매개 변수에 기본값이 있는 경우 코드를 더 쉽게 읽을 수 있습니다.

## 기본값과 다른 인수만 지정

여러 매개변수로 함수를 호출할 때 기본값과 다른 인수만 지정할 수 있습니다. 예를 들어 다음 기능을 고려하십시오.

```kotlin
fun formatDateTime(
    date: String,
    time: String,
    dateFormat: String = "yyyy-MM-dd",
    timeFormat: String = "HH:mm:ss"
): String {
    return "$date $time"
}
```

이 함수에는 네 개의 매개변수가 있으며 그 중 두 개는 기본값이 있습니다. 두 개의 인수를 사용하여 이 함수를 호출할 수 있으며 나머지 매개변수에는 기본값이 사용됩니다.

```kotlin
formatDateTime("2019-01-01", "12:00:00") // "2019-01-01 12:00:00"
```

기본값과 다른 인수만 지정할 수도 있습니다.

```kotlin
formatDateTime(
    date = "2019-01-01",
    time = "12:00:00",
    timeFormat = "hh:mm a"
) // "2019-01-01 12:00:00"
```

위의 예에서 `date` 및 `time` 매개변수에 대한 값을 지정했으며 `dateFormat` 매개변수에는 기본값이 사용됩니다.

## 결론

기본 및 명명된 인수에 대한 Kotlin의 지원을 통해 함수 매개변수에 합리적인 기본값을 쉽게 제공하고 기본값과 다른 인수만 지정할 수 있습니다. 이렇게 하면 코드를 더 쉽게 읽고 이해할 수 있습니다.