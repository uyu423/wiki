---
title: 011：Kotlin 中的属性和字段：了解 getter 和 setter
description: 
published: true
date: 2023-01-31T05:36:58.404Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:36:54.297Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [011: Properties and Fields in Kotlin: Understanding Getters and Setters***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/011-properties-and-fields-in-kotlin-understanding-getters-and-setters)
{.links-list}


# Kotlin 中的属性和字段：了解 getter 和 setter

在 Kotlin 中，属性和字段可以有自定义的 getter 和 setter。默认情况下，属性和字段具有公共可见性，这意味着可以从类外部访问它们。

## 特性

属性是使用 `val` 关键字声明的。它们是不可变的，这意味着它们只能被分配一次。

```kotlin
val name = "John"
```

在上面的示例中，“name”属性被初始化为值“John”。它不能被重新分配。

## 字段

使用 `var` 关键字声明字段。它们是可变的，这意味着它们可以被重新分配。

```kotlin
var name = "John"
name = "Jane"
```

在上面的例子中，`name` 字段被初始化为值“John”。它可以重新分配给“简”。

## 吸气剂和吸气剂

默认情况下，属性和字段具有公共可见性，这意味着可以从类外部访问它们。但是，我们可以创建自定义的 getter 和 setter 来控制它们的访问方式。

getter 用于检索属性或字段的值。当我们在代码中使用属性或字段时会调用它们。

Setter 用于重新分配属性或字段的值。当我们在代码中重新分配属性或字段时会调用它们。

考虑以下属性：

```kotlin
var name: String = "John"
```

我们可以为该属性创建自定义的 getter 和 setter，如下所示：

```kotlin
var name: String = "John"
    get() {
        return field
    }
    set(value) {
        field = value
    }
```

在上面的示例中，`get()` 函数是 getter，`set(value)` 函数是 setter。 `get()` 函数返回 `name` 字段的值，而 `set(value)` 函数设置 `name` 字段的值。

我们还可以为使用 val 关键字声明的属性和字段创建自定义 getter 和 setter。在这种情况下，我们只能创建一个自定义的 getter。我们无法创建自定义 setter，因为该属性是不可变的。

考虑以下属性：

```kotlin
val name: String = "John"
```

我们可以为这个属性创建一个自定义的 getter，如下所示：

```kotlin
val name: String = "John"
    get() {
        return field
    }
```

在上面的示例中，`get()` 函数是 getter。 `get()` 函数返回 `name` 字段的值。

## 结论

在 Kotlin 中，属性和字段可以有自定义的 getter 和 setter。 getter 用于检索属性或字段的值，setter 用于重新分配属性或字段的值。