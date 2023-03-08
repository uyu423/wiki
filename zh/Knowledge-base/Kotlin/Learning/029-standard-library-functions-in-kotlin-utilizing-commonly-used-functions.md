---
title: 029：Kotlin 中的标准库函数：使用常用函数
description: 
published: true
date: 2023-02-06T17:55:48.664Z
tags: 
editor: markdown
dateCreated: 2023-02-06T17:55:47.010Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [029: Standard Library Functions in Kotlin: Utilizing Commonly Used Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/029-standard-library-functions-in-kotlin-utilizing-commonly-used-functions)
{.links-list}


# 029：Kotlin 中的标准库函数：利用常用函数

Kotlin 是一种静态类型的编程语言，运行在 Java 虚拟机上，也可以编译成 JavaScript 源代码。 Kotlin 标准库提供了一组常用函数，无需任何额外依赖即可使用。

在本文中，我们将了解 Kotlin 标准库中一些最常用的函数，以及如何在您的代码中使用它们。

## 收藏

Kotlin 提供了一组用于处理数据集合的函数。这些函数在 ```kotlin.collections``` 包中可用。

### 创建集合

您可以使用```arrayOf()```、```listOf()``` 或```mutableListOf()``` 函数创建一个新集合。 ```arrayOf()``` 函数创建给定元素的数组，```listOf()``` 函数创建一个只读列表，```mutableListOf()``` 函数创建可变列表。

例如，您可以像这样创建一个新的字符串数组：

```kotlin
val array = arrayOf("a", "b", "c")
```

您可以像这样创建一个新的整数列表：

```kotlin
val list = listOf(1, 2, 3)
```

您可以像这样创建一个新的可变浮动列表：

```kotlin
val mutableList = mutableListOf(1.0f, 2.0f, 3.0f)
```

### 访问集合中的元素

您可以使用 ```get()``` 函数访问集合中的元素。这个函数接受一个 ```Int``` 索引并返回该索引处的元素。

例如，您可以像这样访问数组中的第一个元素：

```kotlin
val firstElement = array[0]
```

您可以像这样访问列表中的最后一个元素：

```kotlin
val lastElement = list[list.size - 1]
```

您可以像这样访问可变列表中的中间元素：

```kotlin
val middleElement = mutableList[mutableList.size / 2]
```

### 从集合中添加和删除元素

您可以使用 ```add()``` 和 ```remove()``` 函数在可变集合中添加和删除元素。 ```add()``` 函数将一个元素添加到集合的末尾，```remove()``` 函数从集合中删除一个元素。

例如，您可以像这样将一个元素添加到可变列表中：

```kotlin
mutableList.add("d")
```

您可以像这样从可变列表中删除第一个元素：

```kotlin
mutableList.removeAt(0)
```

您可以像这样从可变列表中删除最后一个元素：

```kotlin
mutableList.removeAt(mutableList.size - 1)
```

## 字符串

Kotlin 提供了一组用于处理字符串的函数。这些函数在 ```kotlin.text``` 包中可用。

### 创建字符串

您可以使用 ```String()``` 函数创建一个新字符串。这个函数接受一个```Any``` 值并将它转换成一个字符串。

例如，您可以像这样从一个整数创建一个新字符串：

```kotlin
val string = String(42)
```

您还可以通过将两个字符串连接在一起来创建一个新字符串。例如，您可以像这样连接字符串“Hello”和字符串“World”：

```kotlin
val string = "Hello" + "World"
```

### 访问字符串中的字符

您可以使用 ```get()``` 函数访问字符串中的字符。这个函数接受一个 ```Int``` 索引并返回该索引处的字符。

例如，您可以像这样访问字符串中的第一个字符：

```kotlin
val firstCharacter = string[0]
```

您可以像这样访问字符串中的最后一个字符：

```kotlin
val lastCharacter = string[string.length - 1]
```

您可以像这样访问字符串中的中间字符：

```kotlin
val middleCharacter = string[string.length / 2]
```

### 添加和删除字符串中的字符

您可以使用 ```plus()``` 和 ```minus()``` 函数在字符串中添加和删除字符。 ```plus()``` 函数将一个字符附加到字符串的末尾，```minus()``` 函数从字符串中删除一个字符。

例如，您可以添加字符“!”到像这样的字符串的末尾：

```kotlin
val exclamationString = string + "!"
```

您可以像这样从字符串中删除第一个字符：

```kotlin
val noFirstCharacterString = string.drop(1)
```

您可以像这样从字符串中删除最后一个字符：

```kotlin
val noLastCharacterString = string.dropLast(1)
```

## 结论

在本文中，我们了解了 Kotlin 标准库中一些最常用的函数。我们已经了解了如何创建和操作集合、如何使用字符串以及如何使用 Kotlin 中的其他一些常用函数。