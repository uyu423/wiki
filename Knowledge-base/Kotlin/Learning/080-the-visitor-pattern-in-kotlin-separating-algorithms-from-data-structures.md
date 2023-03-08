---
title: 080: Kotlin의 방문자 패턴: 데이터 구조에서 알고리즘 분리
description: 
published: true
date: 2023-02-17T06:32:49.499Z
tags: 
editor: markdown
dateCreated: 2023-02-17T06:32:41.104Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [080: The Visitor Pattern in Kotlin: Separating Algorithms from Data Structures***English** document is available*](/en/Knowledge-base/Kotlin/Learning/080-the-visitor-pattern-in-kotlin-separating-algorithms-from-data-structures)
{.links-list}


# Kotlin의 방문자 패턴: 데이터 구조에서 알고리즘 분리

Kotlin은 소프트웨어 개발을 위한 많은 기능을 제공하는 강력한 프로그래밍 언어입니다. 이러한 기능 중 하나는 데이터 구조에서 알고리즘을 분리하는 방법인 방문자 패턴입니다.

방문자 패턴은 데이터 구조에 대해 다른 작업을 수행해야 하지만 구조 자체는 변경하지 않으려는 경우에 유용합니다. 예를 들어 데이터 구조의 내용을 인쇄하거나 구조에 있는 모든 값의 합계를 계산할 수 있습니다.

방문자 패턴을 사용하면 이러한 알고리즘을 별도의 방문자 클래스로 작성한 다음 데이터 구조에 적용할 수 있습니다. 이러한 관심사 분리를 통해 코드를 더 쉽게 이해하고 유지 관리할 수 있습니다.

## 방문자 패턴 적용

예제를 통해 방문자 패턴이 어떻게 작동하는지 살펴보겠습니다. `3 + 4 * 5`와 같은 수학적 표현을 나타내는 데이터 구조가 있다고 가정합니다. 이 표현식은 루트가 되는 `+` 노드, 왼쪽 자식이 되는 `3` 노드 및 오른쪽 자식이 되는 `*` 노드가 있는 트리로 나타낼 수 있습니다.

![표현 트리](https://i.imgur.com/RYjrCz7.png)

이 트리를 나타내기 위해 `node` 클래스를 정의할 수 있습니다.

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

트리의 각 노드에는 `value`가 있는 `NumberNode`를 제외하고 `left` 및 `right` 자식이 있습니다. 모든 노드에는 `visitor` 개체를 사용하고 노드를 인수로 사용하여 방문자에 대해 `visit` 메서드를 호출하는 `accept` 메서드가 있습니다.

이제 각 노드 유형에 대한 `visit` 메서드가 있는 `visitor` 인터페이스를 정의할 수 있습니다.

```kotlin
interface Visitor {
    fun visit(node: AddNode)
    fun visit(node: MultiplyNode)
    fun visit(node: NumberNode)
}
```

마지막으로 트리가 나타내는 표현식의 값을 계산하는 'calculate' 방문자를 작성할 수 있습니다.

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

이 방문자는 'MultiplyNode'에 대해 왼쪽 및 오른쪽 자식의 값을 더하여 'AddNode'의 값을 계산합니다. `NumberNode`의 경우 `value` 필드만 반환합니다.

이제 `expression` 트리의 인스턴스를 만들고 그 값을 계산할 수 있습니다.

```kotlin
val tree = AddNode(
    MultiplyNode(NumberNode(3), NumberNode(4)),
    NumberNode(5)
)

val visitor = CalculateVisitor()
val result = tree.accept(visitor)

println(result) // prints 23
```

## 방문자 패턴의 장점

방문자 패턴은 데이터 구조에서 알고리즘을 분리하는 다른 접근 방식에 비해 몇 가지 장점이 있습니다.

첫째, 방문자 패턴은 매우 유연합니다. 원하는 만큼 방문자를 정의할 수 있으며 각 방문자는 데이터 구조에서 다른 작업을 수행할 수 있습니다.

둘째, 방문자 패턴은 확장하기 쉽습니다. 데이터 구조에 새 유형의 노드를 추가해야 하는 경우 방문자 인터페이스에 새 '방문' 메소드를 추가하기만 하면 모든 기존 방문자가 새 노드 유형으로 작업하게 됩니다.

셋째, 방문자 패턴은 디버그하기 쉽습니다. 방문자 중 하나에 버그가 있는 경우 방문자가 데이터 구조와 별도의 클래스이기 때문에 문제를 쉽게 격리할 수 있습니다.

## 방문자 패턴의 단점

또한 방문자 패턴을 사용하는 데는 몇 가지 단점이 있습니다.

첫째, 방문자 패턴이 느릴 수 있습니다. 데이터 구조의 모든 노드에서 'accept' 메서드를 호출해야 하기 때문에 시간이 걸릴 수 있습니다.

둘째, 방문자 패턴을 이해하기 어려울 수 있습니다. 어떤 방문자가 무엇을 하고 있는지 추적하기 어려울 수 있기 때문입니다.

## 방문자 패턴을 사용하는 경우

방문자 패턴은 강력한 도구이지만 모든 상황에 적합한 것은 아닙니다. 데이터 구조에 대해 다른 작업을 수행해야 하지만 구조 자체는 변경하지 않으려는 경우 방문자 패턴을 사용해야 합니다.

## 추가 정보

- [위키백과: 방문자 패턴](https://en.wikipedia.org/wiki/Visitor_pattern)
- [Kotlinlang: 방문자 패턴](https://kotlinlang.org/docs/reference/type-safe-builders.html# visitor-pattern)

## 외부 리소스

- [JavaWorld: 방문자 디자인 패턴](https://www.javaworld.com/article/2077578/learn-object-oriented-design-the-visitor-design-pattern.html)
- [소스메이킹: 방문자 패턴](https://sourcemaking.com/design_patterns/visitor)