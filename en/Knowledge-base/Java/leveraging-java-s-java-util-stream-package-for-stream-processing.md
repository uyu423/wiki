---
title: Leveraging Java's java.util.stream Package for Stream Processing
description: 
published: true
date: 2023-02-04T12:18:10.751Z
tags: 
editor: markdown
dateCreated: 2023-02-04T12:18:05.320Z
---

- [Aprovechamiento del paquete java.util.stream de Java para el procesamiento de transmisiones***Spanish** document is available*](/es/Knowledge-base/Java/leveraging-java-s-java-util-stream-package-for-stream-processing)
{.links-list}
- [利用 Java 的 java.util.stream 包进行流处理***Chinese Simplified** document is available*](/zh/Knowledge-base/Java/leveraging-java-s-java-util-stream-package-for-stream-processing)
{.links-list}
- [스트림 처리를 위한 Java의 java.util.stream 패키지 활용***Korean** document is available*](/ko/Knowledge-base/Java/leveraging-java-s-java-util-stream-package-for-stream-processing)
{.links-list}


# Leveraging Java's java.util.stream Package for Stream Processing

The java.util.stream package was introduced in Java 8 and has been gaining popularity ever since. It offers a concise and powerful way to process data collections.

In this article, we'll explore how to use the java.util.stream package to perform stream processing. We'll look at some common stream operations and show how they can be used to solve real-world problems.

## What is Stream Processing?

Stream processing is a way of processing data collections in a declarative way. A stream pipeline is a sequence of stream operations, each of which takes an input stream and produces an output stream.

The most basic stream operation is the filter operation. It takes a predicate (a function that returns a boolean) and produces a new stream that contains only the elements that satisfy the predicate.

For example, we can use the filter operation to find all the even numbers in a stream of integers:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> evenStream = stream.filter(i -> i % 2 == 0);
```

The java.util.stream package also provides the map operation. It takes a function that transforms an input element into an output element and produces a new stream that contains the transformed elements.

For example, we can use the map operation to transform a stream of integers into a stream of their square roots:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Double> squareRootStream = stream.map(i -> Math.sqrt(i));
```

## Stream Operations

There are many other stream operations in the java.util.stream package. We'll explore some of the most common ones.

### map

The map operation takes a function that transforms an input element into an output element and produces a new stream that contains the transformed elements.

For example, we can use the map operation to transform a stream of integers into a stream of their square roots:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Double> squareRootStream = stream.map(i -> Math.sqrt(i));
```

We can also use the map operation to transform a stream of strings into a stream of their lengths:

```java
Stream<String> stream = Stream.of("hello", "world");

Stream<Integer> lengthStream = stream.map(s -> s.length());
```

### flatMap

The flatMap operation takes a function that transforms an input element into an output stream and produces a new stream that contains the elements from the output streams of all the input elements.

This is best explained with an example. Say we have a stream of strings, and we want to find all the characters that appear in those strings. We can use the flatMap operation to do this:

```java
Stream<String> stream = Stream.of("hello", "world");

Stream<Character> characterStream = stream.flatMap(s -> {
  List<Character> characters = new ArrayList<>();
  
  for (char c : s.toCharArray()) {
    characters.add(c);
  }
  
  return characters.stream();
});
```

In the example above, we've used the flatMap operation to transform a stream of strings into a stream of characters.

### filter

The filter operation takes a predicate (a function that returns a boolean) and produces a new stream that contains only the elements that satisfy the predicate.

For example, we can use the filter operation to find all the even numbers in a stream of integers:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> evenStream = stream.filter(i -> i % 2 == 0);
```

We can also use the filter operation to find all the strings in a stream that start with the letter 'a':

```java
Stream<String> stream = Stream.of("apple", "banana", "cat", "dog");

Stream<String> filteredStream = stream.filter(s -> s.startsWith("a"));
```

### sorted

The sorted operation takes an optional comparator and produces a new stream that is sorted according to the given comparator. If no comparator is given, the elements are sorted in their natural order.

For example, we can use the sorted operation to sort a stream of integers in ascending order:

```java
Stream<Integer> stream = Stream.of(5, 3, 7, 1, 4, 2, 6);

Stream<Integer> sortedStream = stream.sorted();
```

We can also use the sorted operation to sort a stream of strings in descending order:

```java
Stream<String> stream = Stream.of("hello", "world", "this", "is", "a", "test");

Stream<String> sortedStream = stream.sorted((s1, s2) -> s2.compareTo(s1));
```

### distinct

The distinct operation produces a new stream that contains only the distinct elements from the input stream.

For example, we can use the distinct operation to remove duplicate elements from a stream:

```java
Stream<Integer> stream = Stream.of(1, 1, 2, 2, 3, 3, 4, 4, 5, 5);

Stream<Integer> distinctStream = stream.distinct();
```

### limit

The limit operation takes a long value and produces a new stream that is limited to the given number of elements.

For example, we can use the limit operation to create a stream that contains only the first five elements of another stream:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> limitedStream = stream.limit(5);
```

### skip

The skip operation takes a long value and produces a new stream that skips the given number of elements.

For example, we can use the skip operation to create a stream that contains all but the first five elements of another stream:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> skippedStream = stream.skip(5);
```

### reduce

The reduce operation takes two arguments: an initial value and a binary operator. The binary operator is applied to the initial value and the first element of the stream, then the result of that operation is used as the initial value for the next operation, and so on. The final result is the value of the last operation.

For example, we can use the reduce operation to find the sum of a stream of integers:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

int sum = stream.reduce(0, (i1, i2) -> i1 + i2);
```

We can also use the reduce operation to find the product of a stream of integers:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

int product = stream.reduce(1, (i1, i2) -> i1 * i2);
```

### collect

The collect operation takes a collector and produces a new stream that contains the elements of the input stream, processed by the collector.

A collector is a function that groups elements of the stream into a mutable data structure. For example, we can use the collect operation to group a stream of strings by their length:

```java
Stream<String> stream = Stream.of("hello", "world", "this", "is", "a", "test");

Map<Integer, List<String>> map = stream.collect(Collectors.groupingBy(s -> s.length()));
```

In the example above, we've used the collect operation to group the strings in the stream by their length. The result is a map from length to a list of strings of that length.

## Stream Processing Examples

Now that we've seen some of the most common stream operations, let's look at how they can be used to solve real-world problems.

### Word Count

Say we have a stream of strings that represent a document. We want to count the number of times each word appears in the document. We can use the stream processing operations we've seen to do this:

```java
Stream<String> stream = Stream.of("hello", "world", "this", "is", "a", "test");

Map<String, Long> map = stream.collect(Collectors.groupingBy(s -> s, Collectors.counting()));
```

In the example above, we've used the collect operation to group the strings in the stream by their value. The result is a map from string to the number of times that string appears in the stream.

### Prime Number Sieve

Say we have a stream of integers. We want to find all the prime numbers in the stream. We can use the stream processing operations we've seen to do this:

```java
Stream<Integer> stream = Stream.of(2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20);

List<Integer> primes = stream.filter(i -> {
  for (int j = 2; j < i; j++) {
    if (i % j == 0) {
      return false;
    }
  }
  
  return true;
}).collect(Collectors.toList());
```

In the example above, we've used the filter operation to find all the prime numbers in the stream. The result is a list of the prime numbers in the stream.

## Conclusion

In this article, we've seen how to use the java.util.stream package to perform stream processing. We've looked at some common stream operations and seen how they can be used to solve real-world problems.