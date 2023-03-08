---
title: 036: Operator Overloading in Kotlin: Overloading Common Operators for Custom Types
description: 
published: true
date: 2023-02-14T10:18:46.515Z
tags: 
editor: markdown
dateCreated: 2023-02-14T10:18:39.256Z
---

- [036: Sobrecarga de operadores en Kotlin: Sobrecarga de operadores comunes para tipos personalizados***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/036-operator-overloading-in-kotlin-overloading-common-operators-for-custom-types)
{.links-list}
- [036：Kotlin 中的运算符重载：为自定义类型重载通用运算符***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/036-operator-overloading-in-kotlin-overloading-common-operators-for-custom-types)
{.links-list}
- [036: Kotlin의 연산자 오버로딩: 사용자 지정 유형에 대한 일반 연산자 오버로딩***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/036-operator-overloading-in-kotlin-overloading-common-operators-for-custom-types)
{.links-list}


# Operator Overloading in Kotlin: Overloading Common Operators for Custom Types

Kotlin supports operator overloading, which means you can define custom behavior for common operators like `+`, `-`, `*`, `/`, and so on, when they are used with your own types.

For example, you could define an `Point` class with `x` and `y` properties, and overload the `+` operator so that it adds the `x` and `y` values of two `Point` instances together:

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

In this post, we'll take a look at how to overload common operators in Kotlin. We'll also see how operator overloading can be used to make code more concise and readable.

## Overloading Unary Operators

Unary operators are operators that operate on a single operand. Kotlin provides a set of built-in unary operators, which can be overloaded for user-defined types.

The most common unary operator is the `-` operator, which negates its operand. For example, the `Point` class from the previous section could be extended to overload the `-` operator so that it negates both the `x` and `y` values:

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

In addition to the `-` operator, Kotlin also provides the `!` operator, which inverts a Boolean value. This operator can be overloaded for user-defined types as well:

```kotlin
data class MyBoolean(val value: Boolean) {
    operator fun not(): MyBoolean {
        return MyBoolean(!value)
    }
}

val b1 = MyBoolean(true)
println(!b1) // Prints "MyBoolean(value=false)"
```

## Overloading Binary Operators

Binary operators are operators that operate on two operands. Kotlin provides a set of built-in binary operators, which can be overloaded for user-defined types.

The most common binary operator is the `+` operator, which adds two values together. We've already seen how this operator can be overloaded for the `Point` class:

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

The `-` operator can also be overloaded for user-defined types. For example, we could overload this operator for the `Point` class so that it subtracts the `x` and `y` values of two `Point` instances:

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

Kotlin also provides the `*` and `/` operators, which can be used for multiplication and division respectively. These operators can be overloaded for user-defined types as well:

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

Finally, Kotlin provides the `%` operator, which can be used for remainder calculation. This operator can also be overloaded for user-defined types:

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

## Overloading Comparison Operators

Kotlin provides a set of comparison operators, which can be used to compare two values. These operators can be overloaded for user-defined types as well.

The most common comparison operator is the `==` operator, which can be used to check if two values are equal. For example, we could overload this operator for the `Point` class so that it compares the `x` and `y` values of two `Point` instances:

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

Kotlin also provides the `!=` operator, which can be used to check if two values are not equal. This operator can be overloaded for user-defined types as well:

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

Kotlin also provides the `<`, `>`, `<=`, and `>=` operators, which can be used for less than, greater than, less than or equal to, and greater than or equal to comparisons respectively. These operators can also be overloaded for user-defined types:

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

## Overloading the Array Access Operator

Kotlin provides the `[]` operator, which can be used to access elements in an array. This operator can be overloaded for user-defined types as well.

For example, we could overload this operator for the `Point` class so that it returns the `x` or `y` value when the `0` or `1` index is used respectively:

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

In addition to the `[]` operator, Kotlin also provides the `[]=` operator, which can be used to set the value of an element in an array. This operator can also be overloaded for user-defined types:

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

## Overloading Increment and Decrement Operators

Kotlin provides the `inc()` and `dec()` functions, which can be used to increment and decrement a value respectively. These functions can be overloaded for user-defined types as well.

For example, we could overload these functions for the `Point` class so that they increment or decrement the `x` and `y` values of a `Point` instance:

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

## Conclusion

In this post, we've seen how to overload common operators in Kotlin. We've also seen how operator overloading can be used to make code more concise and readable.

If you want to learn more about operator overloading in Kotlin, I recommend checking out the following resources:

- The official Kotlin documentation on [operator overloading](https://kotlinlang.org/docs/reference/operator-overloading.html)
- A great blog post by [Svetlana Isakova](https://medium.com/@svetlanamisakova/operator-overloading-in-kotlin-4c7f0a0a2e35) on operator overloading in Kotlin