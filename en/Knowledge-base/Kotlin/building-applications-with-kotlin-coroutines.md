---
title: Building Applications with Kotlin Coroutines
description: 
published: true
date: 2023-02-17T18:01:33.573Z
tags: 
editor: markdown
dateCreated: 2023-01-30T03:09:12.338Z
---

- [Kotlin 코루틴으로 애플리케이션 구축***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/building-applications-with-kotlin-coroutines)
{.links-list}


# Building Applications with Kotlin Coroutines

Coroutines were added to Kotlin in version 1.1 and have been gaining popularity ever since. Numerous high-profile projects have switched to using Kotlin coroutines, including Google's Android Architecture Components, Spring Boot, and the ktor web framework.

Coroutines are a way of structuring concurrent code in a more natural way than threads. They allow you to write code that is more responsive, elastic, and maintainable. In this post, we'll take a look at how to use Kotlin coroutines to build concurrent applications.

## What are Coroutines?

A coroutine is a light-weight thread that is managed by the Kotlin runtime. Coroutines can be created with the `launch` or `async` functions from the `kotlinx.coroutines` package.

Coroutines are like regular threads, but they are much lighter-weight and consume less resources. They are also easier to work with, as we'll see later on.

## Creating a Coroutine

Let's take a look at how to create a basic coroutine. We'll use the `launch` function to create a coroutine that runs in the background. The `launch` function takes a lambda as an argument, which contains the code that will be executed in the coroutine.


```kotlin
val job = launch {
    // This code will be executed in the coroutine
}
```

## Joining a Coroutine

When a coroutine is launched, it will run in the background and will not block the main thread. However, sometimes we'll want to wait for a coroutine to finish before continuing. This can be done with the `join` function.

```kotlin
job.join() // Wait for the coroutine to finish
```

## Suspending a Coroutine

A coroutine can be suspended with the `suspend` keyword. This keyword can only be used inside a coroutine. When a coroutine is suspended, it will not block the main thread.

```kotlin
suspend fun foo() {
    // This code will be executed in the coroutine
}
```

## Resuming a Coroutine

A coroutine can be resumed with the `resume` function. This function can only be used inside a coroutine. When a coroutine is resumed, it will continue running from the point where it was last suspended.

```kotlin
foo.resume() // Resume the coroutine
```

## Cancelling a Coroutine

A coroutine can be cancelled with the `cancel` function. This function will cause the coroutine to terminate. Any code that has not yet been executed in the coroutine will not be executed.

```kotlin
job.cancel() // Cancel the coroutine
```

## Making a Coroutine Timeout

A coroutine can be made to timeout with the `withTimeout` function. This function will cause the coroutine to terminate if it does not finish before the specified time limit.

```kotlin
withTimeout(1000L) {
    // This code will be executed in the coroutine
}
```

## Using Exception Handling with Coroutines

Coroutines can be used with exception handling just like regular threads. The `try`/`catch` keywords can be used to catch exceptions that occur in a coroutine.

```kotlin
try {
    // This code will be executed in the coroutine
} catch (e: Exception) {
    // This code will be executed if an exception occurs
}
```

## Passing Data into a Coroutine

Data can be passed into a coroutine with the `passData` function. This function will cause the data to be available in the coroutine when it is resumed.

```kotlin
val data = passData("some data")
```

## Returning Data from a Coroutine

Data can be returned from a coroutine with the `returnData` function. This function will return the data from the coroutine to the caller.

```kotlin
val data = returnData()
```

## Creating a Coroutine Scope

A coroutine scope can be created with the `coroutineScope` function. This function will create a new coroutine scope. All coroutines created in the scope will be children of the scope. When the scope is cancelled, all of its children will be cancelled.

```kotlin
val scope = coroutineScope {
    // This code will be executed in the scope
}
```

## Creating a Child Coroutine

A child coroutine can be created with the `launchChild` function. This function will create a new coroutine that is a child of the current coroutine. When the parent coroutine is cancelled, the child coroutine will be cancelled.

```kotlin
val child = launchChild {
    // This code will be executed in the child coroutine
}
```

## Accessing the Coroutine Context

The coroutine context can be accessed with the `coroutineContext` property. This property will return the current context of the coroutine. The context can be used to access information about the coroutine, such as its parent coroutine or its job.

```kotlin
val context = coroutineContext
```

## Accessing the Coroutine Job

The coroutine job can be accessed with the `coroutineJob` property. This property will return the current job of the coroutine. The job can be used to cancel the coroutine or to wait for it to finish.

```kotlin
val job = coroutineJob
```

## Accessing the Parent Coroutine

The parent coroutine can be accessed with the `coroutineParent` property. This property will return the parent coroutine of the current coroutine. The parent coroutine can be used to cancel the current coroutine or to wait for it to finish.

```kotlin
val parent = coroutineParent
```

## Accessing Dispatchers

Dispatchers can be accessed with the `coroutineDispatcher` property. This property will return the dispatcher of the current coroutine. The dispatcher can be used to control how the coroutine runs.

```kotlin
val dispatcher = coroutineDispatcher
```

## Using Different Dispatchers

Different dispatchers can be used to control how a coroutine runs. The `runBlocking` function will run a coroutine in the blocking dispatcher. The `withContext` function will run a coroutine in the specified dispatcher.

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

## Switching Dispatchers

Dispatchers can be switched with the `switchTo` function. This function will cause the current coroutine to switch to the specified dispatcher.

```kotlin
// Switch to the Default dispatcher
switchTo(Dispatchers.Default)

// Switch to the blocking dispatcher
switchTo(Dispatchers.Main)
```

## Accessing the ThreadLocal Data

Thread-local data can be accessed with the `threadLocalData` property. This property will return the data for the current thread. The data can be used to store information about the thread, such as its name or its ID.

```kotlin
val data = threadLocalData
```

## Accessing the Coroutine Name

The coroutine name can be accessed with the `coroutineName` property. This property will return the name of the current coroutine. The name can be used for debugging or logging purposes.

```kotlin
val name = coroutineName
```

## Naming Coroutines

Coroutines can be named with the `withName` function. This function will cause the specified name to be associated with the current coroutine.

```kotlin
// Name the coroutine "foo"
withName("foo") {
    // This code will be executed in the coroutine "foo"
}
```

## Accessing the Coroutine ID

The coroutine ID can be accessed with the `coroutineId` property. This property will return the ID of the current coroutine. The ID can be used for debugging or logging purposes.

```kotlin
val id = coroutineId
```

## Terminating a Coroutine

A coroutine can be terminated with the `coroutineTerminate` function. This function will cause the coroutine to terminate immediately. Any code that has not yet been executed in the coroutine will not be executed.

```kotlin
coroutineTerminate() // Terminate the coroutine
```