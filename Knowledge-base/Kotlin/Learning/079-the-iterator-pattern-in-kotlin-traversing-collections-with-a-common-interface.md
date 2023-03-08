---
title: 079: Kotlin의 반복자 패턴: 공통 인터페이스로 컬렉션 탐색
description: 
published: true
date: 2023-02-14T05:17:36.213Z
tags: 
editor: markdown
dateCreated: 2023-02-14T05:17:29.034Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [079: The Iterator Pattern in Kotlin: Traversing Collections with a Common Interface***English** document is available*](/en/Knowledge-base/Kotlin/Learning/079-the-iterator-pattern-in-kotlin-traversing-collections-with-a-common-interface)
{.links-list}


# Kotlin의 반복자 패턴: 공통 인터페이스로 컬렉션 탐색

반복자 패턴은 반복자가 컨테이너를 순회하고 컨테이너의 요소에 액세스하는 데 사용되는 디자인 패턴입니다. 반복자 패턴은 기본 구현을 노출하지 않고 집계 개체의 요소에 순차적으로 액세스하는 방법을 제공하는 데 사용됩니다.

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어입니다. Kotlin은 간결하고 안전하며 상호 운용이 가능하고 도구 친화적인 언어입니다. Apache 2.0 라이센스에 따른 오픈 소스 프로젝트입니다.

Kotlin 표준 라이브러리는 요소 컬렉션을 반복하는 방법을 정의하는 인터페이스인 표준 반복자 집합을 제공합니다. Kotlin에는 세 가지 표준 반복자가 있습니다.

- 반복자
- ListIterator
- MutableIterator

반복자 패턴은 기본 구현을 노출하지 않고 Kotlin 컬렉션을 순회하는 유용한 방법입니다. 반복자를 사용하면 기본 구현에 대해 걱정할 필요 없이 Kotlin 컬렉션의 요소에 순차적으로 안전하게 액세스할 수 있습니다.

## Kotlin의 반복자

Kotlin에서 반복자는 컬렉션의 요소에 순차적으로 액세스하는 방법을 제공하는 객체입니다. Kotlin의 표준 라이브러리는 요소 컬렉션을 반복하는 방법을 정의하는 인터페이스인 표준 반복자 집합을 제공합니다. Kotlin에는 세 가지 표준 반복자가 있습니다.

- 반복자
- ListIterator
- MutableIterator

반복자에는 `hasNext()` 및 `next()`의 두 가지 메서드가 있습니다. `hasNext()` 메소드는 컬렉션에 `next()` 메서드로 액세스할 수 있는 다른 요소가 있는 경우 true를 반환합니다. `next()` 메서드는 컬렉션의 다음 요소를 반환합니다.

반복자를 사용하여 목록, 집합, 지도를 비롯한 모든 Kotlin 컬렉션을 반복할 수 있습니다. 목록과 함께 반복자를 사용하는 방법을 살펴보겠습니다.


```kotlin
val list = listOf(1, 2, 3, 4, 5)
val iterator = list.iterator()

while (iterator.hasNext()) {
    println(iterator.next())
}
```

위의 예에서는 정수 목록과 목록에 대한 반복자를 만듭니다. 그런 다음 `hasNext()` 메서드를 사용하여 `next()` 메서드로 액세스할 수 있는 목록에 더 많은 요소가 있는지 확인합니다. 더 많은 요소가 있으면 요소를 콘솔에 인쇄합니다.

또한 `forEach()` 메서드를 사용하여 Kotlin 컬렉션을 반복할 수 있습니다. `forEach()` 메서드는 람다를 인수로 사용하고 컬렉션의 각 요소에 대한 람다를 호출합니다.

```kotlin
val list = listOf(1, 2, 3, 4, 5)

list.forEach {
    println(it)
}
```

위의 예에서 정수 목록을 만들고 `forEach()` 메서드를 사용하여 목록을 반복합니다. 각 요소를 콘솔에 출력하는 `forEach()` 메서드에 람다를 전달합니다.

## Kotlin의 MutableIterator

가변 반복자는 기본 컬렉션을 수정하는 데 사용할 수 있는 반복자입니다. Kotlin의 표준 라이브러리는 변경 가능한 요소 컬렉션을 반복하고 수정하는 방법을 정의하는 `MutableIterator` 인터페이스를 제공합니다.

변경 가능한 이터레이터에는 `hasNext()`, `next()` 및 `remove()`의 세 가지 메서드가 있습니다. `hasNext()` 및 `next()` 메서드는 반복자에 대해 수행하는 것과 동일하게 작동합니다. `remove()` 메서드는 기본 컬렉션에서 `next()` 메서드에 의해 반환된 마지막 요소를 제거합니다.

변경 가능한 반복자를 목록과 함께 사용하는 방법을 살펴보겠습니다.

```kotlin
val list = mutableListOf(1, 2, 3, 4, 5)
val iterator = list.iterator()

while (iterator.hasNext()) {
    val element = iterator.next()
    if (element % 2 == 0) {
        iterator.remove()
    }
}

println(list)
```

위의 예에서 변경 가능한 정수 목록과 목록에 대한 변경 가능한 반복자를 만듭니다. 그런 다음 `hasNext()` 메서드를 사용하여 `next()` 메서드로 액세스할 수 있는 목록에 더 많은 요소가 있는지 확인합니다. 더 많은 요소가 있으면 목록에서 요소를 가져와서 2로 나눌 수 있는지 확인합니다. 그렇다면 `remove()` 메서드를 사용하여 목록에서 제거합니다.

또한 `forEach()` 메서드를 사용하여 Kotlin 컬렉션을 반복하고 수정할 수 있습니다. `forEach()` 메서드는 람다를 인수로 사용하고 컬렉션의 각 요소에 대한 람다를 호출합니다. 람다에는 요소와 요소의 인덱스라는 두 가지 인수가 있습니다.

```kotlin
val list = mutableListOf(1, 2, 3, 4, 5)

list.forEach { element, index ->
    if (element % 2 == 0) {
        list.removeAt(index)
    }
}

println(list)
```

위의 예에서 변경 가능한 정수 목록을 만들고 `forEach()` 메서드를 사용하여 목록을 반복합니다. 요소와 요소의 인덱스라는 두 개의 인수를 사용하는 `forEach()` 메서드에 람다를 전달합니다. 요소가 2로 나누어지면 `removeAt()` 메서드를 사용하여 목록에서 제거합니다.

## 결론

이 글에서는 Iterator 패턴과 Kotlin에서 Iterator를 사용하는 방법에 대해 알아보았습니다. 또한 변경 가능한 반복자와 이를 사용하여 기본 컬렉션을 수정하는 방법에 대해서도 배웠습니다.