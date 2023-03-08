---
title: 076: El patrón de objeto nulo en Kotlin: proporcionar un objeto no nulo en lugar de nulo
description: 
published: true
date: 2023-02-17T05:32:33.308Z
tags: 
editor: markdown
dateCreated: 2023-02-17T05:32:25.019Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [076: The Null Object Pattern in Kotlin: Providing a Non-Null Object in Place of Null***English** document is available*](/en/Knowledge-base/Kotlin/Learning/076-the-null-object-pattern-in-kotlin-providing-a-non-null-object-in-place-of-null)
{.links-list}


# El patrón de objeto nulo en Kotlin: proporcionar un objeto no nulo en lugar de nulo

El sistema de tipos de Kotlin está diseñado para eliminar la necesidad de valores nulos. Sin embargo, hay momentos en los que se requieren valores nulos, como cuando se interactúa con código heredado escrito en Java. En estos casos, el patrón de objeto nulo se puede utilizar para proporcionar un objeto no nulo en lugar de un valor nulo.

## ¿Qué es el patrón de objeto nulo?

El patrón de objeto nulo es un patrón de diseño que tiene como objetivo eliminar la necesidad de valores nulos. Lo hace proporcionando un objeto no nulo en lugar de un valor nulo. Este objeto no nulo se puede utilizar para representar la ausencia de un valor.

## ¿Cómo funciona el patrón de objeto nulo?

El patrón de objeto nulo funciona creando un objeto que representa la ausencia de un valor. Este objeto se puede utilizar en lugar de un valor nulo. Al objeto se le puede dar un valor predeterminado, como una cadena vacía, o se le puede dar un comportamiento que sea apropiado para la situación.

## ¿Cuándo se debe usar el patrón de objeto nulo?

El patrón de objeto nulo debe usarse cuando se requieren valores nulos, como cuando se interactúa con código heredado escrito en Java.

## ¿Cuáles son los beneficios del patrón de objeto nulo?

El patrón de objeto nulo tiene varios beneficios:

- Elimina la necesidad de valores nulos.
- Hace que el código sea más legible.
- Hace que el código sea más mantenible.
- Hace que el código sea más extensible.

## ¿Cuáles son los inconvenientes del patrón de objeto nulo?

El patrón de objeto nulo tiene un inconveniente:

- Puede agregar complejidad al código.

## Implementación de Kotlin

El patrón de objeto nulo se puede implementar en Kotlin siguiendo los siguientes pasos:

1. Cree una interfaz para el objeto.
2. Cree una clase que implemente la interfaz.
3. Crea un objeto que represente la ausencia de un valor.

### Paso 1: crear una interfaz para el objeto

El primer paso es crear una interfaz para el objeto. Esta interfaz definirá el contrato para el objeto.

```kotlin
interface MyInterface {
    fun doSomething()
}
```

### Paso 2: Cree una clase que implemente la interfaz

El segundo paso es crear una clase que implemente la interfaz. Esta clase proporcionará la implementación para el objeto.

```kotlin
class MyClass : MyInterface {
    override fun doSomething() {
        // do something
    }
}
```

### Paso 3: Cree un objeto que represente la ausencia de un valor

El tercer paso es crear un objeto que represente la ausencia de un valor. Este objeto se puede utilizar en lugar de un valor nulo.

```kotlin
object MyObject : MyInterface {
    override fun doSomething() {
        // do something
    }
}
```

## Uso

El patrón de objeto nulo se puede utilizar de la siguiente manera:

```kotlin
fun doSomething(myInterface: MyInterface?) {
    if (myInterface != null) {
        myInterface.doSomething()
    }
}

fun main() {
    val myClass: MyClass? = MyClass()
    val myObject: MyObject? = MyObject()

    doSomething(myClass)
    doSomething(myObject)
}
```

## Información adicional

- El patrón de objeto nulo también se conoce como patrón de objeto ficticio.

## Advertencias

- El patrón de objeto nulo solo debe usarse cuando se requieren valores nulos.

## Peligros

- El patrón de objeto nulo puede agregar complejidad al código.