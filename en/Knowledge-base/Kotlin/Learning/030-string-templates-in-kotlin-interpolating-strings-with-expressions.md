---
title: 030: String Templates in Kotlin: Interpolating Strings with Expressions
description: 
published: true
date: 2023-02-01T05:04:50.358Z
tags: 
editor: markdown
dateCreated: 2023-02-01T05:04:46.507Z
---

- [030: Kotlin의 문자열 템플릿: 표현식으로 문자열 보간***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/030-string-templates-in-kotlin-interpolating-strings-with-expressions)
{.links-list}
- [030: Kotlin の文字列テンプレート: 式による文字列の補間***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/030-string-templates-in-kotlin-interpolating-strings-with-expressions)
{.links-list}
- [030：Kotlin 中的字符串模板：使用表达式插入字符串***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/030-string-templates-in-kotlin-interpolating-strings-with-expressions)
{.links-list}




# String Templates in Kotlin: Interpolating Strings with Expressions

Kotlin's string templates offer a simple and convenient way to interpolate expressions within strings. This can be useful when you need to insert dynamic content into a string, such as a user's name or the current date.

String templates start with a dollar sign `$` followed by an expression in curly braces `{}`. The expression can be any valid Kotlin code, which will be evaluated and its result inserted into the string.

For example, the following string template:

```kotlin
val name = "John"
println("Hello, $name!")
```

will print `Hello, John!`.

You can also use string templates to insert the result of a function call:

```kotlin
fun getCurrentDate(): String {
    // ...
}

println("Today is $getCurrentDate().")
```

If the expression is a complex expression, you can use the `$` character to access its members:

```kotlin
data class User(val name: String, val age: Int)

val user = User("John", 30)
println("User $user.name is $user.age years old.")
```

This will print `User John is 30 years old.`.

You can also use string templates to insert the result of a function call:

```kotlin
fun getCurrentDate(): String {
    // ...
}

println("Today is $getCurrentDate().")
```

If the expression is a complex expression, you can use the `$` character to access its members:

```kotlin
data class User(val name: String, val age: Int)

val user = User("John", 30)
println("User $user.name is $user.age years old.")
```

This will print `User John is 30 years old.`.

You can also use the `${}` syntax to interpolate a complex expression:

```kotlin
data class User(val name: String, val age: Int)

val user = User("John", 30)
println("User ${user.name} is ${user.age} years old.")
```

This is equivalent to the previous example.

## Escaping Curly Braces

If you need to insert a literal `$` or `{` character in a string template, you can escape it with a backslash `\`:

```kotlin
println("\${5 + 5}") // prints ${5 + 5}
println("\$5 + 5") // prints $5 + 5
```

If you need to insert a backslash character, you can escape it with another backslash:

```kotlin
println("\\") // prints \
```

## Trimming White Space

By default, string templates preserve any leading or trailing whitespace in the interpolated expression. If you want to remove this whitespace, you can use the `trimIndent()` or `trimMargin()` methods:

```kotlin
val text = """
    |Lorem ipsum dolor sit amet,
    |consectetur adipiscing elit.
    |""".trimMargin()

println(text) // prints Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

The `trimIndent()` method removes all leading whitespace, while the `trimMargin()` method removes all leading whitespace up to the first non-whitespace character on each line. In the example above, this character is `|`.

## Safe Calls

If you interpolate a nullable expression in a string template, Kotlin will automatically insert a safe call `?.` to prevent a NullPointerException:

```kotlin
fun getUserName(): String? {
    // ...
}

println("User name is ${getUserName()}.")
```

This will print `User name is null.` if the `getUserName()` function returns `null`.

## Non-Null Assertions

If you are sure that an expression is not `null`, you can use the non-null assertion operator `!!` to disable the safe call:

```kotlin
fun getUserName(): String? {
    // ...
}

println("User name is ${getUserName()!!}.")
```

This will print `User name is null.` if the `getUserName()` function returns `null`.

## Conclusion

Kotlin's string templates offer a simple and convenient way to interpolate expressions within strings. This can be useful when you need to insert dynamic content into a string, such as a user's name or the current date.