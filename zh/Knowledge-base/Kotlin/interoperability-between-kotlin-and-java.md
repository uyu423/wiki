---
title: Kotlin 和 Java 之间的互操作性
description: 
published: true
date: 2023-02-09T08:55:26.174Z
tags: 
editor: markdown
dateCreated: 2023-02-09T08:55:20.014Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Interoperability Between Kotlin and Java***English** document is available*](/en/Knowledge-base/Kotlin/interoperability-between-kotlin-and-java)
{.links-list}



# Kotlin 和 Java 之间的互操作性

Java 和 Kotlin 是用于开发 Android 应用程序的两种流行编程语言。虽然 Kotlin 是一种较新的语言，但它可以与 Java 完全互操作。这意味着您可以在同一个项目中同时使用 Kotlin 和 Java，并且可以从 Java 调用 Kotlin 代码，反之亦然。在本文中，我们将了解 Kotlin 和 Java 如何互操作以及如何在 Android 应用程序开发中使用这两种语言。

## 从 Java 调用 Kotlin

从 Java 调用 Kotlin 是无缝和直接的。您可以从 Java 代码调用任何 Kotlin 代码，反之亦然。无需添加任何特殊注释或配置。

要从 Java 调用 Kotlin 代码，只需使用 Kotlin 类、方法或属性的完全限定名称。例如，要从 Java 调用 `Foo` 类中的 `foo()` 函数，您可以使用以下代码：

```java
FooKt.foo();
```

要从 Kotlin 调用 Java 代码，请使用“@JvmName”注释。此注释允许您指定从 Java 调用时将使用的 Kotlin 函数或属性的名称。例如，以下 Kotlin 代码：

```kotlin
@JvmName("bar")
fun foo() {
    // ...
}
```

可以使用以下代码从 Java 中调用：

```java
FooKt.bar();
```

## 使用可空和非空类型

Kotlin 有可空类型和非空类型，这有助于防止空指针异常。在 Kotlin 中，任何类型都可以通过在类型名称后添加 `?` 来设置为可空。例如，以下 Kotlin 代码定义了一个可为 null 的“String”：

```kotlin
var s: String? = null
```

从 Java 调用 Kotlin 代码时，所有可为 null 的类型都会自动转换为其对应的非 null 类型。例如，以下 Kotlin 代码：

```kotlin
fun foo(s: String?) {
    // ...
}
```

可以使用以下代码从 Java 中调用：

```java
foo("Hello");
```

## 使用 Java 集合

Kotlin 和 Java 使用非常不同的集合方法。在 Kotlin 中，所有集合默认都是不可变的，而在 Java 中它们是可变的。这可能会让习惯于使用 Java 集合的开发人员感到困惑。

幸运的是，Kotlin 提供了在 Kotlin 和 Java 集合之间进行转换的简单方法。要将 Java 集合转换为 Kotlin 集合，您可以使用“toMutableList()”或“toList()”函数。例如，下面的 Java 代码：

```java
List<String> list = Arrays.asList("a", "b", "c");
```

可以使用 `toList()` 函数转换为 Kotlin `List`：

```kotlin
val list = list.toList()
```

要将 Kotlin 集合转换为 Java 集合，您可以使用“toJavaList()”或“toJavaSet()”函数。例如，以下 Kotlin 代码：

```kotlin
val list = listOf("a", "b", "c")
```

可以使用 `toJavaList()` 函数转换为 Java `List`：

```java
List<String> list = list.toJavaList();
```

## 结论

Kotlin 和 Java 是两种完全可互操作的流行编程语言。这意味着您可以在同一个项目中同时使用 Kotlin 和 Java，并且可以从 Java 调用 Kotlin 代码，反之亦然。在本文中，我们了解了 Kotlin 和 Java 如何互操作以及如何在 Android 应用程序开发中使用这两种语言。