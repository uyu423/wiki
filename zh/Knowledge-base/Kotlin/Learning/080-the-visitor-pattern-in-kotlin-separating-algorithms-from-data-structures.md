---
title: 080：Kotlin 中的访问者模式：将算法与数据结构分离
description: 
published: true
date: 2023-02-17T06:32:49.499Z
tags: 
editor: markdown
dateCreated: 2023-02-17T06:32:41.104Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [080: The Visitor Pattern in Kotlin: Separating Algorithms from Data Structures***English** document is available*](/en/Knowledge-base/Kotlin/Learning/080-the-visitor-pattern-in-kotlin-separating-algorithms-from-data-structures)
{.links-list}


# Kotlin 中的访问者模式：将算法与数据结构分离

Kotlin 是一种功能强大的编程语言，可为软件开发提供许多功能。其中一个特征是访问者模式，这是一种将算法与数据结构分开的方法。

访问者模式适用于需要对数据结构执行不同操作但又不想更改结构本身的情况。例如，您可能想要打印出数据结构的内容，或者计算结构中所有值的总和。

使用访问者模式，您可以将这些算法编写为单独的访问者类，然后将它们应用于数据结构。这种关注点分离使您更容易理解和维护您的代码。

## 应用访问者模式

让我们通过一个例子来了解访问者模式是如何工作的。假设我们有一个表示数学表达式的数据结构，例如“3 + 4 * 5”。这个表达式可以用一棵树来表示，“+”节点是根，“3”节点是左孩子，“*”节点是右孩子。

![表情树](https://i.imgur.com/RYjrCz7.png)

我们可以定义一个 `node` 类来表示这棵树：

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

树中的每个节点都有一个“左”和“右”子节点，但“NumberNode”除外，它有一个“值”。所有节点都有一个 `accept` 方法，它接受一个 `visitor` 对象，并以该节点作为参数调用访问者的 `visit` 方法。

我们现在可以定义一个 `visitor` 接口，它对每种类型的节点都有一个 `visit` 方法：

```kotlin
interface Visitor {
    fun visit(node: AddNode)
    fun visit(node: MultiplyNode)
    fun visit(node: NumberNode)
}
```

最后，我们可以编写一个 `calculate` 访问器，它计算树所表示的表达式的值：

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

此访问者通过将其左右子节点的值相加来计算 AddNode 的值，对于 MultiplyNode 也是如此。对于“NumberNode”，它只返回“value”字段。

我们现在可以创建一个 expression 树的实例并计算它的值：

```kotlin
val tree = AddNode(
    MultiplyNode(NumberNode(3), NumberNode(4)),
    NumberNode(5)
)

val visitor = CalculateVisitor()
val result = tree.accept(visitor)

println(result) // prints 23
```

## 访问者模式的优点

与其他将算法与数据结构分离的方法相比，访问者模式有几个优点。

首先，访问者模式非常灵活。您可以定义任意数量的访问者，每个访问者可以对数据结构执行不同的任务。

其次，访问者模式易于扩展。如果需要在数据结构中添加新类型的节点，只需在访问者接口中添加一个新的 `visit` 方法，现有的所有访问者都将使用新的节点类型。

第三，访问者模式易于调试。如果其中一个访问者存在错误，则很容易隔离问题，因为访问者是与数据结构分开的类。

## 访问者模式的缺点

使用访问者模式也有一些缺点。

首先，访问者模式可能很慢。这是因为需要在数据结构中的每个节点上调用 accept 方法，这可能需要时间。

其次，访问者模式可能难以理解。这是因为很难跟踪哪个访问者在做什么。

## 何时使用访问者模式

访问者模式是一个强大的工具，但它并不适合所有情况。当您需要对数据结构执行不同的操作但又不想更改结构本身时，您应该使用访问者模式。

## 附加信息

- [维基百科：访客模式](https://en.wikipedia.org/wiki/Visitor_pattern)
- [Kotlinlang：访客模式](https://kotlinlang.org/docs/reference/type-safe-builders.html# visitor-pattern)

## 外部资源

- [JavaWorld：访问者设计模式](https://www.javaworld.com/article/2077578/learn-object-oriented-design-the-visitor-design-pattern.html)
- [SourceMaking：访客模式](https://sourcemaking.com/design_patterns/visitor)