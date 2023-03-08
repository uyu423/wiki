---
title: 011: Kotlin의 속성 및 필드: Getter 및 Setter 이해
description: 
published: true
date: 2023-01-31T05:36:58.404Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:36:54.297Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [011: Properties and Fields in Kotlin: Understanding Getters and Setters***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/011-properties-and-fields-in-kotlin-understanding-getters-and-setters)
{.links-list}


# Kotlin의 속성 및 필드: Getter 및 Setter 이해

Kotlin에서 속성 및 필드는 사용자 지정 getter 및 setter를 가질 수 있습니다. 기본적으로 속성과 필드는 공용 가시성을 가지며 이는 클래스 외부에서 액세스할 수 있음을 의미합니다.

## 속성

속성은 `val` 키워드를 사용하여 선언됩니다. 변경할 수 없습니다. 즉, 한 번만 할당할 수 있습니다.

```kotlin
val name = "John"
```

위의 예에서 `name` 속성은 값 "John"으로 초기화됩니다. 재지정할 수 없습니다.

## 필드

필드는 `var` 키워드를 사용하여 선언됩니다. 변경 가능하므로 재할당할 수 있습니다.

```kotlin
var name = "John"
name = "Jane"
```

위의 예에서 `name` 필드는 값 "John"으로 초기화됩니다. "Jane"에게 재할당할 수 있습니다.

## 게터와 세터

기본적으로 속성과 필드는 공용 가시성을 가지며 이는 클래스 외부에서 액세스할 수 있음을 의미합니다. 그러나 사용자 지정 getter 및 setter를 만들어 액세스 방법을 제어할 수 있습니다.

Getter는 속성 또는 필드의 값을 검색하는 데 사용됩니다. 코드에서 속성이나 필드를 사용할 때 호출됩니다.

Setter는 속성 또는 필드의 값을 재할당하는 데 사용됩니다. 코드에서 속성 또는 필드를 재할당할 때 호출됩니다.

다음 속성을 고려하십시오.

```kotlin
var name: String = "John"
```

다음과 같이 이 속성에 대한 사용자 지정 getter 및 setter를 만들 수 있습니다.

```kotlin
var name: String = "John"
    get() {
        return field
    }
    set(value) {
        field = value
    }
```

위의 예에서 `get()` 함수는 getter이고 `set(value)` 함수는 setter입니다. `get()` 함수는 `name` 필드의 값을 반환하고 `set(value)` 함수는 `name` 필드의 값을 설정합니다.

`val` 키워드로 선언된 속성 및 필드에 대한 사용자 지정 getter 및 setter를 만들 수도 있습니다. 이 경우 사용자 지정 getter만 만들 수 있습니다. 속성이 변경할 수 없기 때문에 사용자 지정 setter를 만들 수 없습니다.

다음 속성을 고려하십시오.

```kotlin
val name: String = "John"
```

다음과 같이 이 속성에 대한 사용자 지정 getter를 만들 수 있습니다.

```kotlin
val name: String = "John"
    get() {
        return field
    }
```

위의 예에서 `get()` 함수는 getter입니다. `get()` 함수는 `name` 필드의 값을 반환합니다.

## 결론

Kotlin에서 속성 및 필드는 사용자 지정 getter 및 setter를 가질 수 있습니다. Getter는 속성 또는 필드의 값을 검색하는 데 사용되며 setter는 속성 또는 필드의 값을 재할당하는 데 사용됩니다.