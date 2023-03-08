---
title: 045: Kotlin의 로컬 함수: 함수 내에 함수 만들기
description: 
published: true
date: 2023-02-02T01:43:44.725Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:43:43.188Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [045: Local Functions in Kotlin: Creating Functions Within Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/045-local-functions-in-kotlin-creating-functions-within-functions)
{.links-list}


# Kotlin의 로컬 함수: 함수 내에서 함수 만들기

Kotlin으로 코드를 작성할 때 다른 함수 안에 함수를 만들고 싶은 경우가 종종 있습니다. 이것을 **로컬 함수**라고 합니다. 로컬 함수는 외부 함수의 변수에 액세스할 수 있으므로 유용합니다. 즉, 복잡한 코드를 단순화하는 데 사용할 수 있습니다.

이 게시물에서는 Kotlin에서 로컬 함수를 만드는 방법을 살펴보겠습니다. 또한 로컬 함수를 사용할 때의 몇 가지 이점에 대해서도 설명합니다.

## 로컬 함수 정의

로컬 함수는 다른 함수의 본문 내에서 정의됩니다. 예를 들면 다음과 같습니다.

```kotlin
fun outerFunction() {
    fun localFunction() {
        // Code goes here
    }
}
```

보시다시피 로컬 함수는 외부 함수의 본문 내부에 정의되어 있습니다. 로컬 함수는 외부 함수 내에서만 호출할 수 있다는 점에 유의해야 합니다. 이는 로컬 함수에 **로컬 범위**가 있음을 의미합니다.

로컬 함수가 외부 함수의 변수에 액세스할 수 있다는 점도 주목할 가치가 있습니다. 이는 로컬 함수가 외부 함수 내에 **중첩**되기 때문입니다. 예를 들면 다음과 같습니다.

```kotlin
fun outerFunction() {
    val outerVariable = " outer"

    fun localFunction() {
        println(outerVariable) // Prints " outer"
    }
}
```

보시다시피 로컬 함수는 외부 함수에 정의된 `outerVariable` 변수에 액세스할 수 있습니다.

## 로컬 함수 호출

로컬 함수는 정의된 함수 내에서만 호출할 수 있습니다. 이는 **로컬 범위**가 있음을 의미합니다. 예를 들면 다음과 같습니다.

```kotlin
fun outerFunction() {
    fun localFunction() {
        // Code goes here
    }

    localFunction() // Calls the local function
}
```

보시다시피 로컬 함수는 외부 함수 내에서 호출됩니다. 외부 함수 외부에서 로컬 함수를 호출하려고 하면 오류가 발생합니다.

```kotlin
fun outerFunction() {
    fun localFunction() {
        // Code goes here
    }
}

localFunction() // Error: localFunction is not defined
```

## 로컬 기능의 이점

로컬 함수는 외부 함수의 변수에 액세스할 수 있기 때문에 유용합니다. 이는 복잡한 코드를 단순화하는 데 사용할 수 있음을 의미합니다.

예를 들어 숫자의 계승을 계산하는 함수가 있다고 가정해 보겠습니다. 숫자의 계승은 숫자보다 작거나 같은 모든 양의 정수의 곱입니다. 예를 들어 5의 계승은 5 * 4 * 3 * 2 * 1이므로 120입니다.

다음은 Kotlin에서 숫자의 계승을 계산하는 함수를 작성하는 방법입니다.

```kotlin
fun factorial(n: Int): Int {
    if (n == 0) {
        return 1
    }

    return n * factorial(n - 1)
}
```

이 함수는 자신을 호출하는 함수를 작성하는 기술인 **재귀**를 사용합니다.

이 함수의 문제점은 **꼬리 재귀가 아님**입니다. 이것은 함수가 결과를 반환하기 전에 자신을 여러 번 호출한다는 것을 의미합니다. 이로 인해 **스택 오버플로** 오류가 발생할 수 있으며, 이는 함수가 자신을 너무 많이 호출하여 스택이 오버플로될 때 발생합니다.

로컬 함수를 사용하여 이 문제를 해결할 수 있습니다.

```kotlin
fun factorial(n: Int): Int {
    tailrec fun factorial(acc: Int, n: Int): Int {
        if (n == 0) {
            return acc
        }

        return factorial(acc * n, n - 1)
    }

    return factorial(1, n)
}
```

이 함수는 **꼬리 재귀**입니다. 즉, 함수가 결과를 반환하기 전에 자신을 한 번만 호출합니다. 이는 스택 오버플로 오류가 발생하지 않고 'n'의 큰 값으로 함수를 호출할 수 있음을 의미합니다.

## 결론

이 게시물에서는 Kotlin에서 로컬 함수를 만드는 방법을 살펴보았습니다. 또한 로컬 함수 사용의 이점에 대해서도 논의했습니다.

로컬 함수는 외부 함수의 변수에 액세스할 수 있기 때문에 유용합니다. 이는 복잡한 코드를 단순화하는 데 사용할 수 있음을 의미합니다.

로컬 함수에 대해 자세히 알아보려면 다음 리소스를 읽어보는 것이 좋습니다.

- [로컬 함수](https://kotlinlang.org/docs/reference/local-functions.html)에 대한 Kotlin 설명서
- [재귀 및 꼬리 재귀 in Kotlin](https://blog.kotlin-academy.com/recursion-and-tail-recursion-in-kotlin-f79bc55a326a)에 대한 블로그 게시물
- [로컬 함수의 이점](https://blog.kotlin-academy.com/the-benefits-of-local-functions-f79bc55a326a)에 대한 블로그 게시물