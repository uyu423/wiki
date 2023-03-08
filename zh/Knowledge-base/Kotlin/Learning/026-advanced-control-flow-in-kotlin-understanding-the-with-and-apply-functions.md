---
title: 026：Kotlin 中的高级控制流：了解 with 和 apply 函数
description: 
published: true
date: 2023-02-14T06:55:55.415Z
tags: 
editor: markdown
dateCreated: 2023-02-14T06:55:48.273Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [026: Advanced Control Flow in Kotlin: Understanding the with and apply Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/026-advanced-control-flow-in-kotlin-understanding-the-with-and-apply-functions)
{.links-list}


# 026：Kotlin 中的高级控制流：了解 with 和 apply 函数

作为一名 Kotlin 程序员，了解控制程序流程的不同方法非常重要。在本文中，我们将了解两个经常一起使用的函数：with 和 apply。我们将了解何时以及如何使用它们，并且我们将看到一些示例来说明如何使用它们来改进我们的代码。

## 什么是 with 和 apply 函数？

with 和 apply 函数都是将接收者作为参数的函数。接收者是调用函数的对象。 with 函数返回接收者，而 apply 函数返回传递给它的 lambda 的结果。

## 我应该在什么时候使用和申请？

只要您想对同一对象执行多个操作，就可以使用 with 和 apply 函数。它们经常一起使用，因为它们允许您简洁地编写代码，如果您使用常规函数调用，这些代码会更加冗长。

例如，假设我们有一个名为 User 的类，它有几个属性：

```kotlin
class User(
    val name: String,
    val age: Int,
    val address: String
)
```

我们有这个类的一个实例：

```kotlin
val user = User("John", 30, "123 Main Street")
```

我们可以使用 with 函数对用户对象执行多项操作：

```kotlin
with(user) {
    // do something with the user object
}
```

我们还可以使用 apply 函数对用户对象执行多项操作：

```kotlin
user.apply {
    // do something with the user object
}
```

## 使用with和apply的例子

让我们看一些示例，了解如何使用 with 和 apply 来改进我们的代码。

### 1。创建和初始化对象

with 和 apply 的一个常见用例是创建和初始化一个对象。假设我们有一个名为 Car 的类，它具有几个属性：

```kotlin
class Car(
    val make: String,
    val model: String,
    val year: Int,
    val color: String
)
```

我们可以使用 with 创建此类的新实例并初始化其属性：

```kotlin
val car = with(Car("Toyota", "Camry", 2020, "red")) {
    // do something with the car object
}
```

我们还可以使用 apply 创建此类的新实例并初始化其属性：

```kotlin
val car = Car("Toyota", "Camry", 2020, "red").apply {
    // do something with the car object
}
```

### 2。访问和修改属性

with 和 apply 的另一个常见用例是访问和修改对象的属性。假设我们有一个名为 Person 的类，它具有几个属性：

```kotlin
class Person(
    var name: String,
    var age: Int,
    var address: String
)
```

我们有这个类的一个实例：

```kotlin
val person = Person("John", 30, "123 Main Street")
```

我们可以使用 with 访问和修改 person 对象的属性：

```kotlin
with(person) {
    name = "Jane"
    age = 31
    address = "456 Main Street"
}
```

我们还可以使用 apply 来访问和修改 person 对象的属性：

```kotlin
person.apply {
    name = "Jane"
    age = 31
    address = "456 Main Street"
}
```

### 3。在一个对象上调用多个方法

with 和 apply 的另一个常见用例是在同一对象上调用多个方法。假设我们有一个名为 Employee 的类，它有几个方法：

```kotlin
class Employee(
    val name: String,
    val age: Int,
    val address: String
) {
    fun work() {
        // do some work
    }

    fun takeBreak() {
        // take a break
    }

    fun goHome() {
        // go home
    }
}
```

我们有这个类的一个实例：

```kotlin
val employee = Employee("John", 30, "123 Main Street")
```

我们可以使用 with 在 employee 对象上调用多个方法：

```kotlin
with(employee) {
    work()
    takeBreak()
    goHome()
}
```

我们还可以使用 apply 调用 employee 对象的多个方法：

```kotlin
employee.apply {
    work()
    takeBreak()
    goHome()
}
```

## 附加信息

以下是一些额外的资源，可用于了解有关 with 和 apply 函数的更多信息：

- with 函数是在 Kotlin 标准库 [此处](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-with/index.html) 中声明的高阶函数。
- apply 函数是 [此处](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-any/apply.html) 声明的 Any 类的成员函数。
- with 和 apply 函数在 [此处](https://kotlinlang.org/docs/reference/lambdas.html# with-and-apply) 的 Kotlin 文档中进行了描述。

## 结论

在这篇文章中，我们了解了 with 和 apply 函数。我们已经了解了何时以及如何使用它们，并且我们已经看到了一些如何使用它们来改进我们的代码的示例。