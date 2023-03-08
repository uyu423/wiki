---
title: 050: Patrones de diseño en Kotlin: aplicación de patrones de diseño comunes a su código.
description: 
published: true
date: 2023-02-16T16:32:51.071Z
tags: 
editor: markdown
dateCreated: 2023-02-16T16:32:48.682Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [050: Design Patterns in Kotlin: Applying Common Design Patterns to Your Code.***English** document is available*](/en/Knowledge-base/Kotlin/Learning/050-design-patterns-in-kotlin-applying-common-design-patterns-to-your-code-)
{.links-list}


# 050: Patrones de diseño en Kotlin: aplicación de patrones de diseño comunes a su código

Los patrones de diseño son una parte crucial del conjunto de herramientas de cualquier desarrollador de software. Proporcionan un lenguaje común que los desarrolladores pueden usar para comunicar soluciones a problemas comunes. Los patrones de diseño también ayudan a que el código sea más legible y fácil de mantener.

Kotlin es un lenguaje de programación moderno que está creciendo en popularidad. Es un gran lenguaje para aplicar patrones de diseño. En esta publicación, veremos algunos de los patrones de diseño más comunes y cómo aplicarlos en Kotlin.

## Patrones de creación

Los patrones creacionales se ocupan de la creación de objetos. Estos patrones ayudan a controlar el proceso de creación de objetos.

### Patrón de fábrica

El patrón de fábrica es un patrón de creación que se utiliza para crear objetos. El patrón de fábrica es útil cuando necesita crear objetos que sean del mismo tipo pero con datos diferentes.

Para crear un patrón de fábrica en Kotlin, necesitamos crear una clase que actúe como nuestra fábrica. Esta clase tendrá un método que creará objetos del tipo que especifiquemos.

```kotlin
class ObjectFactory {

 fun createObject(type: String): Any {

when (type) {
 "A" -> return ObjectA()
 "B" -> return ObjectB()
 else -> throw IllegalArgumentException("Unknown type")
}
}
}
```

Luego podemos usar nuestra fábrica para crear objetos de los tipos que necesitamos.

```kotlin
val factory = ObjectFactory()

val objectA = factory.createObject("A")
val objectB = factory.createObject("B")
```

El patrón de fábrica es una excelente manera de controlar la creación de objetos. También es una buena manera de mantener su código SECO (No se repita).

## Patrones estructurales

Los patrones estructurales se ocupan de la estructura de los objetos y de cómo se componen. Estos patrones nos ayudan a comprender mejor las relaciones entre los objetos.

### Patrón de adaptador

El patrón adaptador es un patrón estructural que se utiliza para adaptar una interfaz a otra. El patrón de adaptador es útil cuando necesita usar una clase existente pero su interfaz no coincide con la interfaz que necesita.

Para crear un patrón de adaptador en Kotlin, necesitamos crear una clase que actúe como nuestro adaptador. Esta clase implementará la interfaz que necesitamos y delegará las llamadas a la clase existente.

```kotlin
class Adapter(val existingClass: ExistingClass) : InterfaceX {

override fun method1() {
 existingClass.method1()
}

override fun method2() {
 existingClass.method2()
}
}
```

Luego podemos usar nuestro adaptador para acceder a los métodos de la clase existente.

```kotlin
val adapter = Adapter(existingClass)

adapter.method1()
adapter.method2()
```

El patrón de adaptador es una excelente manera de reutilizar el código existente. También es una buena manera de hacer que el código sea más legible y mantenible.

## Patrones de comportamiento

Los patrones de comportamiento están relacionados con el comportamiento de los objetos. Estos patrones nos ayudan a comprender mejor el comportamiento de los objetos y cómo interactúan entre sí.

### Patrón de observador

El patrón de observador es un patrón de comportamiento que se utiliza para definir una relación de uno a muchos entre objetos. El patrón de observador es útil cuando necesita notificar a varios objetos sobre cambios en un objeto en particular.

Para crear un patrón de observador en Kotlin, necesitamos crear una clase que actúe como nuestro sujeto. Esta clase tendrá un método para registrar observadores y un método para notificar cambios a los observadores.

```kotlin
class Subject {

private val observers = mutableListOf<Observer>()

fun registerObserver(observer: Observer) {
 observers.add(observer)
}

fun notifyObservers() {
 for (observer in observers) {
  observer.update()
 }
}
}
```

Entonces podemos usar nuestro tema para notificar a los observadores de los cambios.

```kotlin
val subject = Subject()

val observer1 = Observer1()
val observer2 = Observer2()

subject.registerObserver(observer1)
subject.registerObserver(observer2)

subject.notifyObservers()
```

El patrón de observador es una excelente manera de desacoplar objetos. También es una buena manera de hacer que el código sea más legible y mantenible.

## Conclusión

Los patrones de diseño son una parte crucial del conjunto de herramientas de cualquier desarrollador de software. Proporcionan un lenguaje común que los desarrolladores pueden usar para comunicar soluciones a problemas comunes. Los patrones de diseño también ayudan a que el código sea más legible y fácil de mantener.

Kotlin es un gran lenguaje para aplicar patrones de diseño. En esta publicación, hemos analizado algunos de los patrones de diseño más comunes y cómo aplicarlos en Kotlin.