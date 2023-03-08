---
title: 026: Flujo de control avanzado en Kotlin: comprensión de las funciones with y apply
description: 
published: true
date: 2023-02-14T06:55:55.415Z
tags: 
editor: markdown
dateCreated: 2023-02-14T06:55:48.276Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [026: Advanced Control Flow in Kotlin: Understanding the with and apply Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/026-advanced-control-flow-in-kotlin-understanding-the-with-and-apply-functions)
{.links-list}


# 026: Flujo de control avanzado en Kotlin: comprensión de las funciones with y apply

Como programador de Kotlin, es importante comprender las diferentes formas de controlar el flujo de su programa. En esta publicación, veremos dos funciones que a menudo se usan juntas: with y apply. Aprenderemos cuándo y cómo usarlos, y veremos algunos ejemplos de cómo se pueden usar para mejorar nuestro código.

## ¿Qué son las funciones with y apply?

Las funciones with y apply son funciones que toman un receptor como argumento. El receptor es el objeto sobre el que se llama a la función. La función with devuelve el receptor, mientras que la función apply devuelve el resultado de la lambda que se le pasa.

## ¿Cuándo debo usar y aplicar?

Puede usar las funciones with y apply siempre que desee realizar varias operaciones en el mismo objeto. A menudo se usan juntos porque le permiten escribir código de manera concisa que sería más detallado si usara llamadas de función regulares.

Por ejemplo, digamos que tenemos una clase llamada Usuario con varias propiedades:

```kotlin
class User(
    val name: String,
    val age: Int,
    val address: String
)
```

Y tenemos una instancia de esta clase:

```kotlin
val user = User("John", 30, "123 Main Street")
```

Podemos usar la función with para realizar múltiples operaciones en el objeto del usuario:

```kotlin
with(user) {
    // do something with the user object
}
```

También podemos usar la función de aplicación para realizar múltiples operaciones en el objeto de usuario:

```kotlin
user.apply {
    // do something with the user object
}
```

## Ejemplos de Usar con y aplicar

Echemos un vistazo a algunos ejemplos de cómo podemos usar y aplicar para mejorar nuestro código.

### 1. Creación e inicialización de un objeto

Un caso de uso común para with y apply es crear e inicializar un objeto. Digamos que tenemos una clase llamada Car con varias propiedades:

```kotlin
class Car(
    val make: String,
    val model: String,
    val year: Int,
    val color: String
)
```

Podemos usar with para crear una nueva instancia de esta clase e inicializar sus propiedades:

```kotlin
val car = with(Car("Toyota", "Camry", 2020, "red")) {
    // do something with the car object
}
```

También podemos usar apply para crear una nueva instancia de esta clase e inicializar sus propiedades:

```kotlin
val car = Car("Toyota", "Camry", 2020, "red").apply {
    // do something with the car object
}
```

### 2. Acceso y modificación de propiedades

Otro caso de uso común para with y apply es acceder y modificar las propiedades de un objeto. Digamos que tenemos una clase llamada Persona con varias propiedades:

```kotlin
class Person(
    var name: String,
    var age: Int,
    var address: String
)
```

Y tenemos una instancia de esta clase:

```kotlin
val person = Person("John", 30, "123 Main Street")
```

Podemos usar with para acceder y modificar las propiedades del objeto persona:

```kotlin
with(person) {
    name = "Jane"
    age = 31
    address = "456 Main Street"
}
```

También podemos usar apply para acceder y modificar las propiedades del objeto persona:

```kotlin
person.apply {
    name = "Jane"
    age = 31
    address = "456 Main Street"
}
```

### 3. Llamar a múltiples métodos en un objeto

Otro caso de uso común para with y apply es llamar a varios métodos en el mismo objeto. Digamos que tenemos una clase llamada Empleado con varios métodos:

```kotlin
class Employee(
    val name: String,
    val age: Int,
    val address: String
) {
    fun work() {
        // do some work
    }

    fun takeBreak() {
        // take a break
    }

    fun goHome() {
        // go home
    }
}
```

Y tenemos una instancia de esta clase:

```kotlin
val employee = Employee("John", 30, "123 Main Street")
```

Podemos usar with para llamar a varios métodos en el objeto empleado:

```kotlin
with(employee) {
    work()
    takeBreak()
    goHome()
}
```

También podemos usar apply para llamar a varios métodos en el objeto empleado:

```kotlin
employee.apply {
    work()
    takeBreak()
    goHome()
}
```

## Información adicional

Aquí hay algunos recursos adicionales para obtener más información sobre las funciones with y apply:

- La función with es una función de orden superior que se declara en la biblioteca estándar de Kotlin [aquí](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-with/index.html).
- La función de aplicación es una función miembro de la clase Cualquiera que se declara [aquí](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-any/apply.html).
- Las funciones with y apply se describen en la documentación de Kotlin [aquí](https://kotlinlang.org/docs/reference/lambdas.html# with-and-apply).

## Conclusión

En esta publicación, hemos aprendido sobre las funciones with y apply. Hemos visto cuándo y cómo usarlos, y hemos visto algunos ejemplos de cómo se pueden usar para mejorar nuestro código.