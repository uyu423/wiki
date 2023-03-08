---
title: 开始使用 Kotlin 进行后端开发
description: 
published: true
date: 2023-01-31T06:23:17.706Z
tags: 
editor: markdown
dateCreated: 2023-01-31T06:23:16.143Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Getting Started with Kotlin for Backend Development***English** version of this document is available*](/en/Knowledge-base/Backend/getting-started-with-kotlin-for-backend-development)
{.links-list}


# 开始使用 Kotlin 进行后端开发

Kotlin 是一种针对 JVM、Android、JavaScript 和 Native 的静态类型编程语言。它由 JetBrains 开发。 Kotlin 旨在与 Java 完全互操作，JVM 版本可以运行任何 Java 代码。 Kotlin 在 Apache 2 开源许可下发布。

据 JetBrains 称，超过 60% 的 Kotlin 项目使用该语言进行后端开发。原因有很多：Kotlin 简洁、安全、Null-Pointer-Proof™，并且有很好的工具支持。它还可以与 Java 100% 互操作，这意味着您可以在 Kotlin 代码中使用所有现有的 Java 库。

在本文中，我们将了解如何开始使用 Kotlin 进行后端开发。我们将了解如何设置 Kotlin 项目、使用 Kotlin 编写代码并在 JVM 上运行它。

## 设置 Kotlin 项目

设置 Kotlin 项目的方法有很多种。在本文中，我们将使用 Gradle 构建工具。 Gradle 是一个构建工具，专注于构建自动化并支持多种语言。使用 Gradle Kotlin DSL 可以轻松创建 Kotlin 项目。

我们需要做的第一件事是在项目的根目录中创建一个名为“build.gradle.kts”的文件。此文件包含我们的 Kotlin 项目的配置。

```kotlin
plugins {
    id("org.jetbrains.kotlin.jvm") version "1.3.72"
}

group = "com.example"
version = "1.0-SNAPSHOT"

repositories {
    jcenter()
}

dependencies {
    implementation("org.jetbrains.kotlin:kotlin-stdlib-jdk8")
}

tasks.withType<Test> {
    useJUnitPlatform()
}
```

在 `build.gradle.kts` 文件中，我们配置了 Kotlin 插件并添加了对 Kotlin stdlib 的依赖。我们还配置了 `test` 任务以使用 JUnit 平台。

## 编写 Kotlin 代码

现在我们已经设置了一个 Kotlin 项目，我们可以编写一些 Kotlin 代码。我们将从在 `src/` 目录中创建一个名为 `Main.kt` 的文件开始。

在“Main.kt”中，我们将编写一个简单的 Kotlin 程序来打印“Hello, world!”到控制台。

```kotlin
fun main() {
    println("Hello, world!")
}
```

Kotlin 程序以 `main` 函数开始。 `main` 函数是我们程序的入口点。在 `main` 函数中，我们打印了字符串“Hello, world!”到控制台。

## 运行 Kotlin 代码

Kotlin 代码无需任何额外配置即可在 JVM 上运行。要运行我们的 Kotlin 程序，我们可以使用“gradle run”命令。这将编译我们的 Kotlin 代码并运行 `main` 函数。

```
$ gradle run

> Task :run
Hello, world!

BUILD SUCCESSFUL in 0s
2 actionable tasks: 2 executed
```

## 结论

在本文中，我们了解了如何开始使用 Kotlin 进行后端开发。我们已经建立了一个 Kotlin 项目，编写了一些 Kotlin 代码，并在 JVM 上运行它。 Kotlin 是一种用于后端开发的出色语言，我们只是触及了它的皮毛。