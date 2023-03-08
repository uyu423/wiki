---
title: How do Kotlin's lazy collection operations help performance?
description: 
published: true
date: 2023-02-17T18:00:14.972Z
tags: english, kotlin, lambda
editor: markdown
dateCreated: 2022-12-24T19:27:57.210Z
---

- [코틀린의 지연 계산(lazy) 컬렉션 연산은 성능에 어떻게 도움을 주는가?***Korean** version of this document is available*](/ko/dev/Kotlin/How-do-Kotlin-sequence-lazy-operations-help-performance)
{.links-list}

---

- In Kotlin, the `Sequence` class is a lazily evaluated collection of elements that can be transformed and filtered using various operations. The `Sequence` class is similar to the `Stream` class in Java, but it is more lightweight and has better support for functional programming concepts.

- One of the main advantages of the `Sequence` class is that it allows you to perform operations on the elements of a collection lazily, which can improve performance in certain cases. When you perform an operation on a `Sequence`, the operation is not actually executed until you start iterating over the elements of the `Sequence`. This means that the operation is only performed on the elements that are actually needed, which can be more efficient than performing the operation on the entire collection at once.

- Lazily evaluated collections, such as Kotlin's `Sequence` class, can improve performance by avoiding unnecessary work. When you perform an operation on a lazily evaluated collection, the operation is not actually executed until you start iterating over the elements of the collection. This means that the operation is only performed on the elements that are actually needed, which can be more efficient than performing the operation on the entire collection at once.

- For example, consider the following Kotlin code that generates a `Sequence` of the first 10,000 integers and filters out the even numbers:

```kotlin
val numbers = generateSequence(1) { it + 1 }.take(10000)
val evenNumbers = numbers.filter { it % 2 == 0 }
```

- In this example, the `generateSequence` function creates a `Sequence` that generates the integers from 1 to 10,000 lazily, one at a time. The `take` function is used to limit the Sequence to the first 10,000 elements. The filter function is used to filter out the even numbers from the `Sequence`.

- Because the Sequence is lazily evaluated, the filter operation is not actually performed until you start iterating over the Sequence. For example, you could iterate over the `Sequence` and print the even numbers using a for-loop:

```kotlin
for (n in evenNumbers) {
    println(n)
}
```

- In this case, the filter operation is only performed on the elements of the `Sequence` that are actually needed, which are the even numbers that are printed to the console. If you were to perform the filter operation on the entire collection of 10,000 elements at once, it would be less efficient because you would be performing the operation on many elements that are not needed.

- Overall, the `Sequence` class and its lazy operations can help improve performance by allowing you to perform operations on collections lazily and only on the elements that are actually needed. This can be particularly useful when working with large collections or when performing expensive operations on the elements of a collection.

> ***Yowu's Notes*** 😎
> It seems to be more effective in cases where you don't need to search or operate on all elements, such as `find`.
> ```kotlin
> println(listOf(1, 2, 3, 4).asSequence().map { it * it }. find { it > 3});
> // find elements greater than 3 in [1,2,3,4] squared [1,4,9,16]
> ```
> In the above case, in the case of Collection, '1\*1', '2\*2', '3\*3', '4\*4' are all calculated, and then element 4 beyond 3 is searched, but in the case of Sequence, one at a time. It seems to be saying that '3\*3' and '4\*4' are not calculated because each element is processed, which helps performance.

> ***Yowu's Notes 2*** 😎
> `Stream API` of Java also supports lazily evaluated collection.
>
> - Stream class in Java is a lazily evaluated collection of elements that can be transformed and filtered using various operations. Like Kotlin's Sequence class, the Stream class allows you to perform operations on the elements of a collection lazily, which can improve performance in certain cases.
> - When you perform an operation on a Stream, the operation is not actually executed until you start consuming the elements of the Stream, either by iterating over the elements or by using a terminal operation such as count, collect, or reduce . This means that the operation is only performed on the elements that are actually needed, which can be more efficient than performing the operation on the entire collection at once.

![kotlin.jpeg](/kotlin.jpeg =500x){.align-center}