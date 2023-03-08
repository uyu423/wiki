---
title: 032：Kotlin 中的原始字符串：在不转义的情况下创建多行字符串
description: 
published: true
date: 2023-02-01T07:43:37.380Z
tags: 
editor: markdown
dateCreated: 2023-02-01T07:43:33.911Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [032: Raw Strings in Kotlin: Creating Multi-Line Strings Without Escaping***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/032-raw-strings-in-kotlin-creating-multi-line-strings-without-escaping)
{.links-list}


# 032：Kotlin 中的原始字符串：在不转义的情况下创建多行字符串

当您需要创建包含多行文本的字符串时，Kotlin 的原始字符串很有用。原始字符串用三重引号 (""") 括起来，可以跨越多行文本。

与常规字符串不同，原始字符串可以包含任何字符，包括换行符和引号。这使它们非常适合创建包含多行文本的字符串。

要创建原始字符串，只需将字符串括在三重引号中即可。例如：

```kotlin
val rawString = """
    This is a raw string.
    It can span multiple lines.
    It can contain any character, including newlines and quotes.
""".trimIndent()
```

如您所见，原始字符串包含多行文本。它还包含引号 (") 和换行符。

上面的原始字符串被分配给变量“rawString”。我们可以将这个变量的内容打印到控制台：

```kotlin
println(rawString)
```

这会将以下内容打印到控制台：

```
This is a raw string.
It can span multiple lines.
It can contain any character, including newlines and quotes.
```

如您所见，原始字符串包含所有文本，包括换行符和引号。

如果我们使用常规字符串，换行符和引号将被转义并显示如下：

```
This is a raw string.\nIt can span multiple lines.\nIt can contain any character, including newlines and quotes.
```

如您所见，换行符和引号用反斜杠转义。这是因为常规字符串将换行符和引号视为特殊字符。

另一方面，原始字符串将所有字符都视为文字。这使它们非常适合创建包含多行文本的字符串。

使用原始字符串时需要记住一些事项。首先，保留所有前导和尾随空格。这包括换行符、空格和制表符。

其次，无法对原始字符串进行插值。这意味着您不能在原始字符串中使用字符串模板或变量。例如，下面的代码将不会编译：

```kotlin
val name = "John"
val rawString = """
    Hello, $name!
""".trimIndent()
```

如果需要插入字符串，则必须使用常规字符串。

第三，无法连接原始字符串。这意味着您不能使用 `+` 运算符连接原始字符串。例如，下面的代码将不会编译：

```kotlin
val rawString1 = """
    This is a raw string.
""".trimIndent()

val rawString2 = """
    It can span multiple lines.
""".trimIndent()

val rawString = rawString1 + rawString2
```

如果您需要连接原始字符串，则必须使用 `trimMargin()` 或 `trimIndent()` 方法。例如：

```kotlin
val rawString1 = """
    |This is a raw string.
""".trimMargin()

val rawString2 = """
    |It can span multiple lines.
""".trimMargin()

val rawString = rawString1 + rawString2
```

`trimMargin()` 方法删除所有前导空格，包括换行符、空格和制表符。 `trimIndent()` 方法类似，但它只删除第一行的前导空格。

第四，可以使用 `toString()` 方法将原始字符串转换为常规字符串。例如：

```kotlin
val rawString = """
    This is a raw string.
    It can span multiple lines.
    It can contain any character, including newlines and quotes.
""".trimIndent()

val regularString = rawString.toString()
```

`toString()` 方法返回一个常规字符串。这个字符串可以被插入和连接。

最后，可以使用“toByteArray()”方法将原始字符串转换为字节数组。例如：

```kotlin
val rawString = """
    This is a raw string.
    It can span multiple lines.
    It can contain any character, including newlines and quotes.
""".trimIndent()

val byteArray = rawString.toByteArray()
```

`toByteArray()` 方法返回一个字节数组。此字节数组可用于创建常规字符串。

原始字符串是 Kotlin 的一个强大功能。它们对于创建包含多行文本的字符串特别有用。