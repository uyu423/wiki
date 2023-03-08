---
title: 051: The Kotlin Standard Library: Utilizing the Built-in Functions and Classes
description: 
published: true
date: 2023-02-16T17:33:15.896Z
tags: 
editor: markdown
dateCreated: 2023-02-16T17:33:07.861Z
---

- [051: La biblioteca estándar de Kotlin: uso de las funciones y clases integradas***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/051-the-kotlin-standard-library-utilizing-the-built-in-functions-and-classes)
{.links-list}
- [051：Kotlin 标准库：使用内置函数和类***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/051-the-kotlin-standard-library-utilizing-the-built-in-functions-and-classes)
{.links-list}
- [051: Kotlin 표준 라이브러리: 내장 함수 및 클래스 활용***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/051-the-kotlin-standard-library-utilizing-the-built-in-functions-and-classes)
{.links-list}


# The Kotlin Standard Library: Utilizing the Built-in Functions and Classes

Kotlin is a powerful programming language that runs on the Java Virtual Machine. It is a statically typed language that combines both object-oriented and functional programming features. Kotlin is known for its interoperability with Java, making it a great choice for developing Android applications.

One of the Kotlin's most appealing features is its Standard Library, which contains a rich set of functions and classes that can be used in your Kotlin code. In this post, we'll take a look at some of the most useful functions and classes in the Kotlin Standard Library.

## Kotlin Collections

Kotlin collections are immutable by default, which means that they cannot be modified once they are created. This is a great feature because it helps to avoid bugs that can occur when modifying data structures. Kotlin also provides many useful functions for working with collections, such as `filter`, `map`, and `reduce`.

Let's say we have a list of numbers and we want to filter out the even numbers. We can do this with the `filter` function:

```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

val evenNumbers = numbers.filter { it % 2 == 0 }

println(evenNumbers) // prints [2, 4, 6, 8, 10]
```

We can also use the `map` function to transform the elements in a collection. For example, if we have a list of strings and we want to convert them to uppercase, we can use the `map` function:

```kotlin
val strings = listOf("a", "b", "c", "d", "e")

val uppercaseStrings = strings.map { it.toUpperCase() }

println(uppercaseStrings) // prints [A, B, C, D, E]
```

Finally, the `reduce` function can be used to combine the elements in a collection into a single value. For example, if we have a list of numbers and we want to calculate the sum of all the numbers, we can use the `reduce` function:

```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

val sum = numbers.reduce { a, b -> a + b }

println(sum) // prints 55
```

These are just a few of the useful functions that are available for working with Kotlin collections. For a complete list of functions, see the [Kotlin Standard Library documentation](https://kotlinlang.org/api/latest/jvm/stdlib/index.html).

## Kotlin Strings

Kotlin provides many useful functions for working with strings. For example, the `trim` function can be used to remove leading and trailing whitespace from a string:

```kotlin
val s = "  hello world!  "

val trimmedString = s.trim()

println(trimmedString) // prints "hello world!"
```

The `split` function can be used to split a string into a list of substrings, using a specified delimiter:

```kotlin
val s = "a,b,c,d,e"

val substrings = s.split(",")

println(substrings) // prints ["a", "b", "c", "d", "e"]
```

The `replace` function can be used to replace all occurrences of a specified string with another string:

```kotlin
val s = "hello world"

val replacedString = s.replace("hello", "goodbye")

println(replacedString) // prints "goodbye world"
```

These are just a few of the useful functions that are available for working with Kotlin strings. For a complete list of functions, see the [Kotlin Standard Library documentation](https://kotlinlang.org/api/latest/jvm/stdlib/index.html).

## Kotlin Math

The Kotlin Standard Library also provides some basic math functions. For example, the `abs` function can be used to calculate the absolute value of a number:

```kotlin
val x = -10

val absoluteValue = kotlin.math.abs(x)

println(absoluteValue) // prints 10
```

The `max` and `min` functions can be used to calculate the maximum and minimum of two numbers, respectively:

```kotlin
val x = 10
val y = 20

val maximum = kotlin.math.max(x, y)
val minimum = kotlin.math.min(x, y)

println(maximum) // prints 20
println(minimum) // prints 10
```

Finally, the `pow` function can be used to calculate a number raised to a specified power:

```kotlin
val x = 2.0
val y = 10

val xToTheY = kotlin.math.pow(x, y)

println(xToTheY) // prints 1024.0
```

These are just a few of the useful functions that are available for working with Kotlin math. For a complete list of functions, see the [Kotlin Standard Library documentation](https://kotlinlang.org/api/latest/jvm/stdlib/index.html).

## Kotlin Dates and Times

Kotlin provides a comprehensive set of functions and classes for working with dates and times. For example, the `now` function can be used to get the current date and time:

```kotlin
val now = LocalDateTime.now()

println(now) // prints 2020-03-27T12:34:56.789
```

The `parse` function can be used to parse a string into a `LocalDate` object:

```kotlin
val dateString = "2020-03-27"

val date = LocalDate.parse(dateString)

println(date) // prints 2020-03-27
```

The `plusDays` function can be used to add a specified number of days to a `LocalDate` object:

```kotlin
val date = LocalDate.now()

val tomorrow = date.plusDays(1)

println(tomorrow) // prints 2020-03-28
```

These are just a few of the useful functions that are available for working with Kotlin dates and times. For a complete list of functions, see the [Kotlin Standard Library documentation](https://kotlinlang.org/api/latest/jvm/stdlib/index.html).

## Conclusion

In this post, we've taken a look at some of the most useful functions and classes in the Kotlin Standard Library. We've seen how Kotlin collections can be filtered, mapped, and reduced; how Kotlin strings can be trimmed, split, and replaced; and how Kotlin math functions can be used to calculate the absolute value, maximum, minimum, and power of numbers. We've also seen how Kotlin dates and times can be parsed, formatted, and manipulated.

For more information on the Kotlin Standard Library, be sure to check out the [Kotlin Standard Library documentation](https://kotlinlang.org/api/latest/jvm/stdlib/index.html).