---
title: 010: Kotlin의 코루틴: 쉬워진 비동기 프로그래밍
description: 
published: true
date: 2023-01-31T05:27:21.917Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:27:20.300Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [010: Coroutines in Kotlin: Asynchronous Programming Made Easy***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/010-coroutines-in-kotlin-asynchronous-programming-made-easy)
{.links-list}


Kotlin 코루틴을 사용하면 비동기 코드를 순차적으로 작성할 수 있습니다. 즉, 스레딩의 복잡성을 처리할 필요 없이 코드가 동기식으로 실행되는 것처럼 코드를 작성할 수 있습니다.

코루틴은 버전 1.1에서 Kotlin에 추가되었으며 비동기 코드를 작성하는 강력한 방법을 제공합니다. 이 기사에서는 코루틴이 무엇인지, 어떻게 작동하는지, 자신의 코드에서 어떻게 사용하는지 살펴보겠습니다.

## 코루틴이 무엇인가요?

코루틴은 비동기 코드를 순차적으로 작성하는 방법입니다. 즉, 스레딩의 복잡성을 처리할 필요 없이 코드가 동기식으로 실행되는 것처럼 코드를 작성할 수 있습니다.

코루틴은 버전 1.1에서 Kotlin에 추가되었으며 비동기 코드를 작성하는 강력한 방법을 제공합니다. 이 기사에서는 코루틴이 무엇인지, 어떻게 작동하는지, 자신의 코드에서 어떻게 사용하는지 살펴보겠습니다.

## 코루틴은 어떻게 작동하나요?

코루틴은 일시 중단 및 재개할 수 있는 경량 스레드입니다. 이것은 코루틴이 실행 중간에 일시 중지되고 나중에 재개될 수 있음을 의미합니다.

코루틴은 다음과 같이 구성됩니다.

- 코루틴은 부모 코루틴과 함께 생성됩니다.
- 코루틴에는 수명과 다른 코루틴과 상호 작용하는 방식을 결정하는 컨텍스트가 있습니다.
- 코루틴에는 코루틴을 일시 중지하는 데 사용되는 일시 중단 기능이 있습니다.
- 코루틴에는 코루틴을 재개하는 데 사용되는 재개 기능이 있습니다.

코루틴이 생성되면 부모 코루틴이 제공됩니다. 이 상위 코루틴은 하위 코루틴의 실행을 관리합니다. 자식 코루틴은 부모 코루틴이 재개할 때까지 재개할 수 없습니다.

코루틴의 컨텍스트는 수명을 결정합니다. 코루틴을 취소하면 종료될 수 있습니다. 코루틴은 실행을 완료했음을 의미하는 완료될 수도 있습니다.

suspend 함수를 사용하여 코루틴을 일시 중지할 수 있습니다. 이 함수는 일시 중단 함수를 인수로 사용합니다. suspend 함수가 호출되면 코루틴이 일시 중지되고 suspend 함수가 실행됩니다.

재개 기능은 코루틴을 재개하는 데 사용됩니다. 이 함수는 재개 함수를 인수로 사용합니다. 재개 함수가 호출되면 코루틴이 재개되고 재개 함수가 실행됩니다.

## 코루틴 사용법

코루틴을 사용하는 것은 간단합니다. 코드에 다음 줄을 추가하기만 하면 됩니다.

```kotlin
import kotlinx.coroutines.*
```

이 행은 Kotlin에서 코루틴 라이브러리를 가져옵니다.

이제 코드에서 코루틴을 사용할 수 있습니다. 예를 들어 다음 코드는 코루틴을 만든 다음 일시 중지합니다.

```kotlin
import kotlinx.coroutines.*

fun main() {
    val parent = CoroutineScope(Job())

    val child = parent.launch {
        println("Child coroutine")
        delay(1000L)
        println("Child coroutine after delay")
    }

    println("Main coroutine")
    child.suspend()
}
```

이 코드에서는 시작 기능을 사용하여 코루틴을 만듭니다. 이 함수는 새 코루틴을 만들고 이에 대한 참조를 반환합니다. 이 참조를 하위 변수에 저장합니다.

그런 다음 suspend 함수를 사용하여 자식 코루틴을 일시 중지합니다. 이 함수는 일시 중단 함수를 인수로 사용합니다. 이 경우 일시 중지 기능은 지연입니다. 이 함수는 지정된 시간(1000밀리초) 동안 코루틴을 일시 중지합니다.

이 코드를 실행하면 다음과 같은 출력이 표시됩니다.

```
Main coroutine
Child coroutine
```

자식 코루틴은 지연 함수가 호출된 후 일시 중지됩니다. 메인 코루틴은 계속 실행되고 "메인 코루틴"을 출력합니다.

재개 기능을 사용하여 자식 코루틴을 재개할 수 있습니다.

```kotlin
import kotlinx.coroutines.*

fun main() {
    val parent = CoroutineScope(Job())

    val child = parent.launch {
        println("Child coroutine")
        delay(1000L)
        println("Child coroutine after delay")
    }

    println("Main coroutine")
    child.suspend()
    child.resume()
}
```

이 코드에서는 resume 함수를 사용하여 자식 코루틴을 다시 시작합니다. 이 함수는 재개 함수를 인수로 사용합니다. 이 경우 재개 기능은 지연입니다. 이 함수는 지정된 시간(1000밀리초) 동안 코루틴을 일시 중지합니다.

이 코드를 실행하면 다음과 같은 출력이 표시됩니다.

```
Main coroutine
Child coroutine
Child coroutine after delay
```

자식 코루틴은 지연 함수가 호출된 후에 재개됩니다. 메인 코루틴은 계속 실행되고 "메인 코루틴"을 출력합니다.

## 코루틴 취소

취소 기능을 사용하여 코루틴을 취소할 수 있습니다.

```kotlin
import kotlinx.coroutines.*

fun main() {
    val parent = CoroutineScope(Job())

    val child = parent.launch {
        println("Child coroutine")
        delay(1000L)
        println("Child coroutine after delay")
    }

    println("Main coroutine")
    child.cancel()
}
```

이 코드에서는 취소 기능을 사용하여 자식 코루틴을 취소합니다. 이 함수는 일시 중단 함수를 인수로 사용합니다. 이 경우 일시 중지 기능은 지연입니다. 이 함수는 지정된 시간(1000밀리초) 동안 코루틴을 일시 중지합니다.

이 코드를 실행하면 다음과 같은 출력이 표시됩니다.

```
Main coroutine
Child coroutine
```

지연 함수가 호출된 후 자식 코루틴이 취소됩니다. 메인 코루틴은 계속 실행되고 "메인 코루틴"을 출력합니다.

## 결론

이 기사에서는 Kotlin의 코루틴에 대해 살펴보았습니다. 우리는 그것들이 무엇인지, 어떻게 작동하는지, 자신의 코드에서 어떻게 사용하는지 살펴보았습니다. 코루틴은 비동기 코드를 작성하는 강력한 방법입니다.