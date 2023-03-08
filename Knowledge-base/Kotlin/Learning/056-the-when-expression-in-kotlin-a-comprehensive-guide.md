---
title: 056: Kotlin의 When 표현식: 종합 안내서
description: 
published: true
date: 2023-02-16T19:17:31.509Z
tags: 
editor: markdown
dateCreated: 2023-02-16T19:17:30.007Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [056: The When Expression in Kotlin: A Comprehensive Guide***English** document is available*](/en/Knowledge-base/Kotlin/Learning/056-the-when-expression-in-kotlin-a-comprehensive-guide)
{.links-list}


## 소개

Kotlin의 when 표현식은 다양한 유형의 데이터를 일치시키는 데 사용할 수 있는 강력한 도구입니다. 이 가이드에서는 Kotlin에서 when 표현식을 사용하는 방법을 살펴보고 몇 가지 고급 기능을 살펴보겠습니다.

## 기본 사용법

when 표현식은 다른 언어의 switch 문에 해당하는 Kotlin의 표현입니다. 이를 통해 값을 일치시키고 해당 값을 기반으로 코드 블록을 실행할 수 있습니다.

다음은 간단한 예입니다.

```kotlin
when (x) {
    1 -> println("x is 1")
    2 -> println("x is 2")
    else -> println("x is neither 1 nor 2")
}
```

이 예에서는 변수 `x`의 값을 일치시킵니다. `x`가 `1`과 같으면 해당 사례와 관련된 코드 블록이 실행됩니다. 마찬가지로 'x'가 '2'와 같으면 해당 사례와 관련된 코드 블록이 실행됩니다. `x`가 `1`도 `2`도 아닌 경우 `else` 사례와 관련된 코드 블록이 실행됩니다.

'else' 케이스가 필요하지 않다는 점에 유의하는 것이 중요합니다. 'else' 케이스를 생략하면 when 표현식은 다른 케이스에 명시적으로 나열되지 않은 값과 일치하지 않습니다.

```kotlin
when (x) {
    1 -> println("x is 1")
    2 -> println("x is 2")
}
```

이 예에서 `x`가 `1`도 `2`도 아닌 경우 `else` 사례와 연결된 코드 블록이 실행되지 않습니다.

## 유형 일치

값을 일치시키는 것 외에도 when 표현식을 사용하여 유형을 일치시킬 수도 있습니다. 이는 nullable 형식으로 작업할 때 특히 유용합니다.

다음 예를 고려하십시오.

```kotlin
fun process(value: Any) {
    when (value) {
        is String -> println(value.length)
        is Int -> println(value * 2)
        else -> println("I don't know what this is")
    }
}
```

이 예제에는 `Any` 유형을 사용하여 어떤 방식으로든 처리하는 함수가 있습니다. `value` 매개변수의 유형을 일치시키기 위해 when 표현식을 사용합니다.

`value`가 `String`이면 길이를 출력합니다. `value`가 `Int`이면 값에 2를 곱한 값을 출력합니다. `value`가 `String`도 `Int`도 아니면 무엇인지 모른다는 메시지를 출력합니다. .

when 식을 사용하여 nullable 형식을 일치시킬 수도 있습니다. 이것은 두려운 `NullPointerException`을 피하는 데 유용합니다.

다음 예를 고려하십시오.

```kotlin
fun process(value: Any?) {
    when (value) {
        is String -> println(value.length)
        is Int -> println(value * 2)
        null -> println("value is null")
        else -> println("I don't know what this is")
    }
}
```

이 예에서는 `value` 매개변수의 유형을 `Any`에서 `Any?`로 변경했습니다. 이렇게 하면 매개변수가 null을 허용하므로 이제 'null' 값을 사용할 수 있습니다.

`null` 값을 처리하기 위해 when 표현식에 사례를 추가했습니다. `value`가 `null`이면 이를 알리는 메시지를 출력합니다.

`null` 케이스는 `else` 케이스 앞에 와야 한다는 점에 유의하는 것이 중요합니다. 이는 `else` 케이스가 `null`을 포함한 모든 값과 일치하기 때문입니다.

`null` 케이스가 `else` 케이스 뒤에 있으면 절대 실행되지 않습니다.

## 결론

이 가이드에서는 Kotlin에서 when 표현식을 사용하는 방법을 살펴보았습니다. 값과 유형을 일치시키는 방법과 nullable 유형을 처리하는 방법도 살펴보았습니다.