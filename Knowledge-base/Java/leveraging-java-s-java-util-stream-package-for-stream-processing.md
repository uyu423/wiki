---
title: 스트림 처리를 위한 Java의 java.util.stream 패키지 활용
description: 
published: true
date: 2023-02-04T12:18:07.026Z
tags: 
editor: markdown
dateCreated: 2023-02-04T12:18:05.311Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Leveraging Java's java.util.stream Package for Stream Processing***English** document is available*](/en/Knowledge-base/Java/leveraging-java-s-java-util-stream-package-for-stream-processing)
{.links-list}


# 스트림 처리를 위해 Java의 java.util.stream 패키지 활용

java.util.stream 패키지는 Java 8에서 도입되었으며 그 이후로 인기를 얻고 있습니다. 데이터 수집을 처리하는 간결하고 강력한 방법을 제공합니다.

이 기사에서는 java.util.stream 패키지를 사용하여 스트림 처리를 수행하는 방법을 살펴봅니다. 몇 가지 일반적인 스트림 작업을 살펴보고 실제 문제를 해결하는 데 사용할 수 있는 방법을 보여줍니다.

## 스트림 처리란?

스트림 처리는 선언적 방식으로 데이터 컬렉션을 처리하는 방법입니다. 스트림 파이프라인은 각각 입력 스트림을 받아 출력 스트림을 생성하는 일련의 스트림 작업입니다.

가장 기본적인 스트림 작업은 필터 작업입니다. 조건자(부울을 반환하는 함수)를 사용하고 조건자를 충족하는 요소만 포함하는 새 스트림을 생성합니다.

예를 들어 필터 작업을 사용하여 정수 스트림에서 모든 짝수를 찾을 수 있습니다.

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> evenStream = stream.filter(i -> i % 2 == 0);
```

java.util.stream 패키지는 맵 작업도 제공합니다. 입력 요소를 출력 요소로 변환하고 변환된 요소를 포함하는 새 스트림을 생성하는 함수를 사용합니다.

예를 들어 map 연산을 사용하여 정수 스트림을 제곱근 스트림으로 변환할 수 있습니다.

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Double> squareRootStream = stream.map(i -> Math.sqrt(i));
```

## 스트림 작업

java.util.stream 패키지에는 다른 많은 스트림 작업이 있습니다. 가장 일반적인 몇 가지를 살펴보겠습니다.

### 지도

맵 작업은 입력 요소를 출력 요소로 변환하고 변환된 요소를 포함하는 새 스트림을 생성하는 함수를 사용합니다.

예를 들어 map 연산을 사용하여 정수 스트림을 제곱근 스트림으로 변환할 수 있습니다.

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Double> squareRootStream = stream.map(i -> Math.sqrt(i));
```

또한 맵 작업을 사용하여 문자열 스트림을 해당 길이의 스트림으로 변환할 수 있습니다.

```java
Stream<String> stream = Stream.of("hello", "world");

Stream<Integer> lengthStream = stream.map(s -> s.length());
```

### 플랫맵

flatMap 작업은 입력 요소를 출력 스트림으로 변환하고 모든 입력 요소의 출력 스트림에서 요소를 포함하는 새 스트림을 생성하는 함수를 사용합니다.

이것은 예를 들어 가장 잘 설명됩니다. 문자열 스트림이 있고 해당 문자열에 나타나는 모든 문자를 찾고 싶다고 가정해 보겠습니다. flatMap 작업을 사용하여 이를 수행할 수 있습니다.

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

위의 예에서는 flatMap 작업을 사용하여 문자열 스트림을 문자 스트림으로 변환했습니다.

### 필터

필터 작업은 조건자(부울을 반환하는 함수)를 사용하고 조건자를 충족하는 요소만 포함하는 새 스트림을 생성합니다.

예를 들어 필터 작업을 사용하여 정수 스트림에서 모든 짝수를 찾을 수 있습니다.

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> evenStream = stream.filter(i -> i % 2 == 0);
```

필터 작업을 사용하여 문자 'a'로 시작하는 스트림의 모든 문자열을 찾을 수도 있습니다.

```java
Stream<String> stream = Stream.of("apple", "banana", "cat", "dog");

Stream<String> filteredStream = stream.filter(s -> s.startsWith("a"));
```

### 정렬됨

정렬 작업은 선택적 비교기를 사용하고 지정된 비교기에 따라 정렬되는 새 스트림을 생성합니다. 비교기가 제공되지 않으면 요소가 자연 순서대로 정렬됩니다.

예를 들어 정렬된 연산을 사용하여 정수 스트림을 오름차순으로 정렬할 수 있습니다.

```java
Stream<Integer> stream = Stream.of(5, 3, 7, 1, 4, 2, 6);

Stream<Integer> sortedStream = stream.sorted();
```

정렬된 작업을 사용하여 문자열 스트림을 내림차순으로 정렬할 수도 있습니다.

```java
Stream<String> stream = Stream.of("hello", "world", "this", "is", "a", "test");

Stream<String> sortedStream = stream.sorted((s1, s2) -> s2.compareTo(s1));
```

### 별개의

고유 연산은 입력 스트림의 고유 요소만 포함하는 새 스트림을 생성합니다.

예를 들어, 구별 작업을 사용하여 스트림에서 중복 요소를 제거할 수 있습니다.

```java
Stream<Integer> stream = Stream.of(1, 1, 2, 2, 3, 3, 4, 4, 5, 5);

Stream<Integer> distinctStream = stream.distinct();
```

### 한계

제한 작업은 긴 값을 사용하고 주어진 요소 수로 제한되는 새 스트림을 생성합니다.

예를 들어 limit 작업을 사용하여 다른 스트림의 처음 5개 요소만 포함하는 스트림을 만들 수 있습니다.

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> limitedStream = stream.limit(5);
```

### 건너뛰다

건너뛰기 작업은 긴 값을 사용하고 지정된 수의 요소를 건너뛰는 새 스트림을 생성합니다.

예를 들어 건너뛰기 작업을 사용하여 다른 스트림의 처음 5개 요소를 제외한 모든 요소를 포함하는 스트림을 만들 수 있습니다.

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> skippedStream = stream.skip(5);
```

### 줄이다

축소 작업은 초기 값과 이항 연산자라는 두 가지 인수를 사용합니다. 이진 연산자는 초기 값과 스트림의 첫 번째 요소에 적용된 다음 해당 작업의 결과가 다음 작업의 초기 값으로 사용되는 식입니다. 최종 결과는 마지막 작업의 값입니다.

예를 들어 축소 연산을 사용하여 정수 스트림의 합을 찾을 수 있습니다.

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

int sum = stream.reduce(0, (i1, i2) -> i1 + i2);
```

정수 스트림의 곱을 찾기 위해 축소 연산을 사용할 수도 있습니다.

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

int product = stream.reduce(1, (i1, i2) -> i1 * i2);
```

### 모으다

수집 작업은 수집기를 사용하고 수집기에 의해 처리되는 입력 스트림의 요소를 포함하는 새 스트림을 생성합니다.

수집기는 스트림의 요소를 변경 가능한 데이터 구조로 그룹화하는 기능입니다. 예를 들어 수집 작업을 사용하여 문자열 스트림을 길이별로 그룹화할 수 있습니다.

```java
Stream<String> stream = Stream.of("hello", "world", "this", "is", "a", "test");

Map<Integer, List<String>> map = stream.collect(Collectors.groupingBy(s -> s.length()));
```

위의 예에서는 수집 작업을 사용하여 스트림의 문자열을 길이별로 그룹화했습니다. 결과는 길이에서 해당 길이의 문자열 목록으로 매핑됩니다.

## 스트림 처리 예

이제 가장 일반적인 스트림 작업을 살펴보았으므로 실제 문제를 해결하는 데 어떻게 사용할 수 있는지 살펴보겠습니다.

### 단어 수

문서를 나타내는 문자열 스트림이 있다고 가정합니다. 각 단어가 문서에 나타나는 횟수를 세고 싶습니다. 이를 위해 우리가 본 스트림 처리 작업을 사용할 수 있습니다.

```java
Stream<String> stream = Stream.of("hello", "world", "this", "is", "a", "test");

Map<String, Long> map = stream.collect(Collectors.groupingBy(s -> s, Collectors.counting()));
```

위의 예에서는 값별로 스트림의 문자열을 그룹화하기 위해 수집 작업을 사용했습니다. 결과는 문자열에서 문자열이 스트림에 나타나는 횟수로의 매핑입니다.

### 소수 체

정수 스트림이 있다고 가정합니다. 스트림에서 모든 소수를 찾고 싶습니다. 이를 위해 우리가 본 스트림 처리 작업을 사용할 수 있습니다.

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

위의 예에서는 필터 작업을 사용하여 스트림에서 모든 소수를 찾았습니다. 결과는 스트림의 소수 목록입니다.

## 결론

이 기사에서는 java.util.stream 패키지를 사용하여 스트림 처리를 수행하는 방법을 살펴보았습니다. 몇 가지 일반적인 스트림 작업을 살펴보고 실제 문제를 해결하는 데 사용할 수 있는 방법을 확인했습니다.