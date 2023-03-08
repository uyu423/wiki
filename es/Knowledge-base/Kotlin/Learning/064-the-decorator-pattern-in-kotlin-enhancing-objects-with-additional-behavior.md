---
title: 064: El patrón Decorator en Kotlin: mejora de objetos con comportamiento adicional
description: 
published: true
date: 2023-02-11T17:17:37.468Z
tags: 
editor: markdown
dateCreated: 2023-02-11T17:17:35.839Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [064: The Decorator Pattern in Kotlin: Enhancing Objects with Additional Behavior***English** document is available*](/en/Knowledge-base/Kotlin/Learning/064-the-decorator-pattern-in-kotlin-enhancing-objects-with-additional-behavior)
{.links-list}


# 064: El Patrón Decorador en Kotlin: Mejorando Objetos con Comportamiento Adicional

Kotlin es un poderoso lenguaje de programación que ofrece muchas funciones para que los desarrolladores las aprovechen. Una de esas características es el patrón decorador, que permite a los desarrolladores mejorar las clases existentes con un comportamiento adicional.

En esta publicación, veremos qué es el patrón decorador y cómo se puede usar en Kotlin. También exploraremos algunos ejemplos de cómo se puede usar el patrón decorador para agregar nuevas funciones a las clases existentes.

## ¿Qué es el Patrón Decorador?

El patrón decorador es un patrón de diseño que permite a los desarrolladores agregar un nuevo comportamiento a las clases existentes sin modificar la clase en sí. Esto se logra mediante la creación de una nueva clase que envuelve la clase existente y proporciona el nuevo comportamiento.

El patrón decorador se usa a menudo en la programación orientada a objetos para extender la funcionalidad de una clase sin tener que subclasificarla. Esto puede ser útil cuando desea agregar un nuevo comportamiento a una clase existente pero no desea modificar la clase en sí.

## ¿Cómo se usa el patrón Decorator en Kotlin?

En Kotlin, el patrón decorador generalmente se logra mediante la creación de una nueva clase que envuelve una clase existente y proporciona el nuevo comportamiento. Esta nueva clase a menudo se conoce como decorador.

Para usar el patrón decorador, primero debe crear una nueva clase que implemente la misma interfaz que la clase que desea decorar. Esta nueva clase también debe tener una referencia a la clase que está decorando.

A continuación, debe crear un método en la nueva clase que invoque el método que desea decorar. Este método también debe llamar al método en la clase que está decorando.

Finalmente, debe crear una instancia de la nueva clase y pasarle la instancia de la clase que desea decorar.

Aquí hay un ejemplo simple de cómo se puede usar el patrón decorador en Kotlin:

```kotlin
interface Shape {
    fun draw()
}

class Circle(val shape: Shape) : Shape {
    override fun draw() {
        println("Drawing a circle")
        shape.draw()
    }
}

fun main(args: Array<String>) {
    val circle = Circle(shape = Shape())
    circle.draw()
}
```

En este ejemplo, tenemos una interfaz Shape y una clase Circle que implementa la interfaz Shape. La clase Circle también tiene una referencia a la interfaz Shape.

También creamos un método en la clase Circle que invoca el método draw() en la interfaz Shape. Este método también llama al método draw() en la clase que está decorando.

Finalmente, creamos una instancia de la clase Circle y le pasamos la instancia de la interfaz Shape.

Cuando ejecutamos este código, obtenemos el siguiente resultado:

```
Drawing a circle
```

Como puede ver, el patrón decorador se puede usar para agregar un nuevo comportamiento a las clases existentes sin modificar la clase en sí.

## Patrón de decorador frente a herencia

Es importante tener en cuenta que el patrón de decorador es diferente de la herencia. La herencia es un mecanismo para crear nuevas clases a partir de clases existentes. La nueva clase hereda el comportamiento de la clase existente.

El patrón decorador, por otro lado, es una forma de agregar un nuevo comportamiento a una clase existente sin modificar la clase misma. El nuevo comportamiento se agrega mediante la creación de una nueva clase que envuelve la clase existente y proporciona el nuevo comportamiento.

## Patrón de decorador frente a composición

El patrón decorador a menudo se confunde con la composición. La composición es una forma de crear nuevas clases a partir de clases existentes. La nueva clase tiene referencias a la clase existente.

El patrón decorador, por otro lado, es una forma de agregar un nuevo comportamiento a una clase existente sin modificar la clase misma. El nuevo comportamiento se agrega mediante la creación de una nueva clase que envuelve la clase existente y proporciona el nuevo comportamiento.

## ¿Cuándo se debe usar el patrón Decorator?

El patrón decorador debe usarse cuando desee agregar un nuevo comportamiento a una clase existente sin modificar la clase en sí.

El patrón decorador se puede usar para agregar nuevas funciones a una clase existente sin cambiar el código de la clase. Esto puede ser útil cuando desea agregar un nuevo comportamiento a una clase existente pero no desea modificar la clase en sí.

El patrón decorador también se puede usar para agregar un nuevo comportamiento a una clase existente sin subclasificarla. Esto puede ser útil cuando desea agregar un nuevo comportamiento a una clase existente pero no desea crear una nueva subclase.

## Beneficios del Patrón Decorador

El patrón decorador tiene una serie de beneficios:

- El patrón decorador es una alternativa flexible a la herencia.

- El patrón decorador se puede usar para agregar un nuevo comportamiento a una clase existente sin modificar el código de la clase.

- El patrón decorador se puede usar para agregar un nuevo comportamiento a una clase existente sin subclasificarla.

- El patrón decorador es una forma de agregar un nuevo comportamiento a una clase existente sin cambiar la interfaz de la clase.

## Inconvenientes del patrón Decorator

El patrón decorador tiene algunos inconvenientes:

- El patrón decorador puede dificultar la comprensión del código.

- El patrón decorador puede dificultar el mantenimiento del código.

- El patrón decorador puede agregar mucha complejidad a una base de código.