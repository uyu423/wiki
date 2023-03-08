---
title: 036：Kotlin 中的运算符重载：为自定义类型重载通用运算符
description: 
published: true
date: 2023-02-14T10:18:40.942Z
tags: 
editor: markdown
dateCreated: 2023-02-14T10:18:39.251Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [036: Operator Overloading in Kotlin: Overloading Common Operators for Custom Types***English** document is available*](/en/Knowledge-base/Kotlin/Learning/036-operator-overloading-in-kotlin-overloading-common-operators-for-custom-types)
{.links-list}


# Kotlin 中的运算符重载：为自定义类型重载通用运算符

Kotlin 支持运算符重载，这意味着您可以为“+”、“-”、“*”、“/”等常见运算符定义自定义行为，当它们与您自己的类型一起使用时。

例如，您可以定义一个具有“x”和“y”属性的“Point”类，并重载“+”运算符，以便它将两个“Point”实例的“x”和“y”值相加：

```kotlin
data class Point(val x: Int, val y: Int) {
    operator fun plus(other: Point): Point {
        return Point(x + other.x, y + other.y)
    }
}

val p1 = Point(10, 20)
val p2 = Point(30, 40)
println(p1 + p2) // Prints "Point(x=40, y=60)"
```

在本文中，我们将了解如何在 Kotlin 中重载常用运算符。我们还将看到如何使用运算符重载来使代码更加简洁和可读。

## 重载一元运算符

一元运算符是对单个操作数进行运算的运算符。 Kotlin 提供了一组内置的一元运算符，可以为用户定义的类型重载。

最常见的一元运算符是“-”运算符，它取反其操作数。例如，可以扩展上一节中的“Point”类以重载“-”运算符，以便它否定“x”和“y”值：

```kotlin
data class Point(val x: Int, val y: Int) {
    operator fun plus(other: Point): Point {
        return Point(x + other.x, y + other.y)
    }

    operator fun unaryMinus(): Point {
        return Point(-x, -y)
    }
}

val p1 = Point(10, 20)
println(-p1) // Prints "Point(x=-10, y=-20)"
```

除了 `-` 运算符，Kotlin 还提供了 `!` 运算符，它可以反转布尔值。也可以为用户定义的类型重载此运算符：

```kotlin
data class MyBoolean(val value: Boolean) {
    operator fun not(): MyBoolean {
        return MyBoolean(!value)
    }
}

val b1 = MyBoolean(true)
println(!b1) // Prints "MyBoolean(value=false)"
```

## 重载二元运算符

二元运算符是对两个操作数进行运算的运算符。 Kotlin 提供了一组内置的二元运算符，可以为用户定义的类型重载。

最常见的二元运算符是“+”运算符，它将两个值相加。我们已经看到如何为 Point 类重载此运算符：

```kotlin
data class Point(val x: Int, val y: Int) {
    operator fun plus(other: Point): Point {
        return Point(x + other.x, y + other.y)
    }
}

val p1 = Point(10, 20)
val p2 = Point(30, 40)
println(p1 + p2) // Prints "Point(x=40, y=60)"
```

`-` 运算符也可以为用户定义的类型重载。例如，我们可以为 Point 类重载此运算符，以便它减去两个 Point 实例的 x 和 y 值：

```kotlin
data class Point(val x: Int, val y: Int) {
    operator fun plus(other: Point): Point {
        return Point(x + other.x, y + other.y)
    }

    operator fun minus(other: Point): Point {
        return Point(x - other.x, y - other.y)
    }
}

val p1 = Point(10, 20)
val p2 = Point(30, 40)
println(p1 - p2) // Prints "Point(x=-20, y=-20)"
```

Kotlin 还提供了 `*` 和 `/` 运算符，可分别用于乘法和除法。这些运算符也可以为用户定义的类型重载：

```kotlin
data class MyInt(val value: Int) {
    operator fun times(other: MyInt): MyInt {
        return MyInt(value * other.value)
    }

    operator fun div(other: MyInt): MyInt {
        return MyInt(value / other.value)
    }
}

val i1 = MyInt(10)
val i2 = MyInt(20)
println(i1 * i2) // Prints "MyInt(value=200)"
println(i1 / i2) // Prints "MyInt(value=0)"
```

最后，Kotlin 提供了 `%` 运算符，可用于余数计算。也可以为用户定义的类型重载此运算符：

```kotlin
data class MyInt(val value: Int) {
    operator fun times(other: MyInt): MyInt {
        return MyInt(value * other.value)
    }

    operator fun div(other: MyInt): MyInt {
        return MyInt(value / other.value)
    }

    operator fun rem(other: MyInt): MyInt {
        return MyInt(value % other.value)
    }
}

val i1 = MyInt(10)
val i2 = MyInt(3)
println(i1 % i2) // Prints "MyInt(value=1)"
```

## 重载比较运算符

Kotlin 提供了一组比较运算符，可以用来比较两个值。这些运算符也可以为用户定义的类型重载。

最常见的比较运算符是 `==` 运算符，可用于检查两个值是否相等。例如，我们可以为 Point 类重载此运算符，以便它比较两个 Point 实例的 x 和 y 值：

```kotlin
data class Point(val x: Int, val y: Int) {
    operator fun plus(other: Point): Point {
        return Point(x + other.x, y + other.y)
    }

    operator fun minus(other: Point): Point {
        return Point(x - other.x, y - other.y)
    }

    operator fun times(other: Point): Point {
        return Point(x * other.x, y * other.y)
    }

    operator fun div(other: Point): Point {
        return Point(x / other.x, y / other.y)
    }

    operator fun rem(other: Point): Point {
        return Point(x % other.x, y % other.y)
    }

    operator fun compareTo(other: Point): Int {
        return x.compareTo(other.x)
    }
}

val p1 = Point(10, 20)
val p2 = Point(10, 30)
println(p1 == p2) // Prints "false"
```

Kotlin 还提供了 `!=` 运算符，可用于检查两个值是否不相等。也可以为用户定义的类型重载此运算符：

```kotlin
data class Point(val x: Int, val y: Int) {
    operator fun plus(other: Point): Point {
        return Point(x + other.x, y + other.y)
    }

    operator fun minus(other: Point): Point {
        return Point(x - other.x, y - other.y)
    }

    operator fun times(other: Point): Point {
        return Point(x * other.x, y * other.y)
    }

    operator fun div(other: Point): Point {
        return Point(x / other.x, y / other.y)
    }

    operator fun rem(other: Point): Point {
        return Point(x % other.x, y % other.y)
    }

    operator fun compareTo(other: Point): Int {
        return x.compareTo(other.x)
    }
}

val p1 = Point(10, 20)
val p2 = Point(10, 30)
println(p1 != p2) // Prints "true"
```

Kotlin 还提供了`<`、`>`、`<=` 和`>=` 运算符，它们可以分别用于小于、大于、小于等于和大于等于比较。这些运算符也可以为用户定义的类型重载：

```kotlin
data class Point(val x: Int, val y: Int) {
    operator fun plus(other: Point): Point {
        return Point(x + other.x, y + other.y)
    }

    operator fun minus(other: Point): Point {
        return Point(x - other.x, y - other.y)
    }

    operator fun times(other: Point): Point {
        return Point(x * other.x, y * other.y)
    }

    operator fun div(other: Point): Point {
        return Point(x / other.x, y / other.y)
    }

    operator fun rem(other: Point): Point {
        return Point(x % other.x, y % other.y)
    }

    operator fun compareTo(other: Point): Int {
        return x.compareTo(other.x)
    }
}

val p1 = Point(10, 20)
val p2 = Point(10, 30)
println(p1 < p2)  // Prints "true"
println(p1 > p2)  // Prints "false"
println(p1 <= p2) // Prints "true"
println(p1 >= p2) // Prints "false"
```

## 重载数组访问运算符

Kotlin 提供了 `[]` 运算符，可用于访问数组中的元素。也可以为用户定义的类型重载此运算符。

例如，我们可以为“Point”类重载此运算符，以便在分别使用“0”或“1”索引时返回“x”或“y”值：

```kotlin
data class Point(val x: Int, val y: Int) {
    operator fun get(index: Int): Int {
        return when (index) {
            0 -> x
            1 -> y
            else -> throw IndexOutOfBoundsException("Invalid index $index")
        }
    }
}

val p = Point(10, 20)
println(p[0]) // Prints "10"
println(p[1]) // Prints "20"
println(p[2]) // Throws an IndexOutOfBoundsException
```

除了 `[]` 运算符，Kotlin 还提供了 `[]=` 运算符，可用于设置数组中元素的值。也可以为用户定义的类型重载此运算符：

```kotlin
data class Point(var x: Int, var y: Int) {
    operator fun get(index: Int): Int {
        return when (index) {
            0 -> x
            1 -> y
            else -> throw IndexOutOfBoundsException("Invalid index $index")
        }
    }

    operator fun set(index: Int, value: Int) {
        when (index) {
            0 -> x = value
            1 -> y = value
            else -> throw IndexOutOfBoundsException("Invalid index $index")
        }
    }
}

val p = Point(10, 20)
p[0] = 30 // Sets the x value to 30
p[1] = 40 // Sets the y value to 40
println(p) // Prints "Point(x=30, y=40)"
```

## 重载递增和递减运算符

Kotlin 提供了 `inc()` 和 `dec()` 函数，它们可以分别用于递增和递减一个值。这些函数也可以为用户定义的类型重载。

例如，我们可以为 Point 类重载这些函数，以便它们增加或减少 Point 实例的 x 和 y 值：

```kotlin
data class Point(var x: Int, var y: Int) {
    operator fun inc(): Point {
        return Point(x + 1, y + 1)
    }

    operator fun dec(): Point {
        return Point(x - 1, y - 1)
    }
}

val p = Point(10, 20)
println(p++) // Prints "Point(x=10, y=20)"
println(p)   // Prints "Point(x=11, y=21)"
println(++p) // Prints "Point(x=12, y=22)"
println(p--) // Prints "Point(x=12, y=22)"
println(p)   // Prints "Point(x=11, y=21)"
println(--p) // Prints "Point(x=10, y=20)"
```

## 结论

在本文中，我们了解了如何在 Kotlin 中重载常用运算符。我们还看到了如何使用运算符重载来使代码更加简洁和可读。

如果您想了解有关 Kotlin 中运算符重载的更多信息，我建议您查看以下资源：

- 关于[运算符重载]的官方 Kotlin 文档(https://kotlinlang.org/docs/reference/operator-overloading.html)
- [Svetlana Isakova](https://medium.com/@svetlanamisakova/operator-overloading-in-kotlin-4c7f0a0a2e35) 关于 Kotlin 中运算符重载的精彩博文