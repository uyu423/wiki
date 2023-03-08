---
title: 003：Kotlin 基础知识：变量、数据类型和运算符
description: 
published: true
date: 2023-02-07T19:56:03.026Z
tags: 
editor: markdown
dateCreated: 2023-02-07T19:55:57.043Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [003: Kotlin Basics: Variables, Data Types, and Operators***English** document is available*](/en/Knowledge-base/Kotlin/Learning/003-kotlin-basics-variables-data-types-and-operators)
{.links-list}


# Kotlin 基础知识：变量、数据类型和运算符

Kotlin 是一种在 JVM 上运行的静态类型编程语言。它是一种简洁、安全、可互操作且工具友好的语言。

Kotlin 是一种面向对象的语言，因此变量必须在使用前声明。在 Kotlin 中，有两种类型的变量：

* 可变变量：这些变量在初始化后可以更改。要声明可变变量，请使用 ```var``` 关键字。
```kotlin
var name = "John"
name = "Jane" // Valid
```

* 不可变变量：这些变量在初始化后不能更改。要声明一个不可变变量，请使用 ```val``` 关键字。
```kotlin
val name = "John"
name = "Jane" // Invalid
```

Kotlin 具有空安全功能，可消除空指针异常的风险。要允许变量保存空值，您需要使用 ```?``` 符号将其声明为可为空。

```kotlin
var name: String? = null
```

Kotlin 还有一组丰富的可用于变量的运算符。这些包括：

* 算术运算符：```+```, ```-```, ``*```, ```/```, ```%```
* 赋值运算符：```=```, ```+=```, ```-=```, ```*=```, ```/=```, `` `%=```
* 比较运算符：```==```, ```!=```, ```>```, ```<```, ```>=```, ``` <=```
* 逻辑运算符：```&&```, ```||```, ```!```

现在您已经了解了 Kotlin 变量和运算符的基础知识，让我们继续学习数据类型。

## Kotlin 数据类型

Kotlin 具有以下数据类型：

* 数字：Kotlin 支持整数和浮点数。
* 字符：Kotlin 字符由 ```Char``` 类型表示。
* 布尔值：Kotlin 布尔值由 ```Boolean``` 类型表示。
* 数组：Kotlin 数组由 ```Array``` 类型表示。
* 字符串：Kotlin 字符串由 ```String``` 类型表示。

除了上述数据类型，Kotlin 还有一种特殊的类型叫做 ```Unit```。此类型用于表示 void 值。

现在您了解了 Kotlin 数据类型的基础知识，让我们继续学习 Kotlin 运算符。

## Kotlin 运算符

Kotlin 有一组丰富的可用于变量的运算符。这些包括：

* 算术运算符：```+```, ```-```, ``*```, ```/```, ```%```
* 赋值运算符：```=```, ```+=```, ```-=```, ```*=```, ```/=```, `` `%=```
* 比较运算符：```==```, ```!=```, ```>```, ```<```, ```>=```, ``` <=```
* 逻辑运算符：```&&```, ```||```, ```!```

现在您已经了解了 Kotlin 运算符的基础知识，让我们继续学习 Kotlin 控制流。

## Kotlin 控制流程

Kotlin 具有以下控制流结构：

* ```if``` 表达式：用于评估布尔表达式并在表达式为 ```true``` 时执行代码块。
* ```if-else``` 表达式：用于评估布尔表达式并执行两个代码块之一，具体取决于表达式是 ```true``` 还是 ```false```。
* ```when``` 表达式：用于评估表达式并根据表达式的值执行多个代码块之一。
* ```for``` 循环：用于执行一段代码固定次数。
* ```while``` 循环：用于多次执行一段代码，直到满足条件。
* ```do-while``` 循环：用于多次执行一段代码，直到满足条件。 ```while``` 循环和```do-while``` 循环之间的区别在于```do-while``` 循环总是至少执行一次代码块。

现在您了解了 Kotlin 控制流的基础知识，让我们继续学习 Kotlin 函数。

## 科特林函数

函数是接受一个或多个输入参数并产生输出的代码块。在 Kotlin 中，函数是使用“fun”关键字声明的。

这是一个简单的函数，它接受两个输入参数并返回这些参数的总和：

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

如果函数不返回值，则其返回类型应声明为 ```Unit```。

这是一个简单的函数，它接受两个输入参数并打印这些参数的总和：

```kotlin
fun sum(a: Int, b: Int): Unit {
    println(a + b)
}
```

Kotlin 还支持高阶函数，也就是将其他函数作为输入参数的函数。高阶函数可用于创建简洁易读的代码。

这是一个简单的高阶函数，它将一个函数作为输入并执行该函数：

```kotlin
fun execute(f: () -> Unit) {
    f()
}
```

上面的 ```execute``` 函数可用于执行任何不接受任何输入参数且不返回值的函数。

现在您了解了 Kotlin 函数的基础知识，让我们继续学习 Kotlin 类和对象。

## Kotlin 类和对象

在 Kotlin 中，类是用于创建对象的模板。一个类可以有属性和方法。

这是一个简单的 ```Person``` 类，有两个属性：```name``` 和 ```age```。

```kotlin
class Person(val name: String, val age: Int)
```

要从类创建对象，您需要使用 ```new``` 关键字。

```kotlin
val person = new Person("John", 30)
```

Kotlin 还支持面向对象编程。在 Kotlin 中，一个对象是一个单例——一个对象只能有一个实例。

这是一个简单的 ```Logger``` 对象，带有 ```log()``` 方法。

```kotlin
object Logger {
    fun log(message: String) {
        println(message)
    }
}
```

要使用 ```Logger``` 对象，您不需要创建它的实例。您可以直接调用 ```log()``` 方法。

```kotlin
Logger.log("This is a log message")
```

现在您已经了解了 Kotlin 类和对象的基础知识，您可以开始使用 Kotlin 进行编程了！