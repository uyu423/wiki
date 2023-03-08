---
title: 004：Kotlin 中的控制流：if-else 语句、循环和 When 表达式
description: 
published: true
date: 2023-02-16T01:33:01.052Z
tags: 
editor: markdown
dateCreated: 2023-02-16T01:32:59.166Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [004: Control Flow in Kotlin: if-else Statements, Loops, and When Expressions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/004-control-flow-in-kotlin-if-else-statements-loops-and-when-expressions)
{.links-list}


# Kotlin 中的控制流：if-else 语句、循环和 When 表达式

Kotlin 提供了一套全面的控制流结构。在本文中，我们将了解如何在 Kotlin 中使用 if-else 语句、循环和 when 表达式。

## if-else 语句

if-else 语句用于仅在满足特定条件时才执行特定代码块。 Kotlin 中 if-else 语句的一般形式如下：

```kotlin
if (condition) {
    // Execute this block if the condition is true
} else {
    // Execute this block if the condition is false
}
```

让我们看一些如何在 Kotlin 中使用 if-else 语句的示例。

### 示例 1

在此示例中，我们将使用 if-else 语句打印出数字是正数还是负数。

```kotlin
fun main(args: Array<String>) {
    val num = 5

    if (num > 0) {
        println("$num is positive")
    } else {
        println("$num is negative")
    }
}
```

输出：

```
5 is positive
```

### 示例 2

在此示例中，我们将使用 if-else 语句打印出两个数字中较大的一个。

```kotlin
fun main(args: Array<String>) {
    val num1 = 5
    val num2 = 10

    if (num1 > num2) {
        println("$num1 is larger than $num2")
    } else {
        println("$num2 is larger than $num1")
    }
}
```

输出：

```
10 is larger than 5
```

## 循环

循环用于多次执行某个代码块。 Kotlin 提供了三种不同类型的循环：for 循环、while 循环和 do-while 循环。

### 循环

For 循环用于迭代一个值范围或一个值数组。 Kotlin 中 for 循环的一般形式如下：

```kotlin
for (variable in range) {
    // Execute this block for each value in the range
}
```

让我们看几个示例，了解如何在 Kotlin 中使用 for 循环。

### 示例 1

在此示例中，我们将使用 for 循环打印出前 10 个自然数。

```kotlin
fun main(args: Array<String>) {
    for (i in 1..10) {
        println(i)
    }
}
```

输出：

```
1
2
3
4
5
6
7
8
9
10
```

### 示例 2

在此示例中，我们将使用 for 循环打印出数组的元素。

```kotlin
fun main(args: Array<String>) {
    val array = arrayOf(1, 2, 3, 4, 5)

    for (element in array) {
        println(element)
    }
}
```

输出：

```
1
2
3
4
5
```

### while 循环

While 循环用于多次执行某个代码块，直到满足某个条件。 Kotlin中while循环的一般形式如下：

```kotlin
while (condition) {
    // Execute this block while the condition is true
}
```

让我们看几个示例，了解如何在 Kotlin 中使用 while 循环。

### 示例 1

在此示例中，我们将使用 while 循环打印出前 10 个自然数。

```kotlin
fun main(args: Array<String>) {
    var i = 1

    while (i <= 10) {
        println(i)
        i++
    }
}
```

输出：

```
1
2
3
4
5
6
7
8
9
10
```

### 示例 2

在此示例中，我们将使用 while 循环对前 10 个自然数求和。

```kotlin
fun main(args: Array<String>) {
    var i = 1
    var sum = 0

    while (i <= 10) {
        sum += i
        i++
    }

    println("The sum of the first 10 natural numbers is $sum")
}
```

输出：

```
The sum of the first 10 natural numbers is 55
```

### do-while 循环

Do-while 循环用于多次执行某个代码块，直到满足某个条件。 Kotlin 中 do-while 循环的一般形式如下：

```kotlin
do {
    // Execute this block at least once
} while (condition)
```

让我们看几个示例，了解如何在 Kotlin 中使用 do-while 循环。

### 示例 1

在此示例中，我们将使用 do-while 循环打印出前 10 个自然数。

```kotlin
fun main(args: Array<String>) {
    var i = 1

    do {
        println(i)
        i++
    } while (i <= 10)
}
```

输出：

```
1
2
3
4
5
6
7
8
9
10
```

### 示例 2

在此示例中，我们将使用 do-while 循环对前 10 个自然数求和。

```kotlin
fun main(args: Array<String>) {
    var i = 1
    var sum = 0

    do {
        sum += i
        i++
    } while (i <= 10)

    println("The sum of the first 10 natural numbers is $sum")
}
```

输出：

```
The sum of the first 10 natural numbers is 55
```

## 当表达式

当表达式用于根据特定值执行特定代码块时。 Kotlin 中 when 表达式的一般形式如下：

```kotlin
when (value) {
    value1 -> {
        // Execute this block when the value is value1
    }
    value2 -> {
        // Execute this block when the value is value2
    }
    // ...
    else -> {
        // Execute this block when the value is none of the above
    }
}
```

让我们看几个示例，了解如何在 Kotlin 中使用 when 表达式。

### 示例 1

在这个例子中，我们将使用一个 when 表达式来打印出某种颜色的含义。

```kotlin
fun main(args: Array<String>) {
    val color = "red"

    when (color) {
        "red" -> println("Red is the color of blood")
        "blue" -> println("Blue is the color of the sky")
        "green" -> println("Green is the color of grass")
        else -> println("I don't know the meaning of that color")
    }
}
```

输出：

```
Red is the color of blood
```

### 示例 2

在此示例中，我们将使用 when 表达式根据学生的分数打印出学生的成绩。

```kotlin
fun main(args: Array<String>) {
    val score = 95

    when (score) {
        in 90..100 -> println("You got an A!")
        in 80..89 -> println("You got a B!")
        in 70..79 -> println("You got a C!")
        in 60..69 -> println("You got a D!")
        else -> println("You got an F!")
    }
}
```

输出：

```
You got an A!
```

## 结论

在本文中，我们了解了如何在 Kotlin 中使用 if-else 语句、循环和 when 表达式。这些都是重要的控制流结构，您需要了解这些结构才能编写 Kotlin 程序。