---
title: 030：Kotlin 中的字符串模板：使用表达式插入字符串
description: 
published: true
date: 2023-02-01T05:04:48.165Z
tags: 
editor: markdown
dateCreated: 2023-02-01T05:04:46.539Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [030: String Templates in Kotlin: Interpolating Strings with Expressions***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/030-string-templates-in-kotlin-interpolating-strings-with-expressions)
{.links-list}




# Kotlin 中的字符串模板：使用表达式插入字符串

Kotlin 的字符串模板提供了一种在字符串中插入表达式的简单方便的方法。当您需要向字符串中插入动态内容（例如用户名或当前日期）时，这会很有用。

字符串模板以美元符号“$”开头，后跟花括号“{}”中的表达式。表达式可以是任何有效的 Kotlin 代码，它将被计算并将其结果插入到字符串中。

例如，以下字符串模板：

```kotlin
val name = "John"
println("Hello, $name!")
```

将打印“你好，约翰！”。

您还可以使用字符串模板插入函数调用的结果：

```kotlin
fun getCurrentDate(): String {
    // ...
}

println("Today is $getCurrentDate().")
```

如果表达式是一个复杂的表达式，你可以使用 `$` 字符来访问它的成员：

```kotlin
data class User(val name: String, val age: Int)

val user = User("John", 30)
println("User $user.name is $user.age years old.")
```

这将打印 `User John is 30 years old.`。

您还可以使用字符串模板插入函数调用的结果：

```kotlin
fun getCurrentDate(): String {
    // ...
}

println("Today is $getCurrentDate().")
```

如果表达式是一个复杂的表达式，你可以使用 `$` 字符来访问它的成员：

```kotlin
data class User(val name: String, val age: Int)

val user = User("John", 30)
println("User $user.name is $user.age years old.")
```

这将打印 `User John is 30 years old.`。

您还可以使用 `${}` 语法来插入一个复杂的表达式：

```kotlin
data class User(val name: String, val age: Int)

val user = User("John", 30)
println("User ${user.name} is ${user.age} years old.")
```

这相当于前面的例子。

## 转义大括号

如果需要在字符串模板中插入字面值 `$` 或 `{` 字符，可以使用反斜杠 `\` 将其转义：

```kotlin
println("\${5 + 5}") // prints ${5 + 5}
println("\$5 + 5") // prints $5 + 5
```

如果需要插入反斜杠字符，可以使用另一个反斜杠对其进行转义：

```kotlin
println("\\") // prints \
```

## 修剪空白

默认情况下，字符串模板会保留内插表达式中的任何前导或尾随空格。如果要删除此空格，可以使用 `trimIndent()` 或 `trimMargin()` 方法：

```kotlin
val text = """
    |Lorem ipsum dolor sit amet,
    |consectetur adipiscing elit.
    |""".trimMargin()

println(text) // prints Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

`trimIndent()` 方法删除所有前导空白，而 `trimMargin()` 方法删除所有前导空白，直到每行的第一个非空白字符。在上面的例子中，这个字符是`|`。

## 安全通话

如果您在字符串模板中插入可为 null 的表达式，Kotlin 将自动插入一个安全调用 `?.` 以防止出现 NullPointerException：

```kotlin
fun getUserName(): String? {
    // ...
}

println("User name is ${getUserName()}.")
```

这将打印 `User name is null.` 如果 `getUserName()` 函数返回 `null`。

## 非空断言

如果您确定表达式不为“null”，则可以使用非空断言运算符“!!”来禁用安全调用：

```kotlin
fun getUserName(): String? {
    // ...
}

println("User name is ${getUserName()!!}.")
```

这将打印 `User name is null.` 如果 `getUserName()` 函数返回 `null`。

## 结论

Kotlin 的字符串模板提供了一种在字符串中插入表达式的简单方便的方法。当您需要向字符串中插入动态内容（例如用户名或当前日期）时，这会很有用。