---
title: 036: Kotlin의 연산자 오버로딩: 사용자 지정 유형에 대한 일반 연산자 오버로딩
description: 
published: true
date: 2023-02-14T10:18:41.023Z
tags: 
editor: markdown
dateCreated: 2023-02-14T10:18:39.252Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [036: Operator Overloading in Kotlin: Overloading Common Operators for Custom Types***English** document is available*](/en/Knowledge-base/Kotlin/Learning/036-operator-overloading-in-kotlin-overloading-common-operators-for-custom-types)
{.links-list}


# Kotlin의 연산자 오버로딩: 사용자 지정 유형에 대한 일반 연산자 오버로딩

Kotlin은 연산자 오버로딩을 지원합니다. 즉, `+`, `-`, `*`, `/` 등과 같은 일반적인 연산자가 자체 유형과 함께 사용될 때 사용자 지정 동작을 정의할 수 있습니다.

예를 들어 `x` 및 `y` 속성이 있는 `Point` 클래스를 정의하고 `+` 연산자를 오버로드하여 두 `Point` 인스턴스의 `x` 및 `y` 값을 함께 추가할 수 있습니다.

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

이 게시물에서는 Kotlin에서 일반 연산자를 오버로드하는 방법을 살펴보겠습니다. 또한 연산자 오버로딩을 사용하여 코드를 더 간결하고 읽기 쉽게 만드는 방법도 알아봅니다.

## 단항 연산자 오버로딩

단항 연산자는 단일 피연산자에서 작동하는 연산자입니다. Kotlin은 사용자 정의 유형에 대해 오버로드할 수 있는 기본 제공 단항 연산자 세트를 제공합니다.

가장 일반적인 단항 연산자는 피연산자를 부정하는 `-` 연산자입니다. 예를 들어 이전 섹션의 `Point` 클래스는 `-` 연산자를 오버로드하여 `x` 및 `y` 값을 모두 부정하도록 확장할 수 있습니다.

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

`-` 연산자 외에도 Kotlin은 부울 값을 반전시키는 `!` 연산자도 제공합니다. 이 연산자는 사용자 정의 형식에 대해서도 오버로드할 수 있습니다.

```kotlin
data class MyBoolean(val value: Boolean) {
    operator fun not(): MyBoolean {
        return MyBoolean(!value)
    }
}

val b1 = MyBoolean(true)
println(!b1) // Prints "MyBoolean(value=false)"
```

## 이진 연산자 오버로딩

이진 연산자는 두 개의 피연산자에서 작동하는 연산자입니다. Kotlin은 사용자 정의 유형에 대해 오버로드할 수 있는 기본 제공 바이너리 연산자 세트를 제공합니다.

가장 일반적인 이항 연산자는 두 값을 함께 더하는 `+` 연산자입니다. 우리는 이미 `Point` 클래스에 대해 이 연산자를 오버로드하는 방법을 살펴보았습니다.

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

`-` 연산자는 사용자 정의 유형에 대해 오버로드될 수도 있습니다. 예를 들어 `Point` 클래스에 대해 이 연산자를 오버로드하여 두 `Point` 인스턴스의 `x` 및 `y` 값을 뺄 수 있습니다.

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

Kotlin은 곱셈과 나눗셈에 각각 사용할 수 있는 `*` 및 `/` 연산자도 제공합니다. 이러한 연산자는 사용자 정의 형식에 대해서도 오버로드할 수 있습니다.

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

마지막으로 Kotlin은 나머지 계산에 사용할 수 있는 `%` 연산자를 제공합니다. 이 연산자는 사용자 정의 유형에 대해 오버로드될 수도 있습니다.

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

## 비교 연산자 오버로딩

Kotlin은 두 값을 비교하는 데 사용할 수 있는 비교 연산자 세트를 제공합니다. 이러한 연산자는 사용자 정의 형식에 대해서도 오버로드될 수 있습니다.

가장 일반적인 비교 연산자는 `==` 연산자로 두 값이 같은지 확인하는 데 사용할 수 있습니다. 예를 들어 `Point` 클래스에 대해 이 연산자를 오버로드하여 두 `Point` 인스턴스의 `x` 및 `y` 값을 비교할 수 있습니다.

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

Kotlin은 두 값이 같지 않은지 확인하는 데 사용할 수 있는 `!=` 연산자도 제공합니다. 이 연산자는 사용자 정의 형식에 대해서도 오버로드할 수 있습니다.

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

또한 Kotlin은 `<`, `>`, `<=` 및 `>=` 연산자를 제공하며 각각 보다 작음, 보다 큼, 작거나 같음, 크거나 같음 비교에 사용할 수 있습니다. 이러한 연산자는 사용자 정의 형식에 대해 오버로드될 수도 있습니다.

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

## 어레이 액세스 연산자 오버로딩

Kotlin은 배열의 요소에 액세스하는 데 사용할 수 있는 `[]` 연산자를 제공합니다. 이 연산자는 사용자 정의 형식에 대해서도 오버로드될 수 있습니다.

예를 들어 `0` 또는 `1` 인덱스가 각각 사용될 때 `x` 또는 `y` 값을 반환하도록 `Point` 클래스에 대해 이 연산자를 오버로드할 수 있습니다.

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

`[]` 연산자 외에도 Kotlin은 배열의 요소 값을 설정하는 데 사용할 수 있는 `[]=` 연산자도 제공합니다. 이 연산자는 사용자 정의 유형에 대해 오버로드될 수도 있습니다.

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

## 증가 및 감소 연산자 오버로딩

Kotlin은 각각 값을 늘리고 줄이는 데 사용할 수 있는 `inc()` 및 `dec()` 함수를 제공합니다. 이러한 함수는 사용자 정의 유형에 대해서도 오버로드될 수 있습니다.

예를 들어 `Point` 클래스에 대해 이러한 함수를 오버로드하여 `Point` 인스턴스의 `x` 및 `y` 값을 늘리거나 줄일 수 있습니다.

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

## 결론

이 게시물에서는 Kotlin에서 일반 연산자를 오버로드하는 방법을 살펴보았습니다. 또한 연산자 오버로딩을 사용하여 코드를 더 간결하고 읽기 쉽게 만드는 방법도 살펴보았습니다.

Kotlin의 연산자 오버로딩에 대해 자세히 알아보려면 다음 리소스를 확인하는 것이 좋습니다.

- [연산자 오버로딩](https://kotlinlang.org/docs/reference/operator-overloading.html)에 대한 공식 Kotlin 문서
- Kotlin의 연산자 오버로딩에 대한 [Svetlana Isakova](https://medium.com/@svetlanamisakova/operator-overloading-in-kotlin-4c7f0a0a2e35)의 훌륭한 블로그 게시물