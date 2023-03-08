---
title: 080: The Visitor Pattern in Kotlin: Separating Algorithms from Data Structures
description: 
published: true
date: 2023-02-17T06:32:43.792Z
tags: 
editor: markdown
dateCreated: 2023-02-17T06:32:41.675Z
---

- [080: El patrón de visitante en Kotlin: separando algoritmos de estructuras de datos***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/080-the-visitor-pattern-in-kotlin-separating-algorithms-from-data-structures)
{.links-list}
- [080：Kotlin 中的访问者模式：将算法与数据结构分离***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/080-the-visitor-pattern-in-kotlin-separating-algorithms-from-data-structures)
{.links-list}
- [080: Kotlin의 방문자 패턴: 데이터 구조에서 알고리즘 분리***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/080-the-visitor-pattern-in-kotlin-separating-algorithms-from-data-structures)
{.links-list}


# The Visitor Pattern in Kotlin: Separating Algorithms from Data Structures

Kotlin is a powerful programming language that offers many features for software development. One such feature is the visitor pattern, which is a way of separating algorithms from data structures.

The visitor pattern is useful for cases where you need to perform different actions on a data structure, but don't want to change the structure itself. For example, you might want to print out the contents of a data structure, or calculate the sum of all the values in the structure.

With the visitor pattern, you can write these algorithms as separate visitor classes, and then apply them to the data structure. This separation of concerns makes it easier to understand and maintain your code.

## Applying the Visitor Pattern

Let's see how the visitor pattern works by looking at an example. Suppose we have a data structure that represents a mathematical expression, such as `3 + 4 * 5`. This expression can be represented by a tree, with the `+` node being the root, the `3` node being the left child, and the `*` node being the right child.

![expression tree](https://i.imgur.com/RYjrCz7.png)

We can define a `node` class to represent this tree:

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

Each node in the tree has a `left` and `right` child, except for the `NumberNode`, which has a `value`. All nodes have an `accept` method, which takes a `visitor` object and calls the `visit` method on the visitor with the node as an argument.

We can now define a `visitor` interface, which has a `visit` method for each type of node:

```kotlin
interface Visitor {
    fun visit(node: AddNode)
    fun visit(node: MultiplyNode)
    fun visit(node: NumberNode)
}
```

Finally, we can write a `calculate` visitor, which calculates the value of the expression represented by the tree:

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

This visitor calculates the value of an `AddNode` by adding the values of its left and right children, and similarly for `MultiplyNode`. For `NumberNode`, it just returns the `value` field.

We can now create an instance of our `expression` tree and calculate its value:

```kotlin
val tree = AddNode(
    MultiplyNode(NumberNode(3), NumberNode(4)),
    NumberNode(5)
)

val visitor = CalculateVisitor()
val result = tree.accept(visitor)

println(result) // prints 23
```

## Advantages of the Visitor Pattern

The visitor pattern has several advantages over other approaches to separating algorithms from data structures.

First, the visitor pattern is very flexible. You can define as many visitors as you like, and each visitor can perform a different task on the data structure.

Second, the visitor pattern is easy to extend. If you need to add a new type of node to the data structure, you can just add a new `visit` method to the visitor interface, and all the existing visitors will work with the new node type.

Third, the visitor pattern is easy to debug. If there is a bug in one of the visitors, it's easy to isolate the problem, because the visitor is a separate class from the data structure.

## Disadvantages of the Visitor Pattern

There are also some disadvantages to using the visitor pattern.

First, the visitor pattern can be slow. This is because the `accept` method needs to be called on every node in the data structure, which can take time.

Second, the visitor pattern can be difficult to understand. This is because it can be hard to keep track of which visitor is doing what.

## When to Use the Visitor Pattern

The visitor pattern is a powerful tool, but it's not suitable for every situation. You should use the visitor pattern when you need to perform different actions on a data structure, but don't want to change the structure itself.

## Additional Information

- [Wikipedia: Visitor pattern](https://en.wikipedia.org/wiki/Visitor_pattern)
- [Kotlinlang: Visitor Pattern](https://kotlinlang.org/docs/reference/type-safe-builders.html#visitor-pattern)

## External Resources

- [JavaWorld: The visitor design pattern](https://www.javaworld.com/article/2077578/learn-object-oriented-design-the-visitor-design-pattern.html)
- [SourceMaking: Visitor Pattern](https://sourcemaking.com/design_patterns/visitor)