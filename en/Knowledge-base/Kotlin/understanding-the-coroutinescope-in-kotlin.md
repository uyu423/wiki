---
title: Understanding the CoroutineScope in Kotlin
description: 
published: true
date: 2023-02-14T07:55:25.193Z
tags: 
editor: markdown
dateCreated: 2023-02-14T07:55:17.879Z
---

- [Entendiendo CoroutineScope en Kotlin***Spanish** document is available*](/es/Knowledge-base/Kotlin/understanding-the-coroutinescope-in-kotlin)
{.links-list}
- [了解 Kotlin 中的 CoroutineScope***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/understanding-the-coroutinescope-in-kotlin)
{.links-list}
- [Kotlin의 CoroutineScope 이해***Korean** document is available*](/ko/Knowledge-base/Kotlin/understanding-the-coroutinescope-in-kotlin)
{.links-list}


# Understanding the CoroutineScope in Kotlin

Coroutines are a powerful tool for concurrent programming in Kotlin. They are light-weight threads that can be used to improve the performance of your Kotlin application.

In this article, we will take a look at the CoroutineScope and how it can be used to manage coroutines in your application.

## What is CoroutineScope?

CoroutineScope is a class in the Kotlin coroutine library that is used to manage the lifecycle of coroutines. It provides a way to cancel all coroutines started in its scope when the scope is canceled.

Scopes can be created using the coroutineScope builder function. This builder function creates a new scope and adds it to the current scope.

Let's take a look at a simple example:

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

In the example above, we use the coroutineScope builder function to create a new scope. We then launch a coroutine in the scope. The coroutine will delay for one second and then print "World!".

Notice that the coroutine is launched in the scope. This means that the coroutine will be canceled when the scope is canceled.

## Cancelling CoroutineScope

 CoroutineScope can be canceled using the cancel method. This method will cancel all coroutines started in the scope. Let's take a look at a simple example:

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

In the example above, we create a new scope and launch a coroutine in the scope. The coroutine will delay for one second and then print "World!".

We then call the cancel method on the scope. This will cancel all coroutines started in the scope. In this case, the coroutine will not print "World!" because it was canceled before it had a chance to run.

## Conclusion

In this article, we have looked at the CoroutineScope and how it can be used to manage coroutines in your application. We have also seen how to cancel a scope and how this will cancel all coroutines started in the scope.