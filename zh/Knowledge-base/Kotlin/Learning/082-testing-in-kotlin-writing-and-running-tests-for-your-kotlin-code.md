---
title: 082：在 Kotlin 中测试：为您的 Kotlin 代码编写和运行测试
description: 
published: true
date: 2023-02-10T22:55:26.024Z
tags: 
editor: markdown
dateCreated: 2023-02-10T22:55:24.344Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [082: Testing in Kotlin: Writing and Running Tests for Your Kotlin Code***English** document is available*](/en/Knowledge-base/Kotlin/Learning/082-testing-in-kotlin-writing-and-running-tests-for-your-kotlin-code)
{.links-list}


# 082：在 Kotlin 中测试：为您的 Kotlin 代码编写和运行测试

测试是软件开发过程的关键部分。它有助于确保您的代码正确并按预期工作。在本文中，我们将学习如何为 Kotlin 代码编写和运行测试。

## 编写测试

测试是使用 [JUnit](https://junit.org/) 框架在 Kotlin 中编写的。 JUnit 是一种流行的 Java 测试框架，可用于 Kotlin 项目。

要编写测试，请在您的项目中创建一个新的 Kotlin 文件，并使用“@Test”注释对其进行注释。这个注释告诉 JUnit 框架这个文件中的代码是一个测试。

```kotlin
@Test
fun test() {
    // code for the test goes here
}
```

测试通常由三部分组成：设置、执行和验证。在设置阶段，您将初始化测试所需的任何对象或数据。在执行阶段，您将运行正在测试的代码。在验证阶段，您将断言代码的行为符合预期。

让我们看一个简单的例子。假设我们有一个计算数字阶乘的函数。我们可以使用以下模板为此函数编写测试：

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

在设置阶段，我们创建一个变量“input”并将其设置为“5”。在执行阶段，我们以 `input` 作为参数调用 `factorial` 函数。此函数返回“input”的阶乘，我们将其存储在“output”变量中。在验证阶段，我们使用 assertEquals 函数断言 output 等于 120。

如果我们运行这个测试并且它通过了，我们就可以确信我们的“factorial”函数工作正常。

## 运行测试

可以从命令行或从 IDE 中运行测试。要从命令行运行测试，您需要使用 [Gradle](https://gradle.org/) 构建工具。 Gradle 是 Java 项目的构建工具，可用于 Kotlin 项目。

要从命令行运行测试，请导航到项目的根目录并运行以下命令：

```
gradle test
```

这将运行项目中的所有测试。

要从 IDE 中运行测试，您需要为您的 IDE 安装 [JUnit 插件](https://plugins.gradle.org/plugin/org.junit.platform.idea)。安装插件后，您应该能够从 IDE 中运行测试。

## 附加信息

- [JUnit 网站](https://junit.org/)
- [JUnit 文档](https://junit.org/junit5/docs/current/user-guide/)
- [摇篮网站](https://gradle.org/)
- [Gradle 文档](https://docs.gradle.org/current/userguide/userguide.html)