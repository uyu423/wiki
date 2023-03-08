---
title: 016: Kotlin의 예외 처리: 예외 발생 및 포착
description: 
published: true
date: 2023-02-05T10:17:20.838Z
tags: 
editor: markdown
dateCreated: 2023-02-05T10:17:19.261Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [016: Exception Handling in Kotlin: Throwing and Catching Exceptions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/016-exception-handling-in-kotlin-throwing-and-catching-exceptions)
{.links-list}


# Kotlin의 예외 처리: 예외 던지기 및 잡기

예외는 정상적인 명령 흐름을 방해하는 프로그램 실행 중에 발생하는 이벤트입니다. 예외가 발생하면 예외 유형 및 오류 발생 시 프로그램 상태와 같은 오류에 대한 정보가 포함된 예외 개체를 만듭니다.

예외는 다음을 포함하되 이에 국한되지 않는 여러 가지로 인해 발생할 수 있습니다.

- 코드의 버그
- 잘못된 사용자 입력
- 하드웨어 오류

Kotlin에는 선택되지 않은 예외와 확인된 두 가지 유형의 예외가 있습니다. Unchecked 예외는 ```RuntimeException``` 클래스를 확장하는 예외이며, Checked 예외는 ```Exception``` 클래스를 확장하는 예외입니다.

## 예외 던지기

```kotlin
fun average(a: Int, b: Int): Double {
    if (a < 0 || b < 0) {
        throw IllegalArgumentException("Numbers must be positive.")
    }
    return (a + b) / 2.0
}
```코틀린
재미있는 평균(a: Int, b: Int): Double {
    if (a < 0 || b < 0) {
        throw IllegalArgumentException("숫자는 양수여야 합니다.")
    }
    반환 (a + b) / 2.0
}
```kotlin
average(-1, 2) // Throws an IllegalArgumentException
```IllegalArgumentException```을 발생시킵니다. 이제 음수로 ```average``` 함수를 호출하려고 하면 예외가 발생하고 프로그램이 중단됩니다.

```kotlin
fun average(a: Int, b: Int): Double {
    if (a < 0 || b < 0) {
        throw IllegalArgumentException("Numbers must be positive.")
    }
    return (a + b) / 2.0
}

fun main(args: Array<String>) {
    val a = -1
    val b = 2
    try {
        val avg = average(a, b)
        println("The average of $a and $b is $avg")
    } catch (e: IllegalArgumentException) {
        println("Error: ${e.message}")
    }
}
```

## 예외 잡기

```try```/```catch``` 키워드를 사용하여 예외를 잡을 수 있습니다. 이는 오류를 정상적으로 처리하고 프로그램 실행을 계속하는 데 유용합니다. 예를 들어, ```average``` 함수가 던진 예외를 포착하고 사용자에게 오류 메시지를 출력하고 싶다고 가정해 봅시다.

```코틀린
재미있는 평균(a: Int, b: Int): Double {
    if (a < 0 || b < 0) {
        throw IllegalArgumentException("숫자는 양수여야 합니다.")
    }
    반환 (a + b) / 2.0
}

fun main(args: Array<String>) {
    값 a = -1
    값 b = 2
    노력하다 {
        값 평균 = 평균(a, b)
        println("$a와 $b의 평균은 $avg입니다.")
    } 잡기(e: IllegalArgumentException) {
        println("오류: ${e.message}")
    }
}
```

위의 코드에서 ```average``` 함수에 의해 발생한 ```IllegalArgumentException```을 포착합니다. 그런 다음 사용자에게 오류 메시지를 인쇄합니다.

## 추가 정보

- ```try```/```catch``` 키워드를 사용하여 예외를 잡을 수 있습니다.
- ```throw``` 키워드를 사용하여 수동으로 예외를 던질 수 있습니다.
- 확인되지 않은 예외는 ```RuntimeException``` 클래스를 확장하는 예외입니다.
- 확인된 예외는 ```Exception``` 클래스를 확장하는 예외입니다.