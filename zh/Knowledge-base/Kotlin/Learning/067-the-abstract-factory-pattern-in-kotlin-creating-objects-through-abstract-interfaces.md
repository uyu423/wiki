---
title: 067：Kotlin 中的抽象工厂模式：通过抽象接口创建对象
description: 
published: true
date: 2023-02-06T22:17:40.556Z
tags: 
editor: markdown
dateCreated: 2023-02-06T22:17:33.766Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [067: The Abstract Factory Pattern in Kotlin: Creating Objects Through Abstract Interfaces***English** document is available*](/en/Knowledge-base/Kotlin/Learning/067-the-abstract-factory-pattern-in-kotlin-creating-objects-through-abstract-interfaces)
{.links-list}


# Kotlin 中的抽象工厂模式：通过抽象接口创建对象

抽象工厂模式是一种创建型设计模式，它允许我们通过抽象接口创建对象。当我们需要创建属于更大系统（例如 GUI 或数据库）的对象时，此模式特别有用。

在这篇文章中，我们将看看如何在 Kotlin 中使用抽象工厂模式。我们将从查看此模式解决的问题开始。然后我们将看看如何在 Kotlin 中实现该模式。最后，我们将看看使用此模式的一些优点和缺点。

## 问题

考虑一个简单的 GUI 应用程序，它由一个带有按钮的窗口组成。我们可以使用抽象工厂模式创建这个窗口，如下所示：

```kotlin
interface Window {
    fun draw()
}

class Button(val window: Window) {
    fun draw() {
        // ...
    }
}

class Application {
    val window: Window

    init {
        window = WindowFactory.createWindow()
    }

    fun addButton(button: Button) {
        // ...
    }
}

object WindowFactory {
    fun createWindow(): Window {
        // ...
    }
}
```

在这个例子中，我们有一个窗口接口和该接口的具体实现。我们还有一个将窗口作为参数的按钮类。最后，我们有一个 Application 类，它创建一个窗口并向其中添加按钮。

抽象工厂模式允许我们将窗口的创建与应用程序的其余部分分离。这在我们需要支持多个平台（例如 Windows 和 macOS）时特别有用。我们可以简单地为每个平台创建一个新的 WindowFactory，应用程序的其余部分将继续像以前一样工作。

## 执行

现在让我们看看如何在 Kotlin 中实现抽象工厂模式。我们将从查看窗口的界面开始：

```kotlin
interface Window {
    fun draw()
}
```

接下来，我们将为我们的 Windows 平台创建此接口的具体实现：

```kotlin
class WindowsWindow : Window {
    override fun draw() {
        // ...
    }
}
```

我们现在可以创建一个 WindowsWindowFactory，它将返回我们的 WindowsWindow 类的实例：

```kotlin
class WindowsWindowFactory : WindowFactory {
    override fun createWindow(): Window {
        return WindowsWindow()
    }
}
```

我们现在可以创建一个 macOSWindowFactory，它将返回我们的 macOSWindow 类的实例：

```kotlin
class macOSWindowFactory : WindowFactory {
    override fun createWindow(): Window {
        return macOSWindow()
    }
}
```

最后，我们可以更新我们的 Application 类以使用我们新的 WindowFactory：

```kotlin
class Application {
    val window: Window

    init {
        window = WindowFactory.createWindow()
    }

    fun addButton(button: Button) {
        // ...
    }
}
```

## 好处

使用抽象工厂模式有几个好处：

- 该模式允许我们将对象的创建与代码的其余部分分离。当我们需要支持多个平台时，这尤其有用。

- 图案易于延伸。例如，我们可以通过创建一个新的 WindowFactory 轻松地添加一个新的平台。

- 该模式促进了接口的使用。这有利于代码的重用和可维护性。

## 缺点

使用抽象工厂模式也有一些缺点：

- 模式会导致大量样板代码。

- 模式可能难以理解和使用。