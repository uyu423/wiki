---
title: 034: Kotlin의 vararg 함수: 가변 개수의 인수를 허용하는 함수 만들기
description: 
published: true
date: 2023-02-13T18:55:41.925Z
tags: 
editor: markdown
dateCreated: 2023-02-13T18:55:40.241Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [034: vararg Functions in Kotlin: Creating Functions that Accept a Variable Number of Arguments***English** document is available*](/en/Knowledge-base/Kotlin/Learning/034-vararg-functions-in-kotlin-creating-functions-that-accept-a-variable-number-of-arguments)
{.links-list}


# Kotlin의 vararg 함수: 가변 개수의 인수를 허용하는 함수 만들기

Kotlin의 vararg 키워드를 사용하면 가변 개수의 인수를 허용하는 함수를 만들 수 있습니다. 이는 함수 정의에서 인수의 수를 명시적으로 지정하지 않고도 임의의 수의 인수를 취할 수 있는 함수를 작성하려는 경우에 유용할 수 있습니다.

이 게시물에서는 Kotlin에서 vararg 함수를 생성하는 방법과 이를 코드에서 사용하는 방법을 알아봅니다. 또한 vararg 함수를 사용하여 코드를 단순화하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

## Vararg 함수 생성

Kotlin에서 vararg 함수를 생성하려면 함수 정의에서 매개변수 이름 앞에 vararg 키워드를 사용합니다. 예를 들어 가변 개수의 문자열을 받아 출력하는 함수를 만들고 싶다고 가정해 보겠습니다. 다음 함수 정의를 사용하여 이를 수행할 수 있습니다.

```kotlin
fun printStrings(vararg strings: String) {
    for (string in strings) {
        println(string)
    }
}
```

strings 매개변수 앞에 vararg 키워드를 배치했습니다. 이것은 Kotlin에게 함수가 임의 개수의 문자열 인수를 취할 수 있음을 알려줍니다.

우리는 이 함수를 임의 개수의 문자열 인수로 호출할 수 있으며 모두 출력됩니다.

```kotlin
printStrings("Hello", "World") // Prints "Hello" and "World"
printStrings("Kotlin", "is", "awesome") // Prints "Kotlin", "is", and "awesome"
```

인수 없이 함수를 호출할 수도 있습니다. 이 경우 아무 것도 인쇄되지 않습니다.

```kotlin
printStrings() // Prints nothing
```

## Vararg 매개변수에 접근하기

vararg 함수를 만들 때 다른 매개변수와 마찬가지로 함수 본문의 vararg 매개변수에 액세스할 수 있습니다. 위의 printStrings() 함수에서 for 루프의 문자열 매개변수에 액세스하여 모든 문자열을 출력했습니다.

함수 본문 외부에서 vararg 매개 변수에 액세스할 수도 있습니다. 이를 위해 함수를 호출할 때 매개변수 이름 앞에 * 연산자를 사용합니다. 예를 들어 가변 개수의 정수를 받아 출력하는 vararg 함수가 있다고 가정해 보겠습니다.

```kotlin
fun printInts(vararg ints: Int) {
    for (int in ints) {
        println(int)
    }
}
```

우리는 이 함수를 정수 인수로 얼마든지 호출할 수 있으며 모두 출력될 것입니다:

```kotlin
printInts(1, 2, 3) // Prints 1, 2, and 3
printInts(4, 5, 6, 7, 8) // Prints 4, 5, 6, 7, and 8
```

인수 없이 함수를 호출할 수도 있습니다. 이 경우 아무 것도 인쇄되지 않습니다.

```kotlin
printInts() // Prints nothing
```

이제 정수 배열이 있고 printInts() 함수를 사용하여 모두 출력하고 싶다고 가정해 보겠습니다. * 연산자를 사용하여 배열을 개별 인수로 "풀기"하면 됩니다.

```kotlin
val intArray = intArrayOf(1, 2, 3)
printInts(*intArray) // Prints 1, 2, and 3
```

## Vararg 및 Non-Vararg 매개변수

vararg 및 non-vararg 매개 변수를 모두 포함하는 vararg 함수를 만들 수도 있습니다. 예를 들어 가변 개수의 문자열과 정수를 받아 정수와 동일한 횟수만큼 문자열을 출력하는 함수를 만들고 싶다고 가정해 보겠습니다.

```kotlin
fun printStringsNTimes(n: Int, vararg strings: String) {
    for (i in 1..n) {
        for (string in strings) {
            println(string)
        }
    }
}
```

이 함수에는 가변 인수가 아닌 매개변수(n)와 가변 인수 매개변수(문자열)가 있습니다. 우리는 이 함수를 임의 개수의 문자열 인수로 호출할 수 있으며 모두 n번 출력됩니다.

```kotlin
printStringsNTimes(3, "Hello", "World") // Prints "Hello" and "World" three times
printStringsNTimes(5, "Kotlin", "is", "awesome") // Prints "Kotlin", "is", and "awesome" five times
```

문자열 인수 없이 함수를 호출할 수도 있습니다. 이 경우 아무 것도 인쇄되지 않습니다.

```kotlin
printStringsNTimes(3) // Prints nothing
```

## 결론

이 게시물에서는 Kotlin에서 vararg 함수를 만드는 방법과 이를 코드에서 사용하는 방법을 배웠습니다. 또한 vararg 함수를 사용하여 코드를 단순화하는 방법에 대한 몇 가지 예를 살펴보았습니다.

Kotlin에 대해 자세히 알아보려면 Kotlin 설명서를 확인하세요.