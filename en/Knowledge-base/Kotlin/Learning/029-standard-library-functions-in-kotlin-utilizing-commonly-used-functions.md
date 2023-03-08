---
title: 029: Standard Library Functions in Kotlin: Utilizing Commonly Used Functions
description: 
published: true
date: 2023-02-06T17:55:52.682Z
tags: 
editor: markdown
dateCreated: 2023-02-06T17:55:47.018Z
---

- [029: Funciones de biblioteca estándar en Kotlin: uso de funciones de uso común***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/029-standard-library-functions-in-kotlin-utilizing-commonly-used-functions)
{.links-list}
- [029：Kotlin 中的标准库函数：使用常用函数***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/029-standard-library-functions-in-kotlin-utilizing-commonly-used-functions)
{.links-list}
- [029: Kotlin의 표준 라이브러리 함수: 일반적으로 사용되는 함수 활용***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/029-standard-library-functions-in-kotlin-utilizing-commonly-used-functions)
{.links-list}


# 029: Standard Library Functions in Kotlin: Utilizing Commonly Used Functions

Kotlin is a statically typed programming language that runs on the Java Virtual Machine and can also be compiled to JavaScript source code. The Kotlin standard library provides a set of commonly used functions, which are available without any additional dependencies.

In this post, we'll take a look at some of the most commonly used functions in the Kotlin standard library and how to utilize them in your code.

## Collections

Kotlin provides a set of functions for working with collections of data. These functions are available in the ```kotlin.collections``` package.

### Creating Collections

You can create a new collection by using the ```arrayOf()```, ```listOf()```, or ```mutableListOf()``` functions. The ```arrayOf()``` function creates an array of the given elements, the ```listOf()``` function creates a read-only list, and the ```mutableListOf()``` function creates a mutable list.

For example, you can create a new array of strings like this:

```kotlin
val array = arrayOf("a", "b", "c")
```

You can create a new list of integers like this:

```kotlin
val list = listOf(1, 2, 3)
```

And you can create a new mutable list of floats like this:

```kotlin
val mutableList = mutableListOf(1.0f, 2.0f, 3.0f)
```

### Accessing Elements in a Collection

You can access the elements in a collection by using the ```get()``` function. This function takes an ```Int``` index and returns the element at that index.

For example, you can access the first element in an array like this:

```kotlin
val firstElement = array[0]
```

You can access the last element in a list like this:

```kotlin
val lastElement = list[list.size - 1]
```

And you can access the middle element in a mutable list like this:

```kotlin
val middleElement = mutableList[mutableList.size / 2]
```

### Adding and Removing Elements from a Collection

You can add and remove elements from a mutable collection by using the ```add()``` and ```remove()``` functions. The ```add()``` function adds an element to the end of the collection, and the ```remove()``` function removes an element from the collection.

For example, you can add an element to a mutable list like this:

```kotlin
mutableList.add("d")
```

You can remove the first element from a mutable list like this:

```kotlin
mutableList.removeAt(0)
```

And you can remove the last element from a mutable list like this:

```kotlin
mutableList.removeAt(mutableList.size - 1)
```

## Strings

Kotlin provides a set of functions for working with strings. These functions are available in the ```kotlin.text``` package.

### Creating Strings

You can create a new string by using the ```String()``` function. This function takes an ```Any``` value and converts it to a string.

For example, you can create a new string from an integer like this:

```kotlin
val string = String(42)
```

You can also create a new string by concatenating two strings together. For example, you can concatenate the string "Hello" with the string "World" like this:

```kotlin
val string = "Hello" + "World"
```

### Accessing Characters in a String

You can access the characters in a string by using the ```get()``` function. This function takes an ```Int``` index and returns the character at that index.

For example, you can access the first character in a string like this:

```kotlin
val firstCharacter = string[0]
```

You can access the last character in a string like this:

```kotlin
val lastCharacter = string[string.length - 1]
```

And you can access the middle character in a string like this:

```kotlin
val middleCharacter = string[string.length / 2]
```

### Adding and Removing Characters from a String

You can add and remove characters from a string by using the ```plus()``` and ```minus()``` functions. The ```plus()``` function appends a character to the end of the string, and the ```minus()``` function removes a character from the string.

For example, you can add the character "!" to the end of a string like this:

```kotlin
val exclamationString = string + "!"
```

You can remove the first character from a string like this:

```kotlin
val noFirstCharacterString = string.drop(1)
```

And you can remove the last character from a string like this:

```kotlin
val noLastCharacterString = string.dropLast(1)
```

## Conclusion

In this post, we've taken a look at some of the most commonly used functions in the Kotlin standard library. We've seen how to create and manipulate collections, how to work with strings, and how to use some of the other commonly used functions in Kotlin.