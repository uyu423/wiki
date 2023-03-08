---
title: Kotlin의 CoroutineScope 이해
description: 
published: true
date: 2023-02-14T07:55:19.751Z
tags: 
editor: markdown
dateCreated: 2023-02-14T07:55:17.874Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Understanding the CoroutineScope in Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/understanding-the-coroutinescope-in-kotlin)
{.links-list}


# Kotlin의 CoroutineScope 이해하기

코루틴은 Kotlin의 동시 프로그래밍을 위한 강력한 도구입니다. Kotlin 애플리케이션의 성능을 개선하는 데 사용할 수 있는 가벼운 스레드입니다.

이 기사에서는 CoroutineScope를 살펴보고 애플리케이션에서 코루틴을 관리하는 데 어떻게 사용할 수 있는지 살펴보겠습니다.

## CoroutineScope가 무엇인가요?

CoroutineScope는 코루틴의 수명 주기를 관리하는 데 사용되는 Kotlin 코루틴 라이브러리의 클래스입니다. 범위가 취소될 때 해당 범위에서 시작된 모든 코루틴을 취소하는 방법을 제공합니다.

범위는 coroutineScope 빌더 함수를 사용하여 만들 수 있습니다. 이 빌더 함수는 새 범위를 만들고 현재 범위에 추가합니다.

간단한 예를 살펴보겠습니다.

```kotlin
fun main() {
    // create a new scope
    val scope = coroutineScope {
        // launch a coroutine in the scope
        launch {
            delay(1000L)
            println("World!")
        }
        println("Hello")
    }
}
```

위의 예에서는 coroutineScope 빌더 함수를 사용하여 새 범위를 만듭니다. 그런 다음 범위에서 코루틴을 시작합니다. 코루틴은 1초 동안 지연된 다음 "World!"를 인쇄합니다.

범위에서 코루틴이 시작됩니다. 이는 범위가 취소되면 코루틴이 취소됨을 의미합니다.

## CoroutineScope 취소

 CoroutineScope는 cancel 메서드를 사용하여 취소할 수 있습니다. 이 메서드는 범위에서 시작된 모든 코루틴을 취소합니다. 간단한 예를 살펴보겠습니다.

```kotlin
fun main() {
    // create a new scope
    val scope = coroutineScope {
        // launch a coroutine in the scope
        launch {
            delay(1000L)
            println("World!")
        }
        println("Hello")
    }
    // cancel the scope
    scope.cancel()
}
```

위의 예에서는 새 범위를 만들고 범위에서 코루틴을 시작합니다. 코루틴은 1초 동안 지연된 다음 "World!"를 인쇄합니다.

그런 다음 범위에서 취소 메서드를 호출합니다. 이렇게 하면 범위에서 시작된 모든 코루틴이 취소됩니다. 이 경우 코루틴은 "World!"를 인쇄하지 않습니다. 실행 기회를 갖기 전에 취소되었기 때문입니다.

## 결론

이 기사에서는 CoroutineScope와 애플리케이션에서 코루틴을 관리하는 데 어떻게 사용할 수 있는지 살펴보았습니다. 또한 범위를 취소하는 방법과 이것이 범위에서 시작된 모든 코루틴을 취소하는 방법도 살펴보았습니다.