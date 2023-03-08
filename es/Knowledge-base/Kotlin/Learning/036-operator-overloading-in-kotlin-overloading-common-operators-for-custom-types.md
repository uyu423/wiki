---
title: 036: Sobrecarga de operadores en Kotlin: Sobrecarga de operadores comunes para tipos personalizados
description: 
published: true
date: 2023-02-14T10:18:40.951Z
tags: 
editor: markdown
dateCreated: 2023-02-14T10:18:39.255Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [036: Operator Overloading in Kotlin: Overloading Common Operators for Custom Types***English** document is available*](/en/Knowledge-base/Kotlin/Learning/036-operator-overloading-in-kotlin-overloading-common-operators-for-custom-types)
{.links-list}


# Sobrecarga de operadores en Kotlin: Sobrecarga de operadores comunes para tipos personalizados

Kotlin admite la sobrecarga de operadores, lo que significa que puede definir un comportamiento personalizado para operadores comunes como `+`, `-`, `*`, `/`, etc., cuando se usan con sus propios tipos.

Por ejemplo, podría definir una clase `Punto` con las propiedades `x` e `y`, y sobrecargar el operador `+` para que agregue los valores `x` e `y` de dos instancias de `Punto` juntos:

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

En esta publicación, veremos cómo sobrecargar los operadores comunes en Kotlin. También veremos cómo se puede usar la sobrecarga de operadores para hacer que el código sea más conciso y legible.

## Sobrecarga de operadores unarios

Los operadores unarios son operadores que operan en un solo operando. Kotlin proporciona un conjunto de operadores unarios integrados, que se pueden sobrecargar para los tipos definidos por el usuario.

El operador unario más común es el operador `-`, que niega su operando. Por ejemplo, la clase `Punto` de la sección anterior podría extenderse para sobrecargar el operador `-` para que niegue los valores `x` e `y`:

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

Además del operador `-`, Kotlin también proporciona el operador `!`, que invierte un valor booleano. Este operador también se puede sobrecargar para los tipos definidos por el usuario:

```kotlin
data class MyBoolean(val value: Boolean) {
    operator fun not(): MyBoolean {
        return MyBoolean(!value)
    }
}

val b1 = MyBoolean(true)
println(!b1) // Prints "MyBoolean(value=false)"
```

## Sobrecarga de operadores binarios

Los operadores binarios son operadores que operan sobre dos operandos. Kotlin proporciona un conjunto de operadores binarios integrados, que se pueden sobrecargar para los tipos definidos por el usuario.

El operador binario más común es el operador `+`, que suma dos valores. Ya hemos visto cómo este operador puede sobrecargarse para la clase `Punto`:

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

El operador `-` también se puede sobrecargar para los tipos definidos por el usuario. Por ejemplo, podríamos sobrecargar este operador para la clase `Punto` para que reste los valores `x` e `y` de dos instancias `Punto`:

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

Kotlin también proporciona los operadores `*` y `/`, que se pueden usar para multiplicar y dividir respectivamente. Estos operadores también se pueden sobrecargar para los tipos definidos por el usuario:

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

Finalmente, Kotlin proporciona el operador `%`, que se puede usar para calcular el resto. Este operador también se puede sobrecargar para tipos definidos por el usuario:

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

## Sobrecarga de operadores de comparación

Kotlin proporciona un conjunto de operadores de comparación, que se pueden usar para comparar dos valores. Estos operadores también se pueden sobrecargar para los tipos definidos por el usuario.

El operador de comparación más común es el operador `==`, que se puede utilizar para comprobar si dos valores son iguales. Por ejemplo, podríamos sobrecargar este operador para la clase `Punto` para que compare los valores `x` e `y` de dos instancias `Punto`:

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

Kotlin también proporciona el operador `!=`, que se puede usar para verificar si dos valores no son iguales. Este operador también se puede sobrecargar para los tipos definidos por el usuario:

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

Kotlin también proporciona los operadores `<`, `>`, `<=` y `>=`, que se pueden usar para comparaciones de menor que, mayor que, menor que o igual a y mayor que o igual a, respectivamente. Estos operadores también se pueden sobrecargar para tipos definidos por el usuario:

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

## Sobrecarga del operador de acceso al arreglo

Kotlin proporciona el operador `[]`, que se puede usar para acceder a los elementos de una matriz. Este operador también se puede sobrecargar para los tipos definidos por el usuario.

Por ejemplo, podríamos sobrecargar este operador para la clase `Punto` para que devuelva el valor `x` o `y` cuando se usa el índice `0` o `1` respectivamente:

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

Además del operador `[]`, Kotlin también proporciona el operador `[]=`, que se puede usar para establecer el valor de un elemento en una matriz. Este operador también se puede sobrecargar para tipos definidos por el usuario:

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

## Sobrecarga de operadores de incremento y decremento

Kotlin proporciona las funciones `inc()` y `dec()`, que se pueden usar para incrementar y disminuir un valor respectivamente. Estas funciones también se pueden sobrecargar para los tipos definidos por el usuario.

Por ejemplo, podríamos sobrecargar estas funciones para la clase `Punto` para que incrementen o disminuyan los valores `x` e `y` de una instancia `Punto`:

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

## Conclusión

En esta publicación, hemos visto cómo sobrecargar los operadores comunes en Kotlin. También hemos visto cómo se puede usar la sobrecarga de operadores para hacer que el código sea más conciso y legible.

Si desea obtener más información sobre la sobrecarga de operadores en Kotlin, le recomiendo consultar los siguientes recursos:

- La documentación oficial de Kotlin sobre [sobrecarga de operadores](https://kotlinlang.org/docs/reference/operator-overloading.html)
- Una excelente publicación de blog de [Svetlana Isakova](https://medium.com/@svetlanamisakova/operator-overloading-in-kotlin-4c7f0a0a2e35) sobre la sobrecarga de operadores en Kotlin