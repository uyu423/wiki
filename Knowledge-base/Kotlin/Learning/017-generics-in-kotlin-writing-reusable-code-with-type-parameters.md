---
title: 017: Kotlin의 제네릭: 유형 매개변수로 재사용 가능한 코드 작성
description: 
published: true
date: 2023-02-02T02:57:44.936Z
tags: 
editor: markdown
dateCreated: 2023-02-02T02:57:43.260Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [017: Generics in Kotlin: Writing Reusable Code with Type Parameters***English** document is available*](/en/Knowledge-base/Kotlin/Learning/017-generics-in-kotlin-writing-reusable-code-with-type-parameters)
{.links-list}


# Kotlin의 제네릭: 유형 매개변수로 재사용 가능한 코드 작성

Kotlin의 유형 시스템은 적은 코드로 더 많은 작업을 수행할 수 있도록 설계되었습니다. 이를 수행하는 방법 중 하나는 일반적이거나 다양한 유형에서 재사용 가능한 코드를 작성할 수 있도록 하는 것입니다. 이 게시물에서는 제네릭이 Kotlin에서 작동하는 방식과 제네릭을 사용하여 보다 간결하고 표현력이 풍부한 코드를 작성하는 방법을 살펴보겠습니다.

## 제네릭이란 무엇입니까?

제네릭은 여러 유형으로 작업할 수 있는 코드를 작성할 수 있도록 하는 많은 프로그래밍 언어의 기능입니다. 이것은 `Int` 또는 `String`과 같은 한 가지 유형에 특정한 코드와 반대입니다.

제네릭의 가장 일반적인 예 중 하나는 `List` 유형입니다. `목록`은 모든 유형의 요소를 포함할 수 있으므로 _generic_이라고 합니다. Kotlin에서는 다음과 같이 `Int`의 `List`를 만들 수 있습니다.

```kotlin
val list: List<Int> = listOf(1, 2, 3)
```

`String`의 `List`를 만들 수도 있습니다.

```kotlin
val list: List<String> = listOf("a", "b", "c")
```

보시다시피, 이 두 `List` 사이에서 변경되는 유일한 것은 포함된 요소의 유형입니다. `List` 유형 자체는 일반적입니다.

## 제네릭을 사용하는 이유

제네릭은 여러 유형에 사용할 수 있는 코드를 작성할 수 있도록 해주기 때문에 유용합니다. 이것은 당신의 코드를 더 간결하고 표현력있게 만들 수 있습니다.

예를 들어 `List`의 요소를 출력하는 다음 코드를 고려하십시오.

```kotlin
fun printList(list: List<Any>) {
    for (element in list) {
        println(element)
    }
}
```

이 코드는 요소의 유형에 관계없이 모든 `목록`에서 작동합니다. 이를 사용하여 `Int`의 `List`를 출력할 수 있습니다.

```kotlin
val list: List<Int> = listOf(1, 2, 3)
printList(list)
```

그리고 그것을 사용하여 `String`의 `List`를 출력할 수 있습니다:

```kotlin
val list: List<String> = listOf("a", "b", "c")
printList(list)
```

제네릭을 사용하지 않았다면 `Int`의 `List`용 함수와 `String`의 `List`용 함수를 작성해야 합니다. 제네릭을 사용하면 여러 유형과 함께 사용할 수 있는 하나의 함수를 작성할 수 있습니다.

## 제네릭은 어떻게 작동합니까?

Kotlin의 제네릭은 _type 매개변수_를 사용하여 구현됩니다. 유형 매개변수는 특정 유형에 대한 자리 표시자입니다. 제네릭 형식을 만들 때 하나 이상의 형식 매개 변수를 지정합니다. 예를 들어 `List` 유형에는 `T`라는 유형 매개변수가 있습니다.

제네릭 형식의 인스턴스를 만들 때 형식 매개 변수를 대체해야 하는 형식을 지정합니다. 예를 들어 `List<Int>`를 생성할 때 유형 매개변수 `T`를 `Int` 유형으로 대체하도록 지정합니다.

## 유형 매개변수 사용

유형 매개변수는 여러 가지 방법으로 사용할 수 있습니다. 가장 일반적인 방법은 컬렉션의 요소 유형을 지정하는 것입니다. 예를 들어 `List` 유형에는 `List`에 있는 요소의 유형을 지정하는 유형 매개변수가 있습니다.

우리는 이미 `List`의 요소 유형을 지정하기 위해 유형 매개변수를 사용하는 방법을 살펴보았습니다. 유형 매개변수를 사용하여 `Map`에서 키와 값의 유형을 지정할 수도 있습니다.

```kotlin
val map: Map<String, Int> = mapOf("a" to 1, "b" to 2, "c" to 3)
```

이 예제에서는 `Map`의 키 유형이 `String`이어야 하고 값의 유형이 `Int`여야 한다고 지정했습니다.

유형 매개변수는 `Nullable` 유형의 값 유형을 지정하는 데에도 사용할 수 있습니다.

```kotlin
val nullable: String? = null
```

이 예에서는 `Nullable` 유형의 값 유형이 `String`이어야 한다고 지정했습니다.

## 타입 매개변수 선언하기

제네릭 형식을 만들 때 하나 이상의 형식 매개 변수를 지정합니다. 예를 들어 `List` 유형에는 `T`라는 유형 매개변수가 있습니다.

`typeparam` 키워드를 사용하여 유형 매개변수를 선언할 수 있습니다. 예를 들어 다음과 같이 `T`라는 유형 매개변수를 사용하여 `MyType`이라는 제네릭 유형을 만들 수 있습니다.

```kotlin
typealias MyType<T> = T
```

## 경계

경우에 따라 유형 매개변수로 사용할 수 있는 유형을 제한할 수 있습니다. 예를 들어 유형 매개변수가 `Any`의 하위 유형이어야 한다고 지정할 수 있습니다. Kotlin은 이것을 _upper bound_라고 부릅니다.

`where` 키워드를 사용하여 상한을 지정할 수 있습니다. 예를 들어, 다음과 같이 `Any`의 상한이 있는 `T`라는 유형 매개변수를 사용하여 `MyType`이라는 제네릭 유형을 만들 수 있습니다.

```kotlin
typealias MyType<T> where T : Any
```

이 예에서는 유형 매개변수 `T`가 `Any`의 하위 유형이어야 한다고 지정했습니다. 이것은 `Int`, `String`, `List` 등을 포함하여 모든 유형을 유형 매개변수 `T`로 사용할 수 있음을 의미합니다.

`where` 키워드를 사용하여 하한을 지정할 수도 있습니다. 예를 들어, 다음과 같이 하한값이 `Any`인 `T`라는 유형 매개변수를 사용하여 `MyType`이라는 제네릭 유형을 만들 수 있습니다.

```kotlin
typealias MyType<T> where T : Any
```

이 예에서는 유형 매개변수 `T`가 `Any`의 상위 유형이어야 한다고 지정했습니다. 즉 `Any`, `Any?` 등을 포함하여 모든 유형을 유형 매개변수 `T`로 사용할 수 있습니다.

## 와일드카드

유형을 지정하지 않고 유형 매개변수를 사용하려는 경우가 있습니다. 예를 들어 모든 `목록`의 요소를 인쇄할 수 있는 함수를 만들고 싶을 수 있습니다.

Kotlin에서는 _wildcard_를 사용하여 유형 매개변수가 모든 유형이 될 수 있음을 지정할 수 있습니다. 예를 들어 다음과 같이 `List`의 요소를 출력하는 함수를 만들 수 있습니다.

```kotlin
fun printList(list: List<*>) {
    for (element in list) {
        println(element)
    }
}
```

이 예에서는 유형 매개변수 `T`가 모든 유형이 될 수 있음을 지정하기 위해 와일드카드를 사용했습니다. 이는 요소의 유형에 관계없이 모든 `List`와 함께 `printList` 함수를 사용할 수 있음을 의미합니다.

## 결론

이 게시물에서는 Kotlin에서 제네릭이 작동하는 방식을 살펴보았습니다. 유형 매개변수를 사용하여 보다 간결하고 표현력이 풍부한 코드를 작성하는 방법을 살펴보았습니다. 또한 유형 매개변수를 선언하는 방법과 범위 및 와일드카드를 사용하는 방법도 살펴보았습니다.