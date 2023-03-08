---
title: 067: The Abstract Factory Pattern in Kotlin: Creating Objects Through Abstract Interfaces
description: 
published: true
date: 2023-02-06T22:17:35.408Z
tags: 
editor: markdown
dateCreated: 2023-02-06T22:17:33.773Z
---

- [067: The Abstract Factory Pattern en Kotlin: creación de objetos a través de interfaces abstractas***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/067-the-abstract-factory-pattern-in-kotlin-creating-objects-through-abstract-interfaces)
{.links-list}
- [067：Kotlin 中的抽象工厂模式：通过抽象接口创建对象***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/067-the-abstract-factory-pattern-in-kotlin-creating-objects-through-abstract-interfaces)
{.links-list}
- [067: Kotlin의 추상 팩토리 패턴: 추상 인터페이스를 통해 객체 생성***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/067-the-abstract-factory-pattern-in-kotlin-creating-objects-through-abstract-interfaces)
{.links-list}


# The Abstract Factory Pattern in Kotlin: Creating Objects Through Abstract Interfaces

The Abstract Factory pattern is a creational design pattern that allows us to create objects through abstract interfaces. This pattern is particularly useful when we need to create objects that are part of a larger system, such as a GUI or a database.

In this post, we'll take a look at how to use the Abstract Factory pattern in Kotlin. We'll start by looking at the problem that this pattern solves. We'll then look at how to implement the pattern in Kotlin. Finally, we'll look at some of the benefits and drawbacks of using this pattern.

## The Problem

Consider a simple GUI application that consists of a window with a button. We can create this window using the Abstract Factory pattern as follows:

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

In this example, we have an interface for a window and a concrete implementation of that interface. We also have a button class that takes a window as a parameter. Finally, we have an Application class that creates a window and adds buttons to it.

The Abstract Factory pattern allows us to decouple the creation of the window from the rest of the application. This is particularly useful when we need to support multiple platforms, such as Windows and macOS. We can simply create a new WindowFactory for each platform and the rest of the application will continue to work as before.

## Implementation

Let's now take a look at how to implement the Abstract Factory pattern in Kotlin. We'll start by looking at the interface for our window:

```kotlin
interface Window {
    fun draw()
}
```

Next, we'll create a concrete implementation of this interface for our Windows platform:

```kotlin
class WindowsWindow : Window {
    override fun draw() {
        // ...
    }
}
```

We can now create a WindowsWindowFactory that will return instances of our WindowsWindow class:

```kotlin
class WindowsWindowFactory : WindowFactory {
    override fun createWindow(): Window {
        return WindowsWindow()
    }
}
```

We can now create a macOSWindowFactory that will return instances of our macOSWindow class:

```kotlin
class macOSWindowFactory : WindowFactory {
    override fun createWindow(): Window {
        return macOSWindow()
    }
}
```

Finally, we can update our Application class to use our new WindowFactory:

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

## Benefits

There are several benefits to using the Abstract Factory pattern:

- The pattern allows us to decouple the creation of objects from the rest of our code. This is particularly useful when we need to support multiple platforms.

- The pattern is easy to extend. For example, we can easily add a new platform by creating a new WindowFactory.

- The pattern promotes the use of interfaces. This can be beneficial for code reuse and maintainability.

## Drawbacks

There are also some drawbacks to using the Abstract Factory pattern:

- The pattern can lead to a lot of boilerplate code.

- The pattern can be difficult to understand and use.