---
title: 078: Kotlin의 전략 패턴: 알고리즘을 객체로 캡슐화
description: 
published: true
date: 2023-02-14T17:55:28.640Z
tags: 
editor: markdown
dateCreated: 2023-02-14T17:55:26.996Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [078: The Strategy Pattern in Kotlin: Encapsulating Algorithms as Objects***English** document is available*](/en/Knowledge-base/Kotlin/Learning/078-the-strategy-pattern-in-kotlin-encapsulating-algorithms-as-objects)
{.links-list}


# 078: Kotlin의 전략 패턴: 알고리즘을 객체로 캡슐화

## 소개

전략 패턴은 런타임에 알고리즘의 동작을 선택할 수 있도록 하는 동작 소프트웨어 디자인 패턴입니다. 이는 응용 프로그램이 다른 알고리즘을 사용해야 할 때 유용하며 사용자 입력 또는 응용 프로그램의 현재 상태에 따라 런타임에 알고리즘을 선택할 수 있습니다.

전략 패턴은 정책 패턴이라고도 합니다.

## 문제

정수 목록을 정렬하는 간단한 응용 프로그램이 있다고 가정합니다. 다음과 같이 간단한 `정렬` 함수를 작성하여 시작할 수 있습니다.

```kotlin
fun sort(list: List<Int>): List<Int> {
    // implement sorting algorithm here
}
```

이 `정렬` 함수는 정수 목록을 입력으로 받아 오름차순으로 정렬된 새로운 정수 목록을 반환합니다.

이제 응용 프로그램에 다른 정렬 알고리즘을 추가하려고 한다고 가정합니다. 또 다른 `정렬` 함수를 작성할 수 있지만 그렇게 하면 이름은 같지만 동작이 다른 두 함수가 있게 됩니다. 이는 우리 애플리케이션 사용자에게 혼란을 줄 수 있습니다.

대신 전략 패턴을 사용하여 각 정렬 알고리즘을 자체 개체에 캡슐화할 수 있습니다. 그런 다음 정수 목록과 전략 개체를 입력으로 사용하고 전략 개체를 사용하여 목록을 정렬하는 '정렬' 함수를 작성할 수 있습니다.

## 해결책

다음은 전략 패턴을 사용하여 정수 목록을 정렬하는 방법입니다.

```kotlin
// define a sorting strategy interface
interface SortingStrategy {
    fun sort(list: List<Int>): List<Int>
}

// implement a sorting strategy for ascending order
class AscendingSortingStrategy : SortingStrategy {
    override fun sort(list: List<Int>): List<Int> {
        // implement sorting algorithm here
    }
}

// implement a sorting strategy for descending order
class DescendingSortingStrategy : SortingStrategy {
    override fun sort(list: List<Int>): List<Int> {
        // implement sorting algorithm here
    }
}

// use the strategy pattern to sort a list of integers
fun sort(list: List<Int>, strategy: SortingStrategy): List<Int> {
    return strategy.sort(list)
}
```

위의 코드에서 정렬 전략을 나타내는 `SortingStrategy` 인터페이스를 정의했습니다. 또한 'AscendingSortingStrategy' 및 'DescendingSortingStrategy'라는 두 가지 정렬 전략을 구현했습니다.

마지막으로 정수 목록과 정렬 전략을 입력으로 사용하고 정렬 전략을 사용하여 목록을 정렬하는 `sort` 함수를 작성했습니다.

이제 다음과 같이 `정렬` 기능을 사용할 수 있습니다.

```kotlin
// sort a list of integers in ascending order
val ascendingList = sort(list, AscendingSortingStrategy())

// sort a list of integers in descending order
val descendingList = sort(list, DescendingSortingStrategy())
```

## 혜택

전략 패턴에는 다음과 같은 몇 가지 이점이 있습니다.

- 런타임에 알고리즘의 동작을 선택할 수 있습니다.

- 애플리케이션에 새로운 알고리즘을 쉽게 추가할 수 있습니다.

- 알고리즘 테스트가 용이합니다.

- 코드를 더 읽기 쉽고 유지 관리하기 쉽게 만듭니다.

## 함정

전략 패턴을 사용할 때 몇 가지 잠재적인 함정이 있습니다.

- 코드를 더 복잡하게 만들 수 있습니다.

- 코드를 읽고 이해하기 어렵게 만들 수 있습니다.

- 새로운 알고리즘을 변경하거나 추가하기 어렵게 만들 수 있습니다.