---
title: 096：Kotlin 中的移动开发：使用 Kotlin 和 Android/iOS 构建移动应用程序
description: 
published: true
date: 2023-02-14T12:18:36.616Z
tags: 
editor: markdown
dateCreated: 2023-02-14T12:18:29.043Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [096: Mobile Development in Kotlin: Building Mobile Apps with Kotlin and Android/iOS***English** document is available*](/en/Knowledge-base/Kotlin/Learning/096-mobile-development-in-kotlin-building-mobile-apps-with-kotlin-and-androidios)
{.links-list}


# 096：Kotlin 中的移动开发：使用 Kotlin 和 Android/iOS 构建移动应用程序

Kotlin 是一种静态类型的编程语言，运行在 Java 虚拟机上，也可以编译成 JavaScript 源代码。 Kotlin 由 JetBrains 开发，该公司是 IntelliJ IDEA Java IDE 背后的公司。

Kotlin 被设计为 Java 的改进版本，它提供了许多 Java 所没有的特性。 Kotlin 与 Java 完全互操作，因此可用于开发 Android 应用程序。

在本文中，我们将了解如何开始 Kotlin 和 Android 开发。我们将创建一个简单的“Hello, World!”应用程序，然后在 Android 设备上运行它。

## 入门

首先，您需要为 IntelliJ IDEA 安装 Kotlin 插件。您可以在 IDE 中执行此操作，方法是转到首选项 > 插件并搜索“Kotlin”。

安装 Kotlin 插件后，您可以通过转到“文件”>“新建”>“项目”并从项目模板列表中选择“Kotlin/JVM”来创建一个新的 Kotlin 项目。

## 创建一个 Kotlin 项目

创建 Kotlin 项目后，您可以通过转到文件 > 新建 > Kotlin 文件/类来创建新的 Kotlin 文件。

让我们在项目的 src/ 目录中创建一个名为“HelloWorld.kt”的文件。我们将从向文件中添加一个 main 函数开始：

```kotlin
fun main(args: Array<String>) {
    println("Hello, World!")
}
```

此函数打印字符串“Hello, World!”到控制台。

## 运行应用程序

要运行我们的 Kotlin 应用程序，我们需要创建一个运行配置。我们可以通过转到“运行”>“编辑配置”并单击“+”按钮来完成此操作。

从运行配置类型列表中，选择“Kotlin/JVM”。我们将我们的配置命名为“Hello, World!”并将主类设置为“HelloWorldKt”。

最后，我们需要选择一个设备来运行我们的应用程序。我们可以通过运行 > 编辑配置并选择我们的“Hello, World!”来完成此操作。配置。在“设备”下拉菜单下，选择您要使用的设备。

现在，我们已准备好在我们的 Android 设备上运行我们的 Kotlin 应用程序！