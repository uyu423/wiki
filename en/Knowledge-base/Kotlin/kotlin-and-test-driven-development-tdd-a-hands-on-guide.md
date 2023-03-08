---
title: Kotlin and Test Driven Development (TDD): A Hands-on Guide
description: 
published: true
date: 2023-02-17T18:08:45.125Z
tags: 
editor: markdown
dateCreated: 2023-01-30T16:57:19.001Z
---

- [Kotlin 및 테스트 주도 개발(TDD): 실습 가이드***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/kotlin-and-test-driven-development-tdd-a-hands-on-guide)
{.links-list}
- [Kotlin とテスト駆動開発 (TDD): ハンズオン ガイド***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/kotlin-and-test-driven-development-tdd-a-hands-on-guide)
{.links-list}
- [Kotlin 和测试驱动开发 (TDD)：实践指南***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/kotlin-and-test-driven-development-tdd-a-hands-on-guide)
{.links-list}


# Kotlin and Test Driven Development (TDD): A Hands-on Guide

Kotlin is a statically typed programming language that targets the JVM, Android, JavaScript, and Native. It's an open source project under the Apache 2.0 license. Kotlin is also a functional programming language with higher-order functions. Developers can use Kotlin with all existing Java libraries and frameworks.

## What is Test Driven Development (TDD)?

Test-driven development is a development methodology which dictates that tests should be written before code is written. The purpose of this is to ensure that the code satisfies the requirements specified by the test. This methodology is also intended to make code more robust and easier to refactor.

## Why Use Kotlin for TDD?

Kotlin is a very concise language, which can lead to less code overall. This is important for writing tests, as the more code there is, the more time it takes to write tests for all of the functionality. In addition, Kotlin has null safety built in, which helps to avoid null pointer exceptions. This is especially important in tests, as any null pointers will cause the test to fail.

## Setting Up a Kotlin Project for TDD

Assuming that you have already installed the Kotlin plugin for your IDE, create a new Kotlin project. When prompted, choose "Java" as the project template. For this guide, we will be using the Gradle build system.

## Your First Kotlin Test

Now that we have a project set up, let's write our first test. We'll start by creating a file in the `src/test/kotlin` directory called `MyFirstTest.kt`. In this file, we'll write a test to check that Kotlin's `sum` function works as expected:

```kotlin
import org.junit.Assert.*
import org.junit.Test

class MyFirstTest {
    @Test
    fun testSum() {
        assertEquals(4, sum(2, 2))
    }
}
```

Here, we've imported the `junit` library, which we'll use for writing our tests. We've also created a `MyFirstTest` class, which contains a single `testSum` method. This method uses the `assertEquals` function to check that the result of calling `sum` with the arguments `2` and `2` is equal to `4`.

To run this test, right-click on the `MyFirstTest.kt` file and select "Run 'MyFirstTest'". You should see the test run and pass.

## Writing the Code

Now that we have a failing test, it's time to write the code to make it pass. Create a file in the `src/main/kotlin` directory called `MyFirst.kt`. In this file, we'll write the `sum` function:

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

Now if you re-run the test, it should pass.

## Conclusion

In this article, we've seen how to set up a Kotlin project for TDD and how to write our first test and code to make it pass. TDD is a great way to ensure that your code is correct and easy to refactor. Kotlin's concise syntax and built-in null safety make it an ideal language for TDD.