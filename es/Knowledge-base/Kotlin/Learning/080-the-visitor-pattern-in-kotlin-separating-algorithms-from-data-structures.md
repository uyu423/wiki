---
title: 080: El patrón de visitante en Kotlin: separando algoritmos de estructuras de datos
description: 
published: true
date: 2023-02-17T06:32:49.499Z
tags: 
editor: markdown
dateCreated: 2023-02-17T06:32:41.120Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [080: The Visitor Pattern in Kotlin: Separating Algorithms from Data Structures***English** document is available*](/en/Knowledge-base/Kotlin/Learning/080-the-visitor-pattern-in-kotlin-separating-algorithms-from-data-structures)
{.links-list}


# El patrón de visitante en Kotlin: separando los algoritmos de las estructuras de datos

Kotlin es un poderoso lenguaje de programación que ofrece muchas funciones para el desarrollo de software. Una de esas características es el patrón de visitantes, que es una forma de separar los algoritmos de las estructuras de datos.

El patrón de visitante es útil para los casos en los que necesita realizar diferentes acciones en una estructura de datos, pero no desea cambiar la estructura en sí. Por ejemplo, es posible que desee imprimir el contenido de una estructura de datos o calcular la suma de todos los valores de la estructura.

Con el patrón de visitante, puede escribir estos algoritmos como clases de visitantes separadas y luego aplicarlos a la estructura de datos. Esta separación de preocupaciones facilita la comprensión y el mantenimiento de su código.

## Aplicando el patrón de visitante

Veamos cómo funciona el patrón de visitantes con un ejemplo. Supongamos que tenemos una estructura de datos que representa una expresión matemática, como `3 + 4 * 5`. Esta expresión se puede representar mediante un árbol, siendo el nodo `+` la raíz, el nodo `3` el hijo izquierdo y el nodo `*` el hijo derecho.

![árbol de expresiones](https://i.imgur.com/RYjrCz7.png)

Podemos definir una clase `nodo` para representar este árbol:

```kotlin
sealed class Node {
    abstract fun accept(visitor: Visitor)
}

class AddNode(val left: Node, val right: Node) : Node() {
    override fun accept(visitor: Visitor) {
        visitor.visit(this)
    }
}

class MultiplyNode(val left: Node, val right: Node) : Node() {
    override fun accept(visitor: Visitor) {
        visitor.visit(this)
    }
}

class NumberNode(val value: Int) : Node() {
    override fun accept(visitor: Visitor) {
        visitor.visit(this)
    }
}
```

Cada nodo en el árbol tiene un hijo 'izquierdo' y 'derecho', excepto el 'NumberNode', que tiene un 'valor'. Todos los nodos tienen un método 'aceptar', que toma un objeto 'visitante' y llama al método 'visitar' en el visitante con el nodo como argumento.

Ahora podemos definir una interfaz de "visitante", que tiene un método de "visita" para cada tipo de nodo:

```kotlin
interface Visitor {
    fun visit(node: AddNode)
    fun visit(node: MultiplyNode)
    fun visit(node: NumberNode)
}
```

Finalmente, podemos escribir un visitante `calculate`, que calcula el valor de la expresión representada por el árbol:

```kotlin
class CalculateVisitor : Visitor {
    override fun visit(node: AddNode) {
        val left = node.left.accept(this)
        val right = node.right.accept(this)
        return left + right
    }

    override fun visit(node: MultiplyNode) {
        val left = node.left.accept(this)
        val right = node.right.accept(this)
        return left * right
    }

    override fun visit(node: NumberNode) {
        return node.value
    }
}
```

Este visitante calcula el valor de un 'AddNode' sumando los valores de sus hijos izquierdo y derecho, y de manera similar para 'MultiplyNode'. Para `NumberNode`, simplemente devuelve el campo `value`.

Ahora podemos crear una instancia de nuestro árbol `expression` y calcular su valor:

```kotlin
val tree = AddNode(
    MultiplyNode(NumberNode(3), NumberNode(4)),
    NumberNode(5)
)

val visitor = CalculateVisitor()
val result = tree.accept(visitor)

println(result) // prints 23
```

## Ventajas del Patrón Visitante

El patrón de visitante tiene varias ventajas sobre otros enfoques para separar algoritmos de estructuras de datos.

Primero, el patrón de visitantes es muy flexible. Puede definir tantos visitantes como desee, y cada visitante puede realizar una tarea diferente en la estructura de datos.

En segundo lugar, el patrón de visitantes es fácil de extender. Si necesita agregar un nuevo tipo de nodo a la estructura de datos, simplemente puede agregar un nuevo método de `visita` a la interfaz de visitante, y todos los visitantes existentes trabajarán con el nuevo tipo de nodo.

En tercer lugar, el patrón de visitantes es fácil de depurar. Si hay un error en uno de los visitantes, es fácil aislar el problema, porque el visitante es una clase separada de la estructura de datos.

## Desventajas del Patrón Visitante

También hay algunas desventajas al usar el patrón de visitante.

Primero, el patrón de visitantes puede ser lento. Esto se debe a que el método "aceptar" debe llamarse en cada nodo de la estructura de datos, lo que puede llevar tiempo.

En segundo lugar, el patrón de visitantes puede ser difícil de entender. Esto se debe a que puede ser difícil hacer un seguimiento de qué visitante está haciendo qué.

## Cuándo usar el patrón de visitante

El patrón de visitantes es una herramienta poderosa, pero no es adecuada para todas las situaciones. Debe usar el patrón de visitante cuando necesite realizar diferentes acciones en una estructura de datos, pero no desee cambiar la estructura en sí.

## Información adicional

- [Wikipedia: Patrón de visitante](https://en.wikipedia.org/wiki/Visitor_pattern)
- [Kotlinlang: Patrón de visitante](https://kotlinlang.org/docs/reference/type-safe-builders.html# visitor-pattern)

## Recursos externos

- [JavaWorld: El patrón de diseño del visitante](https://www.javaworld.com/article/2077578/learn-object-oriented-design-the-visitor-design-pattern.html)
- [SourceMaking: Patrón de visitante](https://sourcemaking.com/design_patterns/visitor)