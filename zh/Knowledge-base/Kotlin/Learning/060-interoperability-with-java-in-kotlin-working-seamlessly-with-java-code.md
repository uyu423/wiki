---
title: 060：Kotlin 中与 Java 的互操作性：与 Java 代码无缝协作
description: 
published: true
date: 2023-02-16T21:32:43.981Z
tags: 
editor: markdown
dateCreated: 2023-02-16T21:32:41.772Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [060: Interoperability with Java in Kotlin: Working Seamlessly with Java Code***English** document is available*](/en/Knowledge-base/Kotlin/Learning/060-interoperability-with-java-in-kotlin-working-seamlessly-with-java-code)
{.links-list}


# Kotlin 中与 Java 的互操作性：与 Java 代码无缝协作

作为 Android 的官方编程语言，Java 一直是许多开发人员的首选。然而，Kotlin 是编程语言领域的一颗冉冉升起的新星，它提供的许多特性使其成为 Java 的绝佳替代品。

Kotlin 的最大优势之一是它与 Java 的互操作性。这意味着您可以轻松地将 Kotlin 与现有的 Java 代码一起使用，反之亦然。在这篇文章中，我们将了解如何在 Kotlin 中与 Java 代码进行互操作，以及它提供的一些好处。

## 从 Kotlin 调用 Java 代码

最常见的场景之一是从 Kotlin 调用 Java 代码。这通常很简单，因为 Kotlin 旨在与 Java 很好地协同工作。

例如，假设我们有一个这样的 Java 类：

```java
public class MyJavaClass {
    public static void doSomething() {
        System.out.println("Doing something in Java!");
    }
}
```

我们可以像这样从 Kotlin 调用 `doSomething` 方法：

```kotlin
MyJavaClass.doSomething()
```

Kotlin 还可以轻松调用使用泛型的 Java 代码。例如，假设我们有这样一个 Java 方法：

```java
public static <T> T getValue(T defaultValue) {
    return defaultValue;
}
```

我们可以像这样从 Kotlin 调用这个方法：

```kotlin
val result = getValue("Hello, world!")
```

Kotlin 还支持 Java 的可变参数特性，它允许一个方法接受可变数量的参数。例如，假设我们有这样一个 Java 方法：

```java
public static void printValues(String... values) {
    for (String value : values) {
        System.out.println(value);
    }
}
```

我们可以像这样从 Kotlin 调用这个方法：

```kotlin
printValues("Hello", "world", "!")
```

## 从 Java 调用 Kotlin 代码

也可以从 Java 调用 Kotlin 代码。 Kotlin 代码被编译为 Java 字节码，因此它可以像任何其他 Java 代码一样使用。

例如，假设我们有一个这样的 Kotlin 类：

```kotlin
class MyKotlinClass {
    fun doSomething() {
        println("Doing something in Kotlin!")
    }
}
```

我们可以像这样从 Java 中调用 `doSomething` 方法：

```java
MyKotlinClass kotlinClass = new MyKotlinClass();
kotlinClass.doSomething();
```

Kotlin 还支持泛型、null 安全和 lambda 等功能，这些功能可以从 Java 调用。

## 互操作性的好处

Kotlin 和 Java 之间的互操作性有很多好处。

最大的好处之一是它允许开发人员慢慢地从 Java 迁移到 Kotlin，而不必重写他们的整个代码库。对于具有大量遗留 Java 代码的项目来说，这可能是一个很大的优势。

另一个好处是它允许开发人员使用两种语言中最好的。 Kotlin 和 Java 有许多相似的特性，但也有一些关键的区别。通过使用这两种语言，开发人员可以利用最适合他们需要的每种语言的功能。

## 结论

在本文中，我们了解了 Kotlin 如何与 Java 互操作。我们已经了解了如何从 Java 调用 Kotlin 代码，以及如何从 Kotlin 调用 Java 代码。我们还看到了它提供的一些好处。

如果您有兴趣了解有关 Kotlin 的更多信息，请查看以下资源。

## 附加信息

* [面向 Java 开发人员的 Kotlin](https://kotlinlang.org/docs/reference/java-to-kotlin-interop.html)
* [Java 互操作](https://kotlinlang.org/docs/reference/java-interop.html)