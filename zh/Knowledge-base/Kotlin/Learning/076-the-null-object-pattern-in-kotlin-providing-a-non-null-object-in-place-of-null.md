---
title: 076：Kotlin 中的空对象模式：提供非空对象代替空对象
description: 
published: true
date: 2023-02-17T05:32:33.308Z
tags: 
editor: markdown
dateCreated: 2023-02-17T05:32:25.016Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [076: The Null Object Pattern in Kotlin: Providing a Non-Null Object in Place of Null***English** document is available*](/en/Knowledge-base/Kotlin/Learning/076-the-null-object-pattern-in-kotlin-providing-a-non-null-object-in-place-of-null)
{.links-list}


# Kotlin 中的空对象模式：提供一个非空对象代替空对象

Kotlin 的类型系统旨在消除对空值的需求。但是，有时需要空值，例如在与用 Java 编写的遗留代码交互时。在这些情况下，空对象模式可用于提供非空对象来代替空值。

## 什么是空对象模式？

空对象模式是一种设计模式，旨在消除对空值的需求。它通过提供一个非空对象来代替空值来实现这一点。此非空对象可用于表示值的缺失。

## 空对象模式如何工作？

空对象模式通过创建一个表示值缺失的对象来工作。该对象可用于代替空值。可以为该对象指定一个默认值，例如一个空字符串，或者为它指定一个适合该情况的行为。

## 什么时候应该使用空对象模式？

当需要空值时，应该使用空对象模式，例如在与用 Java 编写的遗留代码进行交互时。

## 空对象模式有什么好处？

空对象模式有几个好处：

- 它消除了对空值的需要。
- 它使代码更具可读性。
- 它使代码更易于维护。
- 它使代码更具可扩展性。

## 空对象模式的缺点是什么？

空对象模式有一个缺点：

- 它可以增加代码的复杂性。

## 科特林实现

可以使用以下步骤在 Kotlin 中实现空对象模式：

1.为对象创建一个接口。
2. 创建一个实现该接口的类。
3. 创建一个表示值缺失的对象。

### 第一步：为对象创建接口

第一步是为对象创建一个接口。该接口将定义对象的契约。

```kotlin
interface MyInterface {
    fun doSomething()
}
```

### 第二步：创建一个实现接口的类

第二步是创建一个实现接口的类。此类将提供对象的实现。

```kotlin
class MyClass : MyInterface {
    override fun doSomething() {
        // do something
    }
}
```

### 第 3 步：创建一个表示值缺失的对象

第三步是创建一个表示值缺失的对象。该对象可用于代替空值。

```kotlin
object MyObject : MyInterface {
    override fun doSomething() {
        // do something
    }
}
```

## 用法

空对象模式可以按如下方式使用：

```kotlin
fun doSomething(myInterface: MyInterface?) {
    if (myInterface != null) {
        myInterface.doSomething()
    }
}

fun main() {
    val myClass: MyClass? = MyClass()
    val myObject: MyObject? = MyObject()

    doSomething(myClass)
    doSomething(myObject)
}
```

## 附加信息

- 空对象模式也称为虚拟对象模式。

## 警告

- 只有在需要空值时才应使用空对象模式。

## 危险

- 空对象模式会增加代码的复杂性。