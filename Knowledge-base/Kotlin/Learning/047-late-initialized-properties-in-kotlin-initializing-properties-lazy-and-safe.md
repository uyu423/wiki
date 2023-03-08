---
title: 047: Kotlin에서 늦게 초기화된 속성: 지연되고 안전한 속성 초기화
description: 
published: true
date: 2023-02-16T14:32:27.359Z
tags: 
editor: markdown
dateCreated: 2023-02-16T14:32:19.415Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [047: Late-initialized Properties in Kotlin: Initializing Properties Lazy and Safe***English** document is available*](/en/Knowledge-base/Kotlin/Learning/047-late-initialized-properties-in-kotlin-initializing-properties-lazy-and-safe)
{.links-list}


# Kotlin의 늦게 초기화된 속성: 지연되고 안전한 속성 초기화

Kotlin의 늦은 초기화 속성은 속성을 느리고 안전하게 초기화하는 좋은 방법입니다. 이 게시물에서는 늦게 초기화된 속성을 유리하게 사용하는 방법을 살펴보겠습니다.

## 늦게 초기화되는 속성이 무엇인가요?

늦게 초기화된 속성은 개체 생성 중에 초기화되지 않은 속성입니다. 대신 속성에 처음 액세스하는 동안 초기화됩니다. 이는 초기화 비용이 많이 들거나 자주 사용되지 않는 속성에 유용합니다.

## 늦게 초기화된 속성을 사용하는 방법

늦게 초기화된 속성을 사용하려면 먼저 ```lateinit``` 키워드로 선언해야 합니다.

```kotlin
lateinit var property: Type
```

그런 다음 속성에 처음 액세스할 때 속성을 초기화할 수 있습니다.

```kotlin
property = value
```

## 늦게 초기화된 속성의 장점

늦게 초기화된 속성을 사용하면 성능과 안전성이라는 두 가지 주요 이점이 있습니다.

### 성능

늦게 초기화된 속성은 처음 액세스할 때까지 초기화되지 않기 때문에 성능을 향상시킬 수 있습니다. 즉, 자주 사용하지 않는 속성을 초기화하지 않아도 됩니다.

### 안전

늦게 초기화된 속성도 사용하기에 안전합니다. 처음 액세스할 때까지 초기화되지 않기 때문입니다. 즉, 아직 초기화되지 않은 속성을 사용하지 않아도 됩니다.

## 늦게 초기화되는 속성의 단점

늦게 초기화된 속성을 사용하면 가독성과 디버깅이라는 두 가지 주요 단점이 있습니다.

### 가독성

늦게 초기화된 속성은 처음 액세스할 때까지 초기화되지 않기 때문에 읽기가 더 어려울 수 있습니다. 즉, 속성을 사용하기 전에 속성을 초기화하는 데 주의해야 합니다.

### 디버깅

늦게 초기화된 속성은 처음 액세스할 때까지 초기화되지 않기 때문에 디버깅하기 더 어려울 수도 있습니다. 즉, 속성을 사용하기 전에 속성을 초기화하는 데 주의해야 합니다.