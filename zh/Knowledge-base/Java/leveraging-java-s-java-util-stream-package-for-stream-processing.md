---
title: 利用 Java 的 java.util.stream 包进行流处理
description: 
published: true
date: 2023-02-04T12:18:07.085Z
tags: 
editor: markdown
dateCreated: 2023-02-04T12:18:05.314Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Leveraging Java's java.util.stream Package for Stream Processing***English** document is available*](/en/Knowledge-base/Java/leveraging-java-s-java-util-stream-package-for-stream-processing)
{.links-list}


# 利用 Java 的 java.util.stream 包进行流处理

java.util.stream 包是在 Java 8 中引入的，从那时起就越来越受欢迎。它提供了一种简洁而强大的方式来处理数据集合。

在本文中，我们将探索如何使用 java.util.stream 包来执行流处理。我们将研究一些常见的流操作，并展示如何使用它们来解决实际问题。

## 什么是流处理？

流处理是一种以声明方式处理数据集合的方式。流管道是一系列流操作，每个操作接受一个输入流并产生一个输出流。

最基本的流操作是过滤操作。它接受一个谓词（一个返回布尔值的函数）并生成一个新流，该流只包含满足该谓词的元素。

例如，我们可以使用过滤操作来查找整数流中的所有偶数：

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> evenStream = stream.filter(i -> i % 2 == 0);
```

java.util.stream 包也提供了映射操作。它采用将输入元素转换为输出元素并生成包含转换元素的新流的函数。

例如，我们可以使用 map 操作将整数流转换为平方根流：

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Double> squareRootStream = stream.map(i -> Math.sqrt(i));
```

## 流操作

java.util.stream 包中还有许多其他的流操作。我们将探索一些最常见的。

### 地图

映射操作采用将输入元素转换为输出元素的函数，并生成包含转换后元素的新流。

例如，我们可以使用 map 操作将整数流转换为平方根流：

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Double> squareRootStream = stream.map(i -> Math.sqrt(i));
```

我们还可以使用 map 操作将字符串流转换为它们长度的流：

```java
Stream<String> stream = Stream.of("hello", "world");

Stream<Integer> lengthStream = stream.map(s -> s.length());
```

### 平面地图

flatMap 操作采用将输入元素转换为输出流的函数，并生成一个新流，其中包含所有输入元素的输出流中的元素。

这最好用一个例子来解释。假设我们有一个字符串流，我们想要找到出现在这些字符串中的所有字符。我们可以使用 flatMap 操作来做到这一点：

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

在上面的示例中，我们使用了 flatMap 操作将字符串流转换为字符流。

### 筛选

过滤器操作接受一个谓词（一个返回布尔值的函数）并生成一个新流，该流仅包含满足该谓词的元素。

例如，我们可以使用过滤操作来查找整数流中的所有偶数：

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> evenStream = stream.filter(i -> i % 2 == 0);
```

我们还可以使用过滤操作来查找流中以字母 'a' 开头的所有字符串：

```java
Stream<String> stream = Stream.of("apple", "banana", "cat", "dog");

Stream<String> filteredStream = stream.filter(s -> s.startsWith("a"));
```

### 排序

排序操作采用可选比较器并生成根据给定比较器排序的新流。如果没有给出比较器，则元素按其自然顺序排序。

例如，我们可以使用 sorted 操作按升序对整数流进行排序：

```java
Stream<Integer> stream = Stream.of(5, 3, 7, 1, 4, 2, 6);

Stream<Integer> sortedStream = stream.sorted();
```

我们还可以使用 sorted 操作按降序对字符串流进行排序：

```java
Stream<String> stream = Stream.of("hello", "world", "this", "is", "a", "test");

Stream<String> sortedStream = stream.sorted((s1, s2) -> s2.compareTo(s1));
```

### 清楚的

distinct 操作生成一个新流，其中仅包含来自输入流的不同元素。

例如，我们可以使用 distinct 操作从流中删除重复元素：

```java
Stream<Integer> stream = Stream.of(1, 1, 2, 2, 3, 3, 4, 4, 5, 5);

Stream<Integer> distinctStream = stream.distinct();
```

### 限制

limit 操作采用 long 值并生成一个新的流，该流被限制为给定数量的元素。

例如，我们可以使用限制操作来创建一个仅包含另一个流的前五个元素的流：

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> limitedStream = stream.limit(5);
```

### 跳过

skip 操作采用 long 值并生成一个跳过给定数量的元素的新流。

例如，我们可以使用 skip 操作来创建一个流，其中包含另一个流的前五个元素以外的所有元素：

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> skippedStream = stream.skip(5);
```

### 减少

reduce 操作有两个参数：一个初始值和一个二元运算符。二元运算符应用于初始值和流的第一个元素，然后该操作的结果用作下一个操作的初始值，依此类推。最后的结果就是上次操作的值。

例如，我们可以使用 reduce 操作来查找整数流的总和：

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

int sum = stream.reduce(0, (i1, i2) -> i1 + i2);
```

我们还可以使用 reduce 操作来查找整数流的乘积：

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

int product = stream.reduce(1, (i1, i2) -> i1 * i2);
```

### 收集

collect 操作采用收集器并生成一个新流，其中包含由收集器处理的输入流的元素。

收集器是一种将流的元素分组为可变数据结构的函数。例如，我们可以使用 collect 操作按长度对字符串流进行分组：

```java
Stream<String> stream = Stream.of("hello", "world", "this", "is", "a", "test");

Map<Integer, List<String>> map = stream.collect(Collectors.groupingBy(s -> s.length()));
```

在上面的示例中，我们使用 collect 操作按长度对流中的字符串进行分组。结果是从 length 到该长度字符串列表的映射。

## 流处理示例

现在我们已经了解了一些最常见的流操作，让我们看看如何使用它们来解决实际问题。

### 字数

假设我们有一个表示文档的字符串流。我们要计算每个单词在文档中出现的次数。我们可以使用我们已经看到的流处理操作来做到这一点：

```java
Stream<String> stream = Stream.of("hello", "world", "this", "is", "a", "test");

Map<String, Long> map = stream.collect(Collectors.groupingBy(s -> s, Collectors.counting()));
```

在上面的示例中，我们使用 collect 操作按值对流中的字符串进行分组。结果是从字符串到该字符串在流中出现的次数的映射。

### 素数筛

假设我们有一个整数流。我们想找到流中的所有质数。我们可以使用我们已经看到的流处理操作来做到这一点：

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

在上面的示例中，我们使用过滤操作来查找流中的所有素数。结果是流中素数的列表。

## 结论

在本文中，我们了解了如何使用 java.util.stream 包来执行流处理。我们已经研究了一些常见的流操作，并了解了如何使用它们来解决实际问题。