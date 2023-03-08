---
title: 079: The Iterator Pattern in Kotlin: Traversing Collections with a Common Interface
description: 
published: true
date: 2023-02-14T05:17:31.019Z
tags: 
editor: markdown
dateCreated: 2023-02-14T05:17:29.034Z
---

- [079: El patrón iterador en Kotlin: atravesando colecciones con una interfaz común***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/079-the-iterator-pattern-in-kotlin-traversing-collections-with-a-common-interface)
{.links-list}
- [079：Kotlin 中的迭代器模式：使用通用接口遍历集合***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/079-the-iterator-pattern-in-kotlin-traversing-collections-with-a-common-interface)
{.links-list}
- [079: Kotlin의 반복자 패턴: 공통 인터페이스로 컬렉션 탐색***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/079-the-iterator-pattern-in-kotlin-traversing-collections-with-a-common-interface)
{.links-list}


# The Iterator Pattern in Kotlin: Traversing Collections with a Common Interface

The iterator pattern is a design pattern in which an iterator is used to traverse a container and access the container's elements. The iterator pattern is used to provide a way to access the elements of an aggregate object sequentially without exposing the underlying implementation.

Kotlin is a statically typed programming language that runs on the Java Virtual Machine. Kotlin is a concise, safe, interoperable, and tool-friendly language. It is an open source project under the Apache 2.0 license.

The Kotlin standard library provides a set of standard iterators, which are interfaces that define how to iterate over a collection of elements. There are three standard iterators in Kotlin:

- Iterator
- ListIterator
- MutableIterator

The iterator pattern is a useful way to traverse a Kotlin collection without exposing the underlying implementation. By using an iterator, we can access the elements of a Kotlin collection sequentially and safely without having to worry about the underlying implementation.

## Iterators in Kotlin

In Kotlin, an iterator is an object that provides a way to access the elements of a collection sequentially. Kotlin's standard library provides a set of standard iterators, which are interfaces that define how to iterate over a collection of elements. There are three standard iterators in Kotlin:

- Iterator
- ListIterator
- MutableIterator

An iterator has two methods: `hasNext()` and `next()`. The `hasNext()` method returns true if there is another element in the collection that can be accessed with the `next()` method. The `next()` method returns the next element in the collection.

We can use an iterator to iterate over any Kotlin collection, including lists, sets, and maps. Let's take a look at how to use an iterator with a list.


```kotlin
val list = listOf(1, 2, 3, 4, 5)
val iterator = list.iterator()

while (iterator.hasNext()) {
    println(iterator.next())
}
```

In the example above, we create a list of integers and an iterator for the list. We then use the `hasNext()` method to check if there are more elements in the list that can be accessed with the `next()` method. If there are more elements, we print the element to the console.

We can also use the `forEach()` method to iterate over a Kotlin collection. The `forEach()` method takes a lambda as an argument and calls the lambda for each element in the collection.

```kotlin
val list = listOf(1, 2, 3, 4, 5)

list.forEach {
    println(it)
}
```

In the example above, we create a list of integers and use the `forEach()` method to iterate over the list. We pass a lambda to the `forEach()` method that prints each element to the console.

## MutableIterators in Kotlin

A mutable iterator is an iterator that can be used to modify the underlying collection. Kotlin's standard library provides a `MutableIterator` interface that defines how to iterate over and modify a mutable collection of elements.

A mutable iterator has three methods: `hasNext()`, `next()`, and `remove()`. The `hasNext()` and `next()` methods work the same as they do for an iterator. The `remove()` method removes the last element that was returned by the `next()` method from the underlying collection.

Let's take a look at how to use a mutable iterator with a list.

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

In the example above, we create a mutable list of integers and a mutable iterator for the list. We then use the `hasNext()` method to check if there are more elements in the list that can be accessed with the `next()` method. If there are more elements, we get the element from the list and check if it is divisible by 2. If it is, we remove it from the list with the `remove()` method.

We can also use the `forEach()` method to iterate over and modify a Kotlin collection. The `forEach()` method takes a lambda as an argument and calls the lambda for each element in the collection. The lambda has two arguments: the element and the index of the element.

```kotlin
val list = mutableListOf(1, 2, 3, 4, 5)

list.forEach { element, index ->
    if (element % 2 == 0) {
        list.removeAt(index)
    }
}

println(list)
```

In the example above, we create a mutable list of integers and use the `forEach()` method to iterate over the list. We pass a lambda to the `forEach()` method that takes two arguments: the element and the index of the element. If the element is divisible by 2, we remove it from the list with the `removeAt()` method.

## Conclusion

In this article, we learned about the iterator pattern and how to use iterators in Kotlin. We also learned about mutable iterators and how to use them to modify the underlying collection.