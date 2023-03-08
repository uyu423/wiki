---
title: 079: El patrón iterador en Kotlin: atravesando colecciones con una interfaz común
description: 
published: true
date: 2023-02-14T05:17:36.213Z
tags: 
editor: markdown
dateCreated: 2023-02-14T05:17:29.030Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [079: The Iterator Pattern in Kotlin: Traversing Collections with a Common Interface***English** document is available*](/en/Knowledge-base/Kotlin/Learning/079-the-iterator-pattern-in-kotlin-traversing-collections-with-a-common-interface)
{.links-list}


# El patrón iterador en Kotlin: atravesando colecciones con una interfaz común

El patrón de iterador es un patrón de diseño en el que se utiliza un iterador para atravesar un contenedor y acceder a los elementos del contenedor. El patrón de iterador se utiliza para proporcionar una forma de acceder secuencialmente a los elementos de un objeto agregado sin exponer la implementación subyacente.

Kotlin es un lenguaje de programación de tipo estático que se ejecuta en la máquina virtual de Java. Kotlin es un lenguaje conciso, seguro, interoperable y amigable con las herramientas. Es un proyecto de código abierto bajo la licencia Apache 2.0.

La biblioteca estándar de Kotlin proporciona un conjunto de iteradores estándar, que son interfaces que definen cómo iterar sobre una colección de elementos. Hay tres iteradores estándar en Kotlin:

- Iterador
- ListIterator
- MutableIterator

El patrón de iterador es una forma útil de recorrer una colección de Kotlin sin exponer la implementación subyacente. Mediante el uso de un iterador, podemos acceder a los elementos de una colección de Kotlin de forma secuencial y segura sin tener que preocuparnos por la implementación subyacente.

## Iteradores en Kotlin

En Kotlin, un iterador es un objeto que proporciona una forma de acceder a los elementos de una colección de forma secuencial. La biblioteca estándar de Kotlin proporciona un conjunto de iteradores estándar, que son interfaces que definen cómo iterar sobre una colección de elementos. Hay tres iteradores estándar en Kotlin:

- Iterador
- ListIterator
- MutableIterator

Un iterador tiene dos métodos: `hasNext()` y `next()`. El método `hasNext()` devuelve verdadero si hay otro elemento en la colección al que se puede acceder con el método `next()`. El método `next()` devuelve el siguiente elemento de la colección.

Podemos usar un iterador para iterar sobre cualquier colección de Kotlin, incluidas listas, conjuntos y mapas. Echemos un vistazo a cómo usar un iterador con una lista.


```kotlin
val list = listOf(1, 2, 3, 4, 5)
val iterator = list.iterator()

while (iterator.hasNext()) {
    println(iterator.next())
}
```

En el ejemplo anterior, creamos una lista de enteros y un iterador para la lista. Luego usamos el método `hasNext()` para verificar si hay más elementos en la lista a los que se puede acceder con el método `next()`. Si hay más elementos, imprimimos el elemento en la consola.

También podemos usar el método `forEach()` para iterar sobre una colección de Kotlin. El método `forEach()` toma una lambda como argumento y llama a la lambda para cada elemento de la colección.

```kotlin
val list = listOf(1, 2, 3, 4, 5)

list.forEach {
    println(it)
}
```

En el ejemplo anterior, creamos una lista de enteros y usamos el método `forEach()` para iterar sobre la lista. Pasamos una lambda al método `forEach()` que imprime cada elemento en la consola.

## Iteradores mutables en Kotlin

Un iterador mutable es un iterador que se puede usar para modificar la colección subyacente. La biblioteca estándar de Kotlin proporciona una interfaz `MutableIterator` que define cómo iterar y modificar una colección mutable de elementos.

Un iterador mutable tiene tres métodos: `hasNext()`, `next()` y `remove()`. Los métodos `hasNext()` y `next()` funcionan igual que para un iterador. El método `remove()` elimina el último elemento devuelto por el método `next()` de la colección subyacente.

Echemos un vistazo a cómo usar un iterador mutable con una lista.

```kotlin
val list = mutableListOf(1, 2, 3, 4, 5)
val iterator = list.iterator()

while (iterator.hasNext()) {
    val element = iterator.next()
    if (element % 2 == 0) {
        iterator.remove()
    }
}

println(list)
```

En el ejemplo anterior, creamos una lista mutable de enteros y un iterador mutable para la lista. Luego usamos el método `hasNext()` para verificar si hay más elementos en la lista a los que se puede acceder con el método `next()`. Si hay más elementos, obtenemos el elemento de la lista y comprobamos si es divisible por 2. Si lo es, lo eliminamos de la lista con el método `remove()`.

También podemos usar el método `forEach()` para iterar y modificar una colección de Kotlin. El método `forEach()` toma una lambda como argumento y llama a la lambda para cada elemento de la colección. La lambda tiene dos argumentos: el elemento y el índice del elemento.

```kotlin
val list = mutableListOf(1, 2, 3, 4, 5)

list.forEach { element, index ->
    if (element % 2 == 0) {
        list.removeAt(index)
    }
}

println(list)
```

En el ejemplo anterior, creamos una lista mutable de enteros y usamos el método `forEach()` para iterar sobre la lista. Pasamos una lambda al método `forEach()` que toma dos argumentos: el elemento y el índice del elemento. Si el elemento es divisible por 2, lo eliminamos de la lista con el método `removeAt()`.

## Conclusión

En este artículo, aprendimos sobre el patrón de iterador y cómo usar iteradores en Kotlin. También aprendimos sobre los iteradores mutables y cómo usarlos para modificar la colección subyacente.