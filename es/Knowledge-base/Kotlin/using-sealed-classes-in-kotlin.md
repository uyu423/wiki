---
title: Uso de clases selladas en Kotlin
description: 
published: true
date: 2023-02-15T10:55:47.964Z
tags: 
editor: markdown
dateCreated: 2023-02-15T10:55:40.100Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Using Sealed Classes in Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/using-sealed-classes-in-kotlin)
{.links-list}


# Uso de clases selladas en Kotlin

Las clases selladas de Kotlin son una excelente manera de restringir la herencia de una clase. Al sellar una clase, puede controlar qué otras clases pueden heredar de ella. Esto puede ser útil por varias razones, incluida la prevención de la herencia accidental y la creación de un código más seguro.

Las clases selladas se definen usando la palabra clave `sellado`:

```kotlin
sealed class MySealedClass
```

Las clases selladas pueden tener subclases, pero esas subclases deben declararse en el mismo archivo que la clase sellada. Esto es para evitar la herencia accidental desde fuera del archivo. Por ejemplo, lo siguiente no está permitido:

```kotlin
// MySealedClass.kt

sealed class MySealedClass

// MySubclass.kt

class MySubclass: MySealedClass // Error: MySubclass is not a member of the sealed class
```

Para solucionar esto, puede mover `MySubclass` al mismo archivo que `MySealedClass`:

```kotlin
// MySealedClass.kt

sealed class MySealedClass

class MySubclass: MySealedClass // Ok
```

También puedes declarar clases selladas como `inner`:

```kotlin
class MyClass {
    sealed class MySealedClass
}
```

En este caso, las subclases deben declararse dentro de `MyClass`:

```kotlin
class MyClass {
    sealed class MySealedClass

    class MySubclass: MySealedClass // Ok
}

class MySubclass: MyClass.MySealedClass // Error: MySubclass is not a member of MyClass
```

Las clases selladas son útiles para crear código con seguridad de tipos. Por ejemplo, considere la siguiente jerarquía de clases selladas:

```kotlin
sealed class Shape {
    class Circle(val radius: Double): Shape()
    class Rectangle(val width: Double, val height: Double): Shape()
}
```

Puedes usar una expresión when para manejar las diferentes subclases de `Shape` de una forma segura:

```kotlin
fun getArea(shape: Shape): Double = when(shape) {
    is Shape.Circle -> Math.PI * shape.radius * shape.radius
    is Shape.Rectangle -> shape.width * shape.height
}
```

En este ejemplo, el compilador puede determinar que la variable `shape` solo puede ser del tipo `Circle` o `Rectangle`, por lo que no requiere una rama `else`.

Las clases selladas también son útiles para restringir el tipo de una variable. Por ejemplo, considere la siguiente jerarquía de clases selladas:

```kotlin
sealed class Pet {
    class Dog: Pet()
    class Cat: Pet()
}
```

Puede usar una clase sellada para restringir el tipo de una variable a una subclase específica:

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

En este ejemplo, la función `getPet()` devuelve un `Perro` si el parámetro `nombre` es "Bob" y un `Gato` si el parámetro `nombre` es "Mary". Si el parámetro `name` no es ni "Bob" ni "Mary", `getPet()` devuelve `null`.

La variable `mascota` se declara como tipo `Pet` y se le asigna el valor de retorno de `getPet()`. Esto es válido porque el compilador sabe que el valor de retorno de `getPet()` solo puede ser `Dog`, `Cat` o `null`. Si `getPet()` pudiera devolver cualquier subclase de `Pet`, la asignación no sería válida.

## Referencias

- [Clases selladas de Kotlin](https://kotlinlang.org/docs/reference/sealed-classes.html)
- [Clases selladas en Kotlin](https://medium.com/@BladeCoder/sealed-classes-in-kotlin-67861b4bfe7d)
- [Clases Selladas](https://antonioleiva.com/clases-selladas/)