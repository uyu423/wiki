---
title: 028：Kotlin 中的中缀函数：像运算符一样调用函数
description: 
published: true
date: 2023-02-01T17:23:30.396Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:23:28.882Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [028: Infix Functions in Kotlin: Calling Functions Like Operators***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/028-infix-functions-in-kotlin-calling-functions-like-operators)
{.links-list}



#028：Kotlin 中的中缀函数：像运算符一样调用函数
Kotlin 是一种用于 JVM、Android 和浏览器的静态类型编程语言。它以其互操作性、安全性、工具支持和简洁的语法而闻名。

Kotlin 具有许多使其独一无二且对开发人员具有吸引力的特性，其中之一就是中缀函数。

中缀函数是可以在不使用通常的点符号的情况下调用的函数。这意味着它们可以像运算符一样被调用，这可以使代码更加简洁和可读。

中缀函数标有 infix 关键字。它们必须是成员函数或扩展函数。它们只能有一个参数。

这是中缀函数的一个简单示例：

```kotlin
infix fun Int.times(str: String) = str.repeat(this)

println(2 times "Bye ") // Prints "Bye Bye "
```

在上面的示例中，使用 `2` 和 `"Bye"` 参数调用 `times` 函数。 `times` 函数返回字符串 `"Bye "` 重复了 `2` 次。

中缀函数对于提高代码的可读性非常有用。例如，`+` 运算符通常用于连接字符串。但是，它也可以用于添加。这可能会让不熟悉 Kotlin 的开发人员感到困惑。

使用中缀函数，我们可以定义我们自己的 `+` 运算符来进行字符串连接，这可以使我们的代码更具可读性：

```kotlin
infix fun String.plus(str: String) = this + str

println("Hello" plus " world") // Prints "Hello world"
```

在上面的示例中，我们定义了一个用于字符串连接的中缀函数。我们现在可以使用 `+` 运算符连接两个字符串。这可以使我们的代码更具可读性和简洁性。

中缀函数也可以用于比较。例如，我们可以使用 compareTo 函数来比较两个字符串：

```kotlin
infix fun String.compareTo(str: String) = this.compareTo(str)

println("a" compareTo "b") // Prints -1
println("b" compareTo "a") // Prints 1
println("a" compareTo "a") // Prints 0
```

在上面的例子中，我们定义了一个用于字符串比较的中缀函数。我们现在可以使用 compareTo 函数来比较两个字符串。这可以使我们的代码更具可读性和简洁性。

中缀函数是一个强大的工具，可以使 Kotlin 代码更具可读性和简洁性。但是，应谨慎使用它们，因为如果过度使用它们会降低代码的可读性。