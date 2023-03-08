---
title: Kotlin 코루틴으로 애플리케이션 구축
description: 
published: true
date: 2023-02-17T18:01:35.021Z
tags: 
editor: markdown
dateCreated: 2023-01-30T03:09:12.347Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Building Applications with Kotlin Coroutines***English** version of this document is available*](/en/Knowledge-base/Kotlin/building-applications-with-kotlin-coroutines)
{.links-list}


# Kotlin 코루틴으로 애플리케이션 구축

코루틴은 버전 1.1에서 Kotlin에 추가되었으며 그 이후로 인기를 얻고 있습니다. Google의 Android 아키텍처 구성 요소, Spring Boot 및 ktor 웹 프레임워크를 포함하여 많은 유명 프로젝트에서 Kotlin 코루틴을 사용하도록 전환했습니다.

코루틴은 스레드보다 더 자연스러운 방식으로 동시 코드를 구성하는 방법입니다. 이를 통해 응답성이 뛰어나고 탄력적이며 유지 관리가 가능한 코드를 작성할 수 있습니다. 이 게시물에서는 Kotlin 코루틴을 사용하여 동시 애플리케이션을 빌드하는 방법을 살펴보겠습니다.

## 코루틴이 무엇인가요?

코루틴은 Kotlin 런타임에서 관리하는 경량 스레드입니다. 코루틴은 `kotlinx.coroutines` 패키지의 `launch` 또는 `async` 기능으로 생성할 수 있습니다.

코루틴은 일반 스레드와 비슷하지만 훨씬 가볍고 리소스를 적게 사용합니다. 나중에 살펴보겠지만 작업하기도 더 쉽습니다.

## 코루틴 만들기

기본 코루틴을 만드는 방법을 살펴보겠습니다. `launch` 함수를 사용하여 백그라운드에서 실행되는 코루틴을 생성합니다. `launch` 함수는 코루틴에서 실행될 코드를 포함하는 람다를 인수로 사용합니다.


```kotlin
val job = launch {
    // This code will be executed in the coroutine
}
```

## 코루틴에 합류하기

코루틴이 실행되면 백그라운드에서 실행되며 메인 스레드를 차단하지 않습니다. 그러나 때때로 우리는 계속하기 전에 코루틴이 끝날 때까지 기다리고 싶을 것입니다. 이는 'join' 기능으로 수행할 수 있습니다.

```kotlin
job.join() // Wait for the coroutine to finish
```

## 코루틴 일시 중지

코루틴은 `suspend` 키워드로 일시 중지할 수 있습니다. 이 키워드는 코루틴 내부에서만 사용할 수 있습니다. 코루틴이 일시 중단되면 메인 스레드를 차단하지 않습니다.

```kotlin
suspend fun foo() {
    // This code will be executed in the coroutine
}
```

## 코루틴 재개

코루틴은 'resume' 함수로 다시 시작할 수 있습니다. 이 함수는 코루틴 내부에서만 사용할 수 있습니다. 코루틴이 재개되면 마지막으로 일시 중지된 지점부터 계속 실행됩니다.

```kotlin
foo.resume() // Resume the coroutine
```

## 코루틴 취소

코루틴은 `cancel` 함수로 취소할 수 있습니다. 이 함수는 코루틴을 종료시킵니다. 코루틴에서 아직 실행되지 않은 코드는 실행되지 않습니다.

```kotlin
job.cancel() // Cancel the coroutine
```

## 코루틴 타임아웃 만들기

코루틴은 `withTimeout` 함수로 시간 초과되도록 만들 수 있습니다. 이 함수는 지정된 시간 제한 전에 완료되지 않으면 코루틴을 종료시킵니다.

```kotlin
withTimeout(1000L) {
    // This code will be executed in the coroutine
}
```

## 코루틴으로 예외 처리 사용

코루틴은 일반 스레드처럼 예외 처리와 함께 사용할 수 있습니다. `try`/`catch` 키워드는 코루틴에서 발생하는 예외를 포착하는 데 사용할 수 있습니다.

```kotlin
try {
    // This code will be executed in the coroutine
} catch (e: Exception) {
    // This code will be executed if an exception occurs
}
```

## 코루틴에 데이터 전달

'passData' 함수를 사용하여 데이터를 코루틴으로 전달할 수 있습니다. 이 함수는 재개될 때 코루틴에서 데이터를 사용할 수 있게 합니다.

```kotlin
val data = passData("some data")
```

## 코루틴에서 데이터 반환

`returnData` 함수를 사용하여 코루틴에서 데이터를 반환할 수 있습니다. 이 함수는 코루틴에서 호출자에게 데이터를 반환합니다.

```kotlin
val data = returnData()
```

## 코루틴 범위 만들기

코루틴 범위는 `coroutineScope` 함수로 만들 수 있습니다. 이 함수는 새로운 코루틴 범위를 생성합니다. 범위에서 생성된 모든 코루틴은 범위의 자식이 됩니다. 범위가 취소되면 모든 하위 항목이 취소됩니다.

```kotlin
val scope = coroutineScope {
    // This code will be executed in the scope
}
```

## 자식 코루틴 만들기

자식 코루틴은 `launchChild` 함수로 만들 수 있습니다. 이 함수는 현재 코루틴의 자식인 새 코루틴을 생성합니다. 부모 코루틴이 취소되면 자식 코루틴도 취소됩니다.

```kotlin
val child = launchChild {
    // This code will be executed in the child coroutine
}
```

## 코루틴 컨텍스트에 접근하기

코루틴 컨텍스트는 `coroutineContext` 속성으로 액세스할 수 있습니다. 이 속성은 코루틴의 현재 컨텍스트를 반환합니다. 컨텍스트는 부모 코루틴 또는 작업과 같은 코루틴에 대한 정보에 액세스하는 데 사용할 수 있습니다.

```kotlin
val context = coroutineContext
```

## 코루틴 잡 접근하기

코루틴 작업은 `coroutineJob` 속성으로 액세스할 수 있습니다. 이 속성은 코루틴의 현재 작업을 반환합니다. 작업을 사용하여 코루틴을 취소하거나 완료될 때까지 기다릴 수 있습니다.

```kotlin
val job = coroutineJob
```

## 부모 코루틴 접근하기

상위 코루틴은 `coroutineParent` 속성으로 액세스할 수 있습니다. 이 속성은 현재 코루틴의 상위 코루틴을 반환합니다. 부모 코루틴을 사용하여 현재 코루틴을 취소하거나 완료될 때까지 기다릴 수 있습니다.

```kotlin
val parent = coroutineParent
```

## 디스패처 접근

디스패처는 `coroutineDispatcher` 속성으로 액세스할 수 있습니다. 이 속성은 현재 코루틴의 디스패처를 반환합니다. 디스패처를 사용하여 코루틴이 실행되는 방식을 제어할 수 있습니다.

```kotlin
val dispatcher = coroutineDispatcher
```

## 다른 디스패처 사용

다양한 디스패처를 사용하여 코루틴 실행 방법을 제어할 수 있습니다. `runBlocking` 함수는 차단 디스패처에서 코루틴을 실행합니다. `withContext` 함수는 지정된 디스패처에서 코루틴을 실행합니다.

```kotlin
// Run the coroutine in the blocking dispatcher
runBlocking {
    // This code will be executed in the blocking dispatcher
}

// Run the coroutine in the Default dispatcher
withContext(Dispatchers.Default) {
    // This code will be executed in the Default dispatcher
}
```

## 스위칭 디스패처

Dispatcher는 `switchTo` 기능으로 전환할 수 있습니다. 이 함수는 현재 코루틴이 지정된 디스패처로 전환되도록 합니다.

```kotlin
// Switch to the Default dispatcher
switchTo(Dispatchers.Default)

// Switch to the blocking dispatcher
switchTo(Dispatchers.Main)
```

## ThreadLocal 데이터에 접근하기

스레드 로컬 데이터는 `threadLocalData` 속성으로 액세스할 수 있습니다. 이 속성은 현재 스레드에 대한 데이터를 반환합니다. 데이터는 이름이나 ID와 같은 스레드에 대한 정보를 저장하는 데 사용할 수 있습니다.

```kotlin
val data = threadLocalData
```

## 코루틴 이름에 접근하기

코루틴 이름은 `coroutineName` 속성으로 액세스할 수 있습니다. 이 속성은 현재 코루틴의 이름을 반환합니다. 이 이름은 디버깅 또는 로깅 용도로 사용할 수 있습니다.

```kotlin
val name = coroutineName
```

## 코루틴 이름 짓기

코루틴은 `withName` 함수로 이름을 지정할 수 있습니다. 이 함수는 지정된 이름이 현재 코루틴과 연결되도록 합니다.

```kotlin
// Name the coroutine "foo"
withName("foo") {
    // This code will be executed in the coroutine "foo"
}
```

## 코루틴 ID에 접근하기

코루틴 ID는 `coroutineId` 속성으로 액세스할 수 있습니다. 이 속성은 현재 코루틴의 ID를 반환합니다. ID는 디버깅 또는 로깅 용도로 사용할 수 있습니다.

```kotlin
val id = coroutineId
```

## 코루틴 종료

코루틴은 `coroutineTerminate` 함수로 종료할 수 있습니다. 이 함수는 코루틴을 즉시 종료시킵니다. 코루틴에서 아직 실행되지 않은 코드는 실행되지 않습니다.

```kotlin
coroutineTerminate() // Terminate the coroutine
```