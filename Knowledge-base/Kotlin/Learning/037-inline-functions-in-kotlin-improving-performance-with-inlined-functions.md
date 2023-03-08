---
title: 037: Kotlin의 인라인 함수: 인라인 함수로 성능 향상
description: 
published: true
date: 2023-02-16T10:32:23.644Z
tags: 
editor: markdown
dateCreated: 2023-02-16T10:32:21.635Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [037: Inline Functions in Kotlin: Improving Performance with Inlined Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/037-inline-functions-in-kotlin-improving-performance-with-inlined-functions)
{.links-list}


## 소개

Kotlin은 JVM(Java Virtual Machine)에서 실행되고 JavaScript 소스 코드로 컴파일될 수 있는 정적으로 유형이 지정된 프로그래밍 언어입니다.

이번 포스팅에서는 코틀린에서 인라인 함수로 성능을 향상시키는 방법에 대해 알아보겠습니다.

## 인라인 함수란?

Kotlin에서 인라인 함수는 호출자의 본문에서 확장되는 함수입니다. 이는 함수가 평소와 같이 호출되는 인라인이 아닌 함수와 다릅니다.

인라인 함수를 사용하면 함수 호출의 오버헤드를 줄여 성능을 향상시킬 수 있습니다. 또한 인라인 함수는 호출자의 변수에 액세스할 수 있으므로 성능도 향상될 수 있습니다.

## 인라인 함수 사용 방법

인라인 함수를 사용하려면 `inline` 키워드로 함수에 주석을 달아야 합니다.

예를 들어 인라인하려는 함수 `foo()`가 있다고 가정해 보겠습니다.

```kotlin
inline fun foo() {
    // do something
}
```

이제 `foo()`를 호출할 때마다 함수 본문이 호출자에서 확장됩니다.

## 인라인 함수를 사용해야 하는 경우

일반적으로 함수를 인라인하면 성능이 향상될 것이라고 확신하는 경우에만 인라인 함수를 사용해야 합니다.

또한 함수가 작고 단순한 경우에만 인라인 함수를 사용해야 합니다. 복잡한 함수를 인라인하면 코드가 부풀어 오르고 실제로 성능이 저하될 수 있기 때문입니다.

마지막으로 함수가 여러 위치에서 호출되지 않을 것이라고 확신하는 경우에만 인라인 함수를 사용해야 합니다. 함수를 인라인하면 함수가 여러 위치에서 호출되는 경우 코드가 중복될 수 있기 때문입니다.

## 결론

이번 포스트에서는 Kotlin의 인라인 함수와 이를 사용하여 성능을 향상시키는 방법에 대해 알아보았습니다. 일반적으로 함수를 인라인하면 성능이 향상될 것이라고 확신하는 경우에만 인라인 함수를 사용해야 합니다. 또한 함수가 작고 단순한 경우에만 인라인 함수를 사용해야 합니다.