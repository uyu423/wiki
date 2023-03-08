---
title: 082: Testing in Kotlin: Writing and Running Tests for Your Kotlin Code
description: 
published: true
date: 2023-02-10T22:55:30.915Z
tags: 
editor: markdown
dateCreated: 2023-02-10T22:55:24.347Z
---

- [082: Pruebas en Kotlin: escribir y ejecutar pruebas para su código Kotlin***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/082-testing-in-kotlin-writing-and-running-tests-for-your-kotlin-code)
{.links-list}
- [082：在 Kotlin 中测试：为您的 Kotlin 代码编写和运行测试***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/082-testing-in-kotlin-writing-and-running-tests-for-your-kotlin-code)
{.links-list}
- [082: Kotlin 테스트: Kotlin 코드 테스트 작성 및 실행***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/082-testing-in-kotlin-writing-and-running-tests-for-your-kotlin-code)
{.links-list}


# 082: Testing in Kotlin: Writing and Running Tests for Your Kotlin Code

Testing is a critical part of the software development process. It helps ensure that your code is correct and works as expected. In this post, we'll learn how to write and run tests for Kotlin code.

## Writing Tests

Tests are written in Kotlin using the [JUnit](https://junit.org/) framework. JUnit is a popular testing framework for Java that can be used for Kotlin projects.

To write a test, create a new Kotlin file in your project and annotate it with the `@Test` annotation. This annotation tells the JUnit framework that the code in this file is a test.

```kotlin
@Test
fun test() {
    // code for the test goes here
}
```

Tests are typically made up of three parts: setup, execution, and verification. In the setup phase, you'll initialize any objects or data that are needed for the test. In the execution phase, you'll run the code that you're testing. In the verification phase, you'll assert that the code behaved as expected.

Let's look at a simple example. Suppose we have a function that calculates the factorial of a number. We can write a test for this function using the following template:

```kotlin
@Test
fun test() {
    // setup
    val input = 5

    // execution
    val output = factorial(input)

    // verification
    assertEquals(120, output)
}
```

In the setup phase, we create a variable `input` and set it to `5`. In the execution phase, we call the `factorial` function with `input` as an argument. This function returns the factorial of `input`, which we store in the `output` variable. In the verification phase, we use the `assertEquals` function to assert that `output` is equal to `120`.

If we run this test and it passes, we can be confident that our `factorial` function is working correctly.

## Running Tests

Tests can be run from the command line or from within an IDE. To run tests from the command line, you'll need to use the [Gradle](https://gradle.org/) build tool. Gradle is a build tool for Java projects that can be used for Kotlin projects.

To run tests from the command line, navigate to the root directory of your project and run the following command:

```
gradle test
```

This will run all of the tests in your project.

To run tests from within an IDE, you'll need to install the [JUnit plugin](https://plugins.gradle.org/plugin/org.junit.platform.idea) for your IDE. Once the plugin is installed, you should be able to run tests from within your IDE.

## Additional Information

- [JUnit website](https://junit.org/)
- [JUnit documentation](https://junit.org/junit5/docs/current/user-guide/)
- [Gradle website](https://gradle.org/)
- [Gradle documentation](https://docs.gradle.org/current/userguide/userguide.html)