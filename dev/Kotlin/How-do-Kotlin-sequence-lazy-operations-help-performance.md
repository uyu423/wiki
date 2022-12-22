---
title: 코틀린의 지연 계산(lazy) 컬렉션 연산은 성능에 어떻게 도움을 주는가?
description: 
published: true
date: 2022-12-22T10:51:04.290Z
tags: kotlin, lambda
editor: markdown
dateCreated: 2022-12-22T09:58:59.616Z
---

## Korean

- Kotlin에서 `Sequence` 클래스는 다양한 동작을 지원하여 변환 및 필터링할 수 있습니다. 또한 평가가 지연(lazily evaluated)됩니다. `Sequence` 클래스는 Java의 `Stream` 클래스와 비슷하지만 더 가볍고 함수형 프로그래밍 개념을 더 잘 지원합니다.

- `Sequence` 클래스의 주요 이점 중 하나는 컬렉션의 요소에 대한 작업을 느리게 수행(지연)할 수 있어 특정 상황에 성능을 향상시킬 수 있다는 것입니다. **`Sequence`에서 작업을 수행하면 `Sequence`의 요소에 대해 반복을 시작할 때까지 작업이 실제로 실행되지 않습니다.** 즉, 실제로 필요한 요소에 대해서만 작업이 수행되므로 전체 컬렉션에 대한 작업을 한 번에 수행하는 것보다 효율적일 수 있습니다.

- Kotlin의 `Sequence` 클래스와 같이 평가가 지연되는 컬렉션은 불필요한 작업을 피함으로써 성능을 향상시킬 수 있습니다. 평가가 지연된 컬렉션에서 작업을 수행하면 컬렉션의 요소에 대해 반복을 시작할 때까지 작업이 실제로 실행되지 않습니다. 즉, 실제로 필요한 요소에 대해서만 작업이 수행되므로 전체 컬렉션에 대한 작업을 한 번에 수행하는 것보다 효율적일 수 있습니다.

- 예를 들어, 처음 10,000개 정수의 `Sequence`를 생성하고 짝수를 필터링하는 다음 Kotlin 코드가 있습니다.

```kotlin
val numbers = generateSequence(1) { it + 1 }.take(10000)
val evenNumbers = numbers.filter { it % 2 == 0 }
```

- 이 예제에서 `generateSequence` 함수는 1에서 10,000까지의 정수를 1씩 증가시키며 `Sequence`를 생성합니다. `take` 함수는 `Sequence`를 처음 10,000개의 요소로 제한하는 데 사용됩니다. 필터 기능은 `Sequence`에서 짝수를 걸러내는 데 사용됩니다.

- `Sequence`는 평가가 지연(lazily evaluated)되기 때문에 `Sequence`에 대한 반복을 시작할 때까지 실제로 필터 작업이 수행되지 않습니다. 예를 들어 아래 코드는 `Sequence`를 반복하고 `for` 루프를 사용하여 짝수를 출력합니다.

```kotlin
for (n in evenNumbers) {
    println(n)
}
```

- 이 경우 실제로 필요한 `Sequence`의 요소, 즉 콘솔에 출력되는 짝수에 대해서만 필터 연산이 수행됩니다. 만약 `Sequence`가 아닌 `Collection`의 경우 10,000개 전체에 대해 필터 작업을 한 번에 수행하는 경우 **필요하지 않은 많은 요소에 대해 작업을 수행하게 되므로 효율성이 떨어집니다.**

- 전반적으로 `Sequence` 클래스와 그 지연 작업(lazy operations)은 실제로 필요한 요소에 대해서만 컬렉션에 대해 지연된 작업을 수행할 수 있도록 하여 성능을 향상시키는 데 도움이 될 수 있습니다. 이는 **대규모 컬렉션으로 작업하거나 컬렉션 요소에 대해 비용이 많이 드는 작업을 수행할 때 특히 유용할 수 있습니다.**

> ***요우의 사담*** 😎
> `find` 와 같이 모든 요소를 탐색하거나 연산할 필요가 없는 케이스에서 더 효과적일 것으로 보인다.
> ```kotlin
> println(listOf(1, 2, 3, 4).asSequence().map { it * it }.find { it > 3});
> // [1,2,3,4]의 제곱 [1,4,9,16] 에서 3을 넘는 요소를 찾는다.
> ```
> 위와 같은 경우에 `Collection` 의 경우 1\*1, 2\*2, 3\*3, 4\*4 을 모두 연산한 다음에 3을 넘는 요소 4 를 탐색하지만,
> `Sequence` 의 경우 한번에 하나의 요소씩 처리하기 때문에 3\*3, 4\*4 가 연산되지 않아 성능에 도움을 준다는 얘기처럼 보인다.

> ***요우의 사담 2*** 😎
> Java의 `Stream API`도 lazily evaluated collection 을 지원한다.
>
> - `Stream` class in Java is a lazily evaluated collection of elements that can be transformed and filtered using various operations. Like Kotlin's `Sequence` class, the `Stream` class allows you to perform operations on the elements of a collection lazily, which can improve performance in certain cases.
> 
> - When you perform an operation on a `Stream`, the operation is not actually executed until you start consuming the elements of the `Stream`, either by iterating over the elements or by using a terminal operation such as `count`, `collect`, or `reduce`. This means that the operation is only performed on the elements that are actually needed, which can be more efficient than performing the operation on the entire collection at once.

## English

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

![kotlin.jpeg](/kotlin.jpeg =500x){.align-center}