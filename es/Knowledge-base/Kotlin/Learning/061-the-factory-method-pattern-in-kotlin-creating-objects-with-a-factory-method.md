---
title: 061: El patrón del método de fábrica en Kotlin: creación de objetos con un método de fábrica
description: 
published: true
date: 2023-02-16T22:32:31.224Z
tags: 
editor: markdown
dateCreated: 2023-02-16T22:32:29.909Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [061: The Factory Method Pattern in Kotlin: Creating Objects with a Factory Method***English** document is available*](/en/Knowledge-base/Kotlin/Learning/061-the-factory-method-pattern-in-kotlin-creating-objects-with-a-factory-method)
{.links-list}


# El patrón del método de fábrica en Kotlin: creación de objetos con un método de fábrica

En el desarrollo de software, el patrón de método de fábrica es un patrón de diseño creacional que utiliza métodos de fábrica para crear objetos. El patrón del método de fábrica es una forma de encapsular el código de creación de objetos para que no quede expuesto al código del cliente.

El patrón de método de fábrica también se conoce como patrón de constructor virtual.

## ¿Qué es un método de fábrica?

Un método de fábrica es un método estático que crea y devuelve un objeto. El objeto que devuelve el método de fábrica suele ser una instancia de una clase definida por el desarrollador.

El patrón del método de fábrica se usa a menudo cuando el desarrollador no quiere exponer los detalles del proceso de creación del objeto al código del cliente.

El patrón del método de fábrica también es útil cuando el desarrollador desea devolver objetos de diferentes tipos según los datos de entrada o el estado del sistema.

## ¿Cuándo usar el patrón del método de fábrica?

El patrón del método de fábrica se debe utilizar cuando

- el desarrollador quiere encapsular el código de creación del objeto.
- el desarrollador quiere devolver objetos de diferentes tipos según los datos de entrada o el estado del sistema.
- el desarrollador quiere devolver objetos creados por una biblioteca de terceros.

## ¿Cómo implementar el patrón del método de fábrica en Kotlin?

Kotlin no tiene un soporte integrado para el patrón de método de fábrica. Sin embargo, el patrón se puede implementar en Kotlin usando la palabra clave `object`.

La palabra clave `object` en Kotlin se usa para crear objetos singleton. Un objeto singleton es un objeto que solo puede tener una instancia.

Cuando se usa la palabra clave `object`, el compilador de Kotlin crea un campo estático en la clase generada y un método estático que devuelve la instancia del objeto.

La palabra clave `objeto` se puede usar para crear objetos que se pueden usar como métodos de fábrica.

Por ejemplo, considere una clase `Shape` que tiene un método `create`. El método `create` toma un parámetro `type` y devuelve un objeto de la clase `Shape`. El parámetro `type` se utiliza para determinar el tipo de objeto que devuelve el método `create`.

```kotlin
class Shape {
    companion object {
        fun create(type: String): Shape {
            return when (type) {
                "circle" -> Circle()
                "square" -> Square()
                else -> throw IllegalArgumentException("Unknown shape type")
            }
        }
    }
}
```

En el ejemplo anterior, el método `create` es un método estático que se define en el objeto complementario de la clase `Shape`. El método `create` toma un parámetro `type` y devuelve un objeto de la clase `Shape`.

El parámetro `type` se utiliza para determinar el tipo de objeto que devuelve el método `create`. Si el parámetro `type` es `"circle"`, entonces el método `create` devuelve una instancia de la clase `Circle`. Si el parámetro `tipo` es `"cuadrado"`, entonces el método `crear` devuelve una instancia de la clase `Cuadrado`.

El método `create` se puede utilizar como método de fábrica para crear objetos de la clase `Shape`.

```kotlin
val circle = Shape.create("circle")
val square = Shape.create("square")
```

En el ejemplo anterior, el método `create` se usa para crear una instancia de la clase `Circle` y una instancia de la clase `Square`.

## Ventajas del patrón del método de fábrica

El patrón del método de fábrica tiene las siguientes ventajas:

- El patrón del método de fábrica encapsula el código de creación del objeto.
- El patrón del método de fábrica permite al desarrollador devolver objetos de diferentes tipos según los datos de entrada o el estado del sistema.
- El patrón del método de fábrica permite al desarrollador devolver objetos creados por una biblioteca de terceros.

## Desventajas del patrón del método de fábrica

El patrón del método de fábrica tiene las siguientes desventajas:

- El patrón del método de fábrica puede dificultar la lectura y el mantenimiento del código.
- El patrón del método de fábrica puede dificultar la prueba del código.

## Recursos

- [Patrón de método de fábrica] (https://en.wikipedia.org/wiki/Factory_method_pattern)
- [Método de fábrica](https://kotlinlang.org/docs/reference/object-declarations.html# factory-method)
- [Cómo implementar el patrón del método de fábrica en Kotlin] (https://www.baeldung.com/kotlin-factory-method-pattern)