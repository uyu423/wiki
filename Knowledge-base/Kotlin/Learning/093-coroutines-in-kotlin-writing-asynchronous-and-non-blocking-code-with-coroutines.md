---
title: 093: Kotlin의 코루틴: 코루틴으로 비동기 및 비차단 코드 작성
description: 
published: true
date: 2023-02-17T22:06:27.043Z
tags: 
editor: markdown
dateCreated: 2023-02-17T22:06:20.207Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [093: Coroutines in Kotlin: Writing Asynchronous and Non-Blocking Code with Coroutines***English** document is available*](/en/Knowledge-base/Kotlin/Learning/093-coroutines-in-kotlin-writing-asynchronous-and-non-blocking-code-with-coroutines)
{.links-list}


# Kotlin의 코루틴: 코루틴으로 비동기 및 비차단 코드 작성

비동기 프로그래밍은 특정 이벤트가 완료될 때까지 기다리지 않고 프로그램이 계속 실행되도록 하는 프로그래밍의 한 형태입니다. 이는 네트워크 요청과 같이 완료하는 데 오랜 시간이 걸리는 이벤트를 처리할 때 유용할 수 있습니다.

코루틴은 Kotlin에서 사용할 수 있는 일종의 비동기 프로그래밍입니다. 기본 스레드를 차단하지 않고 백그라운드에서 코드를 실행하는 데 사용할 수 있는 경량 스레드입니다.

코루틴은 비동기 및 비차단 코드를 작성하는 데 사용할 수 있습니다. 네트워크 요청, 데이터베이스 작업 및 UI 업데이트와 같은 작업에 자주 사용됩니다.

## 코루틴 만들기

코루틴은 `launch` 함수를 사용하여 만들 수 있습니다. 이 함수는 `suspend` 람다를 인수로 사용합니다. `suspend` 키워드는 기능을 일시 중지할 수 있는 것으로 표시하는 데 사용됩니다.

```kotlin
launch {
    // code to be run in the background
}
```

## 코루틴 일시 중지

코루틴은 `suspend` 키워드를 사용하여 일시 중지할 수 있습니다. 이 키워드는 기능을 일시 중지할 수 있는 것으로 표시하는 데 사용할 수 있습니다. 일시 중단된 기능은 나중에 재개할 수 있습니다.

```kotlin
suspend fun doSomething() {
    // code to be run in the background
}
```

## 코루틴 재개

코루틴은 'resume' 함수를 사용하여 재개할 수 있습니다. 이 함수는 `suspend` 람다를 인수로 사용합니다. `suspend` 키워드는 기능을 재개할 수 있는 것으로 표시하는 데 사용됩니다.

```kotlin
resume {
    // code to be run in the background
}
```

## 코루틴 취소

코루틴은 `cancel` 함수를 사용하여 취소할 수 있습니다. 이 함수는 `suspend` 람다를 인수로 사용합니다. `suspend` 키워드는 기능을 취소할 수 있는 것으로 표시하는 데 사용됩니다.

```kotlin
cancel {
    // code to be run in the background
}
```

## UI 업데이트와 함께 코루틴 사용하기

코루틴을 사용하여 메인 스레드를 차단하지 않고 UI를 업데이트할 수 있습니다. 이것은 `withContext` 함수를 사용하여 수행할 수 있습니다. 이 함수는 `suspend` 람다를 인수로 사용합니다. `suspend` 키워드는 기능을 일시 중지할 수 있는 것으로 표시하는 데 사용됩니다.

```kotlin
withContext {
    // code to be run in the background
}
```

## 결론

코루틴은 Kotlin에서 사용할 수 있는 일종의 비동기 프로그래밍입니다. 기본 스레드를 차단하지 않고 백그라운드에서 코드를 실행하는 데 사용할 수 있는 경량 스레드입니다.

코루틴은 비동기 및 비차단 코드를 작성하는 데 사용할 수 있습니다. 네트워크 요청, 데이터베이스 작업 및 UI 업데이트와 같은 작업에 자주 사용됩니다.