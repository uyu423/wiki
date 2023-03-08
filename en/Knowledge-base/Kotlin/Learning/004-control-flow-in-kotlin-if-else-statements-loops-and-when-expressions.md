---
title: 004: Control Flow in Kotlin: if-else Statements, Loops, and When Expressions
description: 
published: true
date: 2023-02-16T01:33:06.953Z
tags: 
editor: markdown
dateCreated: 2023-02-16T01:32:59.171Z
---

- [004: Flujo de control en Kotlin: declaraciones if-else, bucles y expresiones when***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/004-control-flow-in-kotlin-if-else-statements-loops-and-when-expressions)
{.links-list}
- [004：Kotlin 中的控制流：if-else 语句、循环和 When 表达式***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/004-control-flow-in-kotlin-if-else-statements-loops-and-when-expressions)
{.links-list}
- [004: Kotlin의 제어 흐름: if-else 문, 루프 및 When 표현식***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/004-control-flow-in-kotlin-if-else-statements-loops-and-when-expressions)
{.links-list}


# Control Flow in Kotlin: if-else Statements, Loops, and When Expressions

Kotlin provides a comprehensive set of control flow constructs. In this post, we'll take a look at how to use if-else statements, loops, and when expressions in Kotlin.

## if-else Statements

If-else statements are used to execute a certain block of code only if a certain condition is met. The general form of an if-else statement in Kotlin is as follows:

```kotlin
if (condition) {
    // Execute this block if the condition is true
} else {
    // Execute this block if the condition is false
}
```

Let's see a few examples of how to use if-else statements in Kotlin.

### Example 1

In this example, we'll use an if-else statement to print out whether a number is positive or negative.

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

Output:

```
5 is positive
```

### Example 2

In this example, we'll use an if-else statement to print out the larger of two numbers.

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

Output:

```
10 is larger than 5
```

## Loops

Loops are used to execute a certain block of code multiple times. Kotlin provides three different types of loops: for loops, while loops, and do-while loops.

### for Loops

For loops are used to iterate over a range of values or an array of values. The general form of a for loop in Kotlin is as follows:

```kotlin
for (variable in range) {
    // Execute this block for each value in the range
}
```

Let's see a few examples of how to use for loops in Kotlin.

### Example 1

In this example, we'll use a for loop to print out the first 10 natural numbers.

```kotlin
fun main(args: Array<String>) {
    for (i in 1..10) {
        println(i)
    }
}
```

Output:

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

### Example 2

In this example, we'll use a for loop to print out the elements of an array.

```kotlin
fun main(args: Array<String>) {
    val array = arrayOf(1, 2, 3, 4, 5)

    for (element in array) {
        println(element)
    }
}
```

Output:

```
1
2
3
4
5
```

### while Loops

While loops are used to execute a certain block of code multiple times until a certain condition is met. The general form of a while loop in Kotlin is as follows:

```kotlin
while (condition) {
    // Execute this block while the condition is true
}
```

Let's see a few examples of how to use while loops in Kotlin.

### Example 1

In this example, we'll use a while loop to print out the first 10 natural numbers.

```kotlin
fun main(args: Array<String>) {
    var i = 1

    while (i <= 10) {
        println(i)
        i++
    }
}
```

Output:

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

### Example 2

In this example, we'll use a while loop to sum the first 10 natural numbers.

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

Output:

```
The sum of the first 10 natural numbers is 55
```

### do-while Loops

Do-while loops are used to execute a certain block of code multiple times until a certain condition is met. The general form of a do-while loop in Kotlin is as follows:

```kotlin
do {
    // Execute this block at least once
} while (condition)
```

Let's see a few examples of how to use do-while loops in Kotlin.

### Example 1

In this example, we'll use a do-while loop to print out the first 10 natural numbers.

```kotlin
fun main(args: Array<String>) {
    var i = 1

    do {
        println(i)
        i++
    } while (i <= 10)
}
```

Output:

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

### Example 2

In this example, we'll use a do-while loop to sum the first 10 natural numbers.

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

Output:

```
The sum of the first 10 natural numbers is 55
```

## When Expressions

When expressions are used to execute a certain block of code based on a certain value. The general form of a when expression in Kotlin is as follows:

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

Let's see a few examples of how to use when expressions in Kotlin.

### Example 1

In this example, we'll use a when expression to print out the meaning of a certain color.

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

Output:

```
Red is the color of blood
```

### Example 2

In this example, we'll use a when expression to print out the grade of a student based on their score.

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

Output:

```
You got an A!
```

## Conclusion

In this post, we've seen how to use if-else statements, loops, and when expressions in Kotlin. These are all important control flow constructs that you'll need to know in order to write Kotlin programs.