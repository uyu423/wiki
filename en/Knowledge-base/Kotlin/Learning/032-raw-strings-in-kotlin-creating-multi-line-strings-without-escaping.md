---
title: 032: Raw Strings in Kotlin: Creating Multi-Line Strings Without Escaping
description: 
published: true
date: 2023-02-01T07:43:35.343Z
tags: 
editor: markdown
dateCreated: 2023-02-01T07:43:33.908Z
---

- [032: Kotlin의 원시 문자열: 이스케이프 없이 여러 줄 문자열 만들기***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/032-raw-strings-in-kotlin-creating-multi-line-strings-without-escaping)
{.links-list}
- [032：Kotlin 中的原始字符串：在不转义的情况下创建多行字符串***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/032-raw-strings-in-kotlin-creating-multi-line-strings-without-escaping)
{.links-list}


# 032: Raw Strings in Kotlin: Creating Multi-Line Strings Without Escaping

Kotlin's raw strings are useful when you need to create strings that contain multiple lines of text. Raw strings are enclosed in triple quotes (""") and can span multiple lines of text.

Unlike regular strings, raw strings can contain any character, including newlines and quotes. This makes them ideal for creating strings that contain multiple lines of text.

To create a raw string, simply enclose the string in triple quotes. For example:

```kotlin
val rawString = """
    This is a raw string.
    It can span multiple lines.
    It can contain any character, including newlines and quotes.
""".trimIndent()
```

As you can see, the raw string contains multiple lines of text. It also contains quotes (") and newlines.

The raw string above is assigned to the variable `rawString`. We can print the contents of this variable to the console:

```kotlin
println(rawString)
```

This will print the following to the console:

```
This is a raw string.
It can span multiple lines.
It can contain any character, including newlines and quotes.
```

As you can see, the raw string contains all of the text, including the newlines and quotes.

If we had used a regular string, the newlines and quotes would have been escaped and would have appeared as follows:

```
This is a raw string.\nIt can span multiple lines.\nIt can contain any character, including newlines and quotes.
```

As you can see, the newlines and quotes are escaped with backslashes. This is because regular strings treat newlines and quotes as special characters.

Raw strings, on the other hand, treat all characters as literal. This makes them ideal for creating strings that contain multiple lines of text.

There are a few things to keep in mind when working with raw strings. First, all leading and trailing whitespace is preserved. This includes newlines, spaces, and tabs.

Second, raw strings can't be interpolated. This means that you can't use string templates or variables inside of a raw string. For example, the following code will not compile:

```kotlin
val name = "John"
val rawString = """
    Hello, $name!
""".trimIndent()
```

If you need to interpolate a string, you must use a regular string.

Third, raw strings can't be concatenated. This means that you can't use the `+` operator to concatenate raw strings. For example, the following code will not compile:

```kotlin
val rawString1 = """
    This is a raw string.
""".trimIndent()

val rawString2 = """
    It can span multiple lines.
""".trimIndent()

val rawString = rawString1 + rawString2
```

If you need to concatenate raw strings, you must use the `trimMargin()` or `trimIndent()` methods. For example:

```kotlin
val rawString1 = """
    |This is a raw string.
""".trimMargin()

val rawString2 = """
    |It can span multiple lines.
""".trimMargin()

val rawString = rawString1 + rawString2
```

The `trimMargin()` method removes all leading whitespace, including newlines, spaces, and tabs. The `trimIndent()` method is similar, but it only removes leading whitespace on the first line.

Fourth, raw strings can be converted to regular strings using the `toString()` method. For example:

```kotlin
val rawString = """
    This is a raw string.
    It can span multiple lines.
    It can contain any character, including newlines and quotes.
""".trimIndent()

val regularString = rawString.toString()
```

The `toString()` method returns a regular string. This string can be interpolated and concatenated.

Finally, raw strings can be converted to byte arrays using the `toByteArray()` method. For example:

```kotlin
val rawString = """
    This is a raw string.
    It can span multiple lines.
    It can contain any character, including newlines and quotes.
""".trimIndent()

val byteArray = rawString.toByteArray()
```

The `toByteArray()` method returns a byte array. This byte array can be used to create a regular string.

Raw strings are a powerful feature of Kotlin. They are especially useful for creating strings that contain multiple lines of text.