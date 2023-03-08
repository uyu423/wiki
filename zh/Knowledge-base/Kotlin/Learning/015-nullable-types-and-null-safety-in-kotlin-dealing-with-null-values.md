---
title: 015：Kotlin 中的可空类型和空安全：处理空值
description: 
published: true
date: 2023-02-16T04:32:56.450Z
tags: 
editor: markdown
dateCreated: 2023-02-16T04:32:54.821Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [015: Nullable Types and Null Safety in Kotlin: Dealing with Null Values***English** document is available*](/en/Knowledge-base/Kotlin/Learning/015-nullable-types-and-null-safety-in-kotlin-dealing-with-null-values)
{.links-list}


## 介绍

Kotlin 是一种在 Java 虚拟机上运行的静态类型编程语言。它是一种通用语言，旨在简洁、安全和可互操作。

Kotlin 的关键特性之一是空安全。空安全是一种防止空指针异常的机制。 Kotlin 的类型系统旨在消除代码中出现空引用的可能性。

可空类型是一种表示可以为空的类型的方式。在 Kotlin 中，默认情况下所有类型都是不可空的。这意味着非空类型的变量不能包含空值。

要创建可空类型，我们在类型名称后使用问号 (?)。例如，以下代码定义了一个可为 null 的字符串变量：

```kotlin
var str: String? = "Hello"
```

现在，str 变量可以保存字符串值或空值。

如果我们试图将一个空值赋给一个非空类型的变量，我们将得到一个编译错误：

```kotlin
var str: String = "Hello"
str = null // error: null can not be a value of a non-null type String
```

要解决此问题，我们可以将 str 变量的类型更改为可空类型或使用非空断言。非空断言是一个运算符，它告诉编译器变量不为空。我们这样使用它：

```kotlin
var str: String = "Hello"
str = null // error: null can not be a value of a non-null type String

str!!.length // non-null assertion
```

非空断言运算符是双感叹号 (!!)。仅当我们确定变量不为空时才应使用它。否则，我们将得到一个运行时异常。

## 检查是否为空

在 Kotlin 中，我们可以使用 isNullOrEmpty() 函数检查变量是否为空：

```kotlin
fun main() {
    var str: String? = "Hello"
    if (str.isNullOrEmpty()) {
        println("str is null or empty")
    } else {
        println(str.length)
    }
}
```

如果字符串为 null 或空，则 isNullOrEmpty() 函数返回 true。否则，它返回 false。

我们还可以使用 `?` 运算符来检查变量是否为空：

```kotlin
fun main() {
    var str: String? = "Hello"
    val length = str?.length // str is not null, so length is not null
    println(length)
}
```

`?` 运算符称为安全调用运算符。它在调用 length 属性之前检查变量是否为 null。如果变量为 null，则返回 null。否则，它返回字符串的长度。

我们可以使用 `?` 运算符在可空变量上调用函数：

```kotlin
fun main() {
    var str: String? = "Hello"
    str?.let {
        println(it.length) // it is not null, so we can call the length property
    }
}
```

`let` 函数是一个以 lambda 作为参数的高阶函数。 lambda 仅在变量不为空时执行。

如果变量不为空，我们还可以使用 `?` 运算符来执行代码块：

```kotlin
fun main() {
    var str: String? = "Hello"
    str?.let {
        println(it.length) // it is not null, so we can call the length property
    }
}
```

`?` 运算符称为安全调用运算符。它在执行 lambda 之前检查变量是否为 null。如果变量为 null，则它不执行任何操作。否则，它执行 lambda。

## 猫王运算符

Elvis 运算符是一种将默认值分配给可空变量的方法。我们这样使用它：

```kotlin
fun main() {
    var str: String? = "Hello"
    val length = str?.length ?: 0 // if str is null, length is 0
    println(length)
}
```

如果 `str` 变量为 null，则 `length` 变量被赋予值 0。否则，它被赋予 `str.length` 的值。

Elvis 运算符通常与 let 函数一起使用：

```kotlin
fun main() {
    var str: String? = "Hello"
    str?.let {
        println(it.length) // it is not null, so we can call the length property
    } ?: println("str is null") // if str is null, print "str is null"
}
```

如果 str 变量为空，则执行 println("str is null") 语句。否则，将执行 `println(it.length)` 语句。

## 非空断言运算符

非空断言运算符是一种告诉编译器变量不为空的方法。我们这样使用它：

```kotlin
fun main() {
    var str: String? = "Hello"
    str!!.length // str is not null, so we can call the length property
}
```

非空断言运算符是一个双感叹号 (!!)。仅当我们确定变量不为空时才应使用它。否则，我们将得到一个运行时异常。

## 这 ！！操作员

这 ！！运算符是一种告诉编译器变量不为空的方法。我们这样使用它：

```kotlin
fun main() {
    var str: String? = "Hello"
    str!!.length // str is not null, so we can call the length property
}
```

这 ！！运算符是双感叹号 (!!)。仅当我们确定变量不为空时才应使用它。否则，我们将得到一个运行时异常。

## 结论

在本文中，我们了解了 Kotlin 中的空安全性。我们已经了解了如何使用可空类型以及检查空值的不同方法。我们还了解了如何使用 Elvis 运算符和非空断言运算符。