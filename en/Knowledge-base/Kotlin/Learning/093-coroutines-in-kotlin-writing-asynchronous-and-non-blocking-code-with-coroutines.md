---
title: 093: Coroutines in Kotlin: Writing Asynchronous and Non-Blocking Code with Coroutines
description: 
published: true
date: 2023-02-17T22:06:21.572Z
tags: 
editor: markdown
dateCreated: 2023-02-17T22:06:20.214Z
---

- [093: Kotlin의 코루틴: 코루틴으로 비동기 및 비차단 코드 작성***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/093-coroutines-in-kotlin-writing-asynchronous-and-non-blocking-code-with-coroutines)
{.links-list}


# Coroutines in Kotlin: Writing Asynchronous and Non-Blocking Code with Coroutines

Asynchronous programming is a form of programming that allows a program to continue running without waiting for a particular event to finish. This can be useful when dealing with events that take a long time to complete, such as network requests.

Coroutines are a type of asynchronous programming that can be used in Kotlin. They are lightweight threads that can be used to run code in the background without blocking the main thread.

Coroutines can be used to write asynchronous and non-blocking code. They are often used for tasks such as network requests, database operations, and UI updates.

## Creating a Coroutine

A coroutine can be created using the `launch` function. This function takes a `suspend` lambda as an argument. The `suspend` keyword is used to mark a function as being able to be suspended.

```kotlin
launch {
    // code to be run in the background
}
```

## Suspending a Coroutine

A coroutine can be suspended using the `suspend` keyword. This keyword can be used to mark a function as being able to be suspended. A suspended function can be resumed at a later time.

```kotlin
suspend fun doSomething() {
    // code to be run in the background
}
```

## Resuming a Coroutine

A coroutine can be resumed using the `resume` function. This function takes a `suspend` lambda as an argument. The `suspend` keyword is used to mark a function as being able to be resumed.

```kotlin
resume {
    // code to be run in the background
}
```

## Cancelling a Coroutine

A coroutine can be cancelled using the `cancel` function. This function takes a `suspend` lambda as an argument. The `suspend` keyword is used to mark a function as being able to be cancelled.

```kotlin
cancel {
    // code to be run in the background
}
```

## Using Coroutines with UI Updates

Coroutines can be used to update the UI without blocking the main thread. This can be done using the `withContext` function. This function takes a `suspend` lambda as an argument. The `suspend` keyword is used to mark a function as being able to be suspended.

```kotlin
withContext {
    // code to be run in the background
}
```

## Conclusion

Coroutines are a type of asynchronous programming that can be used in Kotlin. They are lightweight threads that can be used to run code in the background without blocking the main thread.

Coroutines can be used to write asynchronous and non-blocking code. They are often used for tasks such as network requests, database operations, and UI updates.