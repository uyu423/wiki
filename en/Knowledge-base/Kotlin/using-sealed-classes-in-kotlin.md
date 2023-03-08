---
title: Using Sealed Classes in Kotlin
description: 
published: true
date: 2023-02-15T10:55:42.018Z
tags: 
editor: markdown
dateCreated: 2023-02-15T10:55:40.104Z
---

- [Uso de clases selladas en Kotlin***Spanish** document is available*](/es/Knowledge-base/Kotlin/using-sealed-classes-in-kotlin)
{.links-list}
- [在 Kotlin 中使用密封类***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/using-sealed-classes-in-kotlin)
{.links-list}
- [Kotlin에서 봉인된 클래스 사용***Korean** document is available*](/ko/Knowledge-base/Kotlin/using-sealed-classes-in-kotlin)
{.links-list}


# Using Sealed Classes in Kotlin

Kotlin's sealed classes are a great way to restrict a class's inheritance. By sealing a class, you can control which other classes can inherit from it. This can be useful for a number of reasons, including preventing accidental inheritance and creating more type-safe code.

Sealed classes are defined using the `sealed` keyword:

```kotlin
sealed class MySealedClass
```

Sealed classes can have subclasses, but those subclasses must be declared in the same file as the sealed class. This is to prevent accidental inheritance from outside the file. For example, the following is not allowed:

```kotlin
// MySealedClass.kt

sealed class MySealedClass

// MySubclass.kt

class MySubclass: MySealedClass // Error: MySubclass is not a member of the sealed class
```

To fix this, you can move `MySubclass` into the same file as `MySealedClass`:

```kotlin
// MySealedClass.kt

sealed class MySealedClass

class MySubclass: MySealedClass // Ok
```

You can also declare sealed classes as `inner`:

```kotlin
class MyClass {
    sealed class MySealedClass
}
```

In this case, the subclasses must be declared inside `MyClass`:

```kotlin
class MyClass {
    sealed class MySealedClass

    class MySubclass: MySealedClass // Ok
}

class MySubclass: MyClass.MySealedClass // Error: MySubclass is not a member of MyClass
```

Sealed classes are useful for creating type-safe code. For example, consider the following sealed class hierarchy:

```kotlin
sealed class Shape {
    class Circle(val radius: Double): Shape()
    class Rectangle(val width: Double, val height: Double): Shape()
}
```

You can use a when expression to handle the different subclasses of `Shape` in a type-safe way:

```kotlin
fun getArea(shape: Shape): Double = when(shape) {
    is Shape.Circle -> Math.PI * shape.radius * shape.radius
    is Shape.Rectangle -> shape.width * shape.height
}
```

In this example, the compiler can determine that the `shape` variable can only be of type `Circle` or `Rectangle`, so it does not require an `else` branch.

Sealed classes are also useful for restricting the type of a variable. For example, consider the following sealed class hierarchy:

```kotlin
sealed class Pet {
    class Dog: Pet()
    class Cat: Pet()
}
```

You can use a sealed class to restrict the type of a variable to a specific subclass:

```kotlin
fun getPet(name: String): Pet? = when(name) {
    "Bob" -> Pet.Dog()
    "Mary" -> Pet.Cat()
    else -> null
}

val pet: Pet = getPet("Bob") // Ok
val pet: Pet = getPet("Mary") // Ok
val pet: Pet = getPet("John") // Error: Type mismatch: inferred type is Pet? but Pet was expected
```

In this example, the `getPet()` function returns a `Dog` if the `name` parameter is "Bob" and a `Cat` if the `name` parameter is "Mary". If the `name` parameter is neither "Bob" nor "Mary", `getPet()` returns `null`.

The `pet` variable is declared as type `Pet` and is assigned the return value of `getPet()`. This is valid because the compiler knows that the return value of `getPet()` can only be `Dog`, `Cat`, or `null`. If `getPet()` could return any subclass of `Pet`, the assignment would be invalid.

## References

- [Kotlin Sealed Classes](https://kotlinlang.org/docs/reference/sealed-classes.html)
- [Sealed Classes in Kotlin](https://medium.com/@BladeCoder/sealed-classes-in-kotlin-67861b4bfe7d)
- [Sealed Classes](https://antonioleiva.com/sealed-classes/)