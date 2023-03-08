---
title: 084: Kotlin에서 디버깅: 중단점, 감시 및 로그로 Kotlin 코드 디버깅
description: 
published: true
date: 2023-02-14T22:17:16.054Z
tags: 
editor: markdown
dateCreated: 2023-02-14T22:17:14.486Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [084: Debugging in Kotlin: Debugging Your Kotlin Code with Breakpoints, Watches, and Logs***English** document is available*](/en/Knowledge-base/Kotlin/Learning/084-debugging-in-kotlin-debugging-your-kotlin-code-with-breakpoints-watches-and-logs)
{.links-list}


# Kotlin 디버깅: 중단점, 감시 및 로그로 Kotlin 코드 디버깅

디버깅은 모든 개발자에게 필수적인 기술입니다. 프로그램이 올바르게 실행되도록 코드에서 오류를 찾고 수정할 수 있습니다.

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 프로그래밍 언어입니다. Java와 상호 운용이 가능하도록 설계된 정적으로 유형이 지정된 언어입니다. Kotlin은 점점 인기를 얻고 있는 간결하고 안전하며 강력한 언어입니다.

이 게시물에서는 중단점, 감시 및 로그를 사용하여 Kotlin 코드를 디버그하는 방법을 알아봅니다. 또한 Kotlin 코드 디버깅을 위한 몇 가지 모범 사례에 대해서도 알아봅니다.

## 중단점이란 무엇입니까?

중단점은 프로그램 실행이 일시 중지되는 코드의 지점입니다. 이를 통해 프로그램의 상태를 검사하고 진행 상황을 확인할 수 있습니다. 중단점은 코드에서 문제가 있는 위치를 좁힐 수 있기 때문에 디버깅에 매우 유용합니다.

중단점에는 줄 중단점과 메서드 중단점의 두 가지 유형이 있습니다. 줄 중단점은 특정 코드 줄에 설정되며 해당 줄에 도달하면 프로그램 실행을 일시 중지합니다. 메서드 중단점은 특정 메서드에 설정되며 해당 메서드가 호출될 때 프로그램 실행을 일시 중지합니다.

다음 구문을 사용하여 Kotlin에서 중단점을 설정할 수 있습니다.

```kotlin
val x = 5

x.setBreakpoint() // line breakpoint

fun foo() {
    // ...
}

foo.setBreakpoint() // method breakpoint
```

## 시계란?

감시는 프로그램이 실행되는 동안 모니터링하는 변수입니다. 다음 구문을 사용하여 Kotlin에서 감시를 설정할 수 있습니다.

```kotlin
val x = 5

x.watch() // watch x

fun foo() {
    // ...
}

foo.watch() // watch foo
```

## 로그란?

로그는 프로그램이 실행되는 동안 인쇄할 수 있는 메시지입니다. 이것은 특정 시점에서 코드에서 어떤 일이 벌어지고 있는지 볼 수 있기 때문에 디버깅에 유용할 수 있습니다. 다음 구문을 사용하여 Kotlin에서 로그를 설정할 수 있습니다.

```kotlin
val x = 5

x.log() // print x

fun foo() {
    // ...
}

foo.log() // print foo
```

## Kotlin 코드 디버깅 모범 사례

다음은 Kotlin 코드 디버깅을 위한 몇 가지 모범 사례입니다.

- 중단점을 사용하여 코드에서 문제가 있는 위치를 좁힙니다.
- 프로그램이 실행되는 동안 시계를 사용하여 변수를 모니터링합니다.
- 로그를 사용하여 프로그램이 실행되는 동안 메시지를 출력하십시오.
- 디버깅할 때 인내심을 갖고 체계적으로 행동하십시오. 답답할 수 있지만 시간을 들여 결국 문제를 찾을 수 있습니다.

## 추가 정보

- [Kotlin 디버깅 문서](https://kotlinlang.org/docs/reference/debugging.html)
- [IntelliJ IDEA 디버깅 설명서](https://www.jetbrains.com/help/idea/debugging.html)
- [Eclipse 디버깅 문서](https://help.eclipse.org/2018-09/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Fconcepts%2Fconcepts-debug.htm)