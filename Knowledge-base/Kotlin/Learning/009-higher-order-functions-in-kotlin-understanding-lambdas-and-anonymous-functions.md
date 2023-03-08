---
title: 009: Kotlin의 고차 함수: 람다 및 익명 함수 이해
description: 
published: true
date: 2023-01-31T05:36:06.422Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:36:02.765Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [009: Higher-Order Functions in Kotlin: Understanding Lambdas and Anonymous Functions***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/009-higher-order-functions-in-kotlin-understanding-lambdas-and-anonymous-functions)
{.links-list}


# 009: Kotlin의 고차 함수: 람다 및 익명 함수 이해

컴퓨터 프로그래밍에서 고차 함수는 하나 이상의 함수를 인수(즉, 절차적 매개변수)로 취하고 그 결과로 새로운 함수를 반환하는 함수입니다.

Kotlin에서는 언어의 풍부한 내장 함수 세트와 함수가 일급 시민이라는 사실로 인해 고차 함수가 매우 일반적입니다. 즉, 변수에 저장되고 다른 함수에 인수로 전달될 수 있습니다.

Kotlin에서 가장 일반적으로 사용되는 고차 함수 중 하나는 객체에서 주어진 코드 블록을 실행한 다음 객체 자체를 반환하는 데 사용되는 '적용' 함수입니다. 예를 들어 다음 코드를 고려하십시오.

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

위의 코드에서 `apply` 함수는 `list` 객체에서 주어진 코드 블록(즉, 중괄호 사이의 코드)을 실행한 다음 `list` 객체 자체를 반환하는 데 사용됩니다. 그런 다음 `also` 함수를 사용하여 `list` 개체에 대한 몇 가지 추가 작업을 수행합니다(이 경우 콘솔에 인쇄).

고차 함수에 대해 이해해야 할 핵심 사항 중 하나는 반복되는 코드 패턴을 추상화하는 데 사용할 수 있다는 것입니다. 예를 들어 다음 코드를 고려하십시오.

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

위의 코드에서 `apply` 함수는 `list`에 새 요소를 추가한 다음 `list`를 반환하는 데 사용됩니다. 이 특정 코드 패턴은 매우 일반적이어서 Kotlin은 대신 사용할 수 있는 기본 제공 `+=` 연산자를 제공합니다.

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list += 5
    list += listOf(6, 7, 8)

    println(list)
}
```

`+=` 연산자는 `apply` 함수의 줄임말이며, 이는 다음 코드와 동일함을 의미합니다.

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }

    println(list)
}
```

보시다시피 `+=` 연산자는 요소를 목록(또는 다른 변경 가능한 컬렉션)에 추가하는 일반적인 코드 패턴을 추상화하는 데 사용할 수 있습니다.

또 다른 일반적인 고차 함수는 개체에서 주어진 코드 블록을 실행한 다음 코드 결과를 반환하는 데 사용되는 `let` 함수입니다. 예를 들어 다음 코드를 고려하십시오.

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list.let {
        it.add(5)
        it.addAll(listOf(6, 7, 8))
        it
    }

    println(newList)
}
```

위의 코드에서 `let` 함수는 `list` 개체에서 주어진 코드 블록을 실행한 다음 `list` 개체 자체를 반환하는 데 사용됩니다. `it` 변수는 코드 블록 내부의 `list` 개체를 참조하는 데 사용됩니다.

'apply' 함수와 유사하게 'let' 함수는 반복되는 코드 패턴을 추상화하는 데 사용할 수 있습니다. 예를 들어 다음 코드를 고려하십시오.

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list.let {
        it.add(5)
        it.addAll(listOf(6, 7, 8))
        it
    }

    println(newList)
}
```

위의 코드에서 `let` 함수는 `list`에 새 요소를 추가한 다음 `list`를 반환하는 데 사용됩니다. 이 특정 코드 패턴은 매우 일반적이어서 Kotlin은 대신 사용할 수 있는 기본 제공 `+=` 연산자를 제공합니다.

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list += 5
    val newList = list += listOf(6, 7, 8)

    println(newList)
}
```

`+=` 연산자는 `let` 함수의 속기일 뿐이며, 이는 다음 코드와 동일함을 의미합니다.

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list.let {
        it.add(5)
        it.addAll(listOf(6, 7, 8))
        it
    }

    println(newList)
}
```

보시다시피 `+=` 연산자는 요소를 목록(또는 다른 변경 가능한 컬렉션)에 추가하는 일반적인 코드 패턴을 추상화하는 데 사용할 수 있습니다.

마지막으로 고차 함수는 종종 이름이 없는 익명 함수인 람다와 함께 사용된다는 점을 언급할 가치가 있습니다. 람다는 종종 코드 블록을 고차 함수에 인수로 전달하는 데 사용됩니다. 예를 들어 다음 코드를 고려하십시오.

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        this.add(5)
        this.addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

위의 코드에서 `apply` 함수는 `list` 객체에서 주어진 람다를 실행한 다음 `list` 객체 자체를 반환하는 데 사용됩니다. 그런 다음 `also` 함수를 사용하여 `list` 개체에 대한 몇 가지 추가 작업을 수행합니다(이 경우 콘솔에 인쇄).

보시다시피 람다는 반복되는 코드 패턴을 추상화하는 데 사용할 수 있습니다. 예를 들어 다음 코드를 고려하십시오.

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

위의 코드에서 `apply` 함수는 `list`에 새 요소를 추가한 다음 `list`를 반환하는 데 사용됩니다. 이 특정 코드 패턴은 매우 일반적이어서 Kotlin은 대신 사용할 수 있는 기본 제공 `+=` 연산자를 제공합니다.

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list += 5
    list += listOf(6, 7, 8)

    println(list)
}
```

`+=` 연산자는 `apply` 함수의 줄임말이며, 이는 다음 코드와 동일함을 의미합니다.

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }

    println(list)
}
```

보시다시피 `+=` 연산자는 요소를 목록(또는 다른 변경 가능한 컬렉션)에 추가하는 일반적인 코드 패턴을 추상화하는 데 사용할 수 있습니다.

키 포인트:
- 고차 함수는 하나 이상의 함수를 인수로 취하고 그 결과로 새 함수를 반환하는 함수입니다.
- Kotlin에서는 언어의 풍부한 내장 함수 세트와 함수가 일급 시민이라는 사실 때문에 고차원 함수가 매우 일반적입니다.
- Kotlin에서 가장 일반적으로 사용되는 고차 함수 중 하나는 객체에서 주어진 코드 블록을 실행한 다음 객체 자체를 반환하는 데 사용되는 `apply` 함수입니다.
- 또 다른 일반적인 고차 함수는 개체에서 주어진 코드 블록을 실행한 다음 코드의 결과를 반환하는 데 사용되는 `let` 함수입니다.
- 고차 함수는 종종 이름이 없는 익명 함수인 람다와 함께 사용됩니다.