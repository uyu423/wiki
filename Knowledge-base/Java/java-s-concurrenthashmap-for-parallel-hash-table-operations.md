---
title: 병렬 해시 테이블 작업을 위한 Java의 ConcurrentHashMap
description: 
published: true
date: 2023-02-25T07:33:15.235Z
tags: 
editor: markdown
dateCreated: 2023-02-25T07:33:07.378Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Java's ConcurrentHashMap for Parallel Hash Table Operations***English** document is available*](/en/Knowledge-base/Java/java-s-concurrenthashmap-for-parallel-hash-table-operations)
{.links-list}


# 병렬 해시 테이블 작업을 위한 Java의 ConcurrentHashMap

Java의 `ConcurrentHashMap` 클래스는 다중 스레드 응용 프로그램에서 사용하기에 적합한 동시 해시 테이블 구현을 제공합니다. 이 클래스는 대부분의 상황에서 `synchronized` `HashMap` 클래스보다 더 나은 성능을 제공하며 다양한 동시 응용 프로그램에서 사용할 수 있습니다.

## 개요

해시 테이블은 키-값 쌍을 배열에 저장하는 데이터 구조이며 해시 함수를 사용하여 각 키가 저장되어야 하는 인덱스를 계산합니다. 해시 함수는 키를 사용하여 배열을 인덱싱하는 데 사용할 수 있는 해시 코드라는 숫자 값을 계산하는 함수입니다.

동시 해시 테이블은 여러 스레드에서 동시에 안전하게 액세스할 수 있는 해시 테이블입니다. 동시 해시 테이블은 데이터 손상 없이 여러 스레드의 동시 업데이트를 처리할 수 있어야 합니다.

Java의 `ConcurrentHashMap` 클래스는 동시 해시 테이블 구현을 제공합니다. 이 클래스는 `java.util.concurrent` 패키지의 멤버입니다.

## 용법

### ConcurrentHashMap 만들기

`ConcurrentHashMap` 생성자를 사용하거나 `java.util.Map` 인터페이스에서 `of` 메소드를 사용하여 `ConcurrentHashMap`을 생성할 수 있습니다.

`ConcurrentHashMap` 생성자는 두 개의 매개변수를 사용합니다.

- 맵의 초기 용량(즉, 맵에 저장할 수 있는 키-값 쌍의 수)
- 맵의 로드 팩터(즉, 크기를 조정하기 전에 맵에 저장할 수 있는 키-값 쌍의 최대 수)

`of` 메소드는 키-값 쌍의 가변 개수를 사용하고 해당 키-값 쌍을 포함하는 `Map` 개체를 반환합니다.

```java
// Construct a ConcurrentHashMap with an initial capacity of 10 and a load factor of 0.75
ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>(10, 0.75);

// Construct a ConcurrentHashMap with the key-value pairs {"A", 1}, {"B", 2}, and {"C", 3}
Map<String, Integer> map = Map.of("A", 1, "B", 2, "C", 3);
```

### ConcurrentHashMap에 데이터 추가

`put` 또는 `putIfAbsent` 메소드를 사용하여 `ConcurrentHashMap`에 데이터를 추가할 수 있습니다.

'put' 메서드는 키-값 쌍을 맵에 추가하고 키와 관련된 이전 값을 반환하거나 이전 값이 없는 경우 'null'을 반환합니다.

'putIfAbsent' 메서드는 키가 맵에 아직 없는 경우에만 키-값 쌍을 맵에 추가합니다. 이 메서드는 키와 관련된 이전 값을 반환하거나 이전 값이 없는 경우 'null'을 반환합니다.

```java
// Add the key-value pair ("A", 1) to the map
map.put("A", 1);

// Add the key-value pair ("B", 2) to the map only if the key "B" is not already present
map.putIfAbsent("B", 2);
```

### ConcurrentHashMap에서 데이터 가져오기

`get` 또는 `getOrDefault` 메소드를 사용하여 `ConcurrentHashMap`에서 데이터를 검색할 수 있습니다.

'get' 메서드는 주어진 키와 관련된 값을 반환하거나 키가 지도에 없으면 'null'을 반환합니다.

`getOrDefault` 메서드는 주어진 키와 관련된 값을 반환하거나 키가 맵에 없는 경우 기본값을 반환합니다.

```java
// Get the value associated with the key "A"
int value = map.get("A");

// Get the value associated with the key "B", or return 0 if the key is not present
int value = map.getOrDefault("B", 0);
```

### ConcurrentHashMap에서 데이터 업데이트

`replace` 또는 `compute` 메소드를 사용하여 `ConcurrentHashMap`의 데이터를 업데이트할 수 있습니다.

'replace' 메서드는 주어진 키와 관련된 값을 새 값으로 바꿉니다. 이 메서드는 키와 관련된 이전 값을 반환하거나 이전 값이 없는 경우 'null'을 반환합니다.

`compute` 메서드는 키와 함수를 사용하고 함수를 사용하여 키의 새 값을 계산합니다. 이 메서드는 새 값을 반환합니다.

```java
// Replace the value associated with the key "A" with the new value 2
int oldValue = map.replace("A", 2);

// Compute a new value for the key "B"
int newValue = map.compute("B", (k, v) -> (v == null) ? 1 : v + 1);
```

### 키 또는 값의 존재 확인

`containsKey` 또는 `containsValue` 메소드를 사용하여 `ConcurrentHashMap`에 키 또는 값이 있는지 확인할 수 있습니다.

`containsKey` 메서드는 맵에 주어진 키가 포함되어 있으면 `true`를 반환하고 그렇지 않으면 `false`를 반환합니다.

`containsValue` 메서드는 지도에 주어진 값이 포함되어 있으면 `true`를 반환하고 그렇지 않으면 `false`를 반환합니다.

```java
// Check if the key "A" is present in the map
boolean containsKey = map.containsKey("A");

// Check if the value 1 is present in the map
boolean containsValue = map.containsValue(1);
```

### ConcurrentHashMap 반복하기

`forEach` 메서드를 사용하여 `ConcurrentHashMap`에서 키-값 쌍을 반복할 수 있습니다.

'forEach' 메서드는 키와 값을 받는 함수를 사용하고 해당 함수를 맵의 각 키-값 쌍에 적용합니다.

```java
// Iterate over the key-value pairs in the map and print each pair
map.forEach((k, v) -> System.out.println(k + "=" + v));
```

## 예

다음 예제는 `ConcurrentHashMap` 클래스를 사용하여 간단한 다중 스레드 사전을 구현하는 방법을 보여줍니다. 사전은 영어 단어와 그 정의로 채워져 있으며 주어진 단어의 정의를 쿼리할 수 있습니다. 사전은 새로운 단어와 정의로 업데이트할 수 있습니다.

```java
import java.util.concurrent.ConcurrentHashMap;

public class Dictionary {
    // The map that stores the words and definitions
    private ConcurrentHashMap<String, String> map;
    
    public Dictionary() {
        // Create a new ConcurrentHashMap with an initial capacity of 10 and a load factor of 0.75
        map = new ConcurrentHashMap<>(10, 0.75);
        
        // Populate the map with some data
        map.put("dog", "a domestic animal");
        map.put("cat", "a small carnivorous mammal");
        map.put("mouse", "a small rodent");
    }
    
    public String getDefinition(String word) {
        // Get the definition of the given word, or return null if the word is not in the dictionary
        return map.get(word);
    }
    
    public void addWord(String word, String definition) {
        // Add a new word and definition to the dictionary
        map.put(word, definition);
    }
}
```

## 참조

- [ConcurrentHashMap(자바 플랫폼 SE 8)](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentHashMap.html)
- [HashMap(자바 플랫폼 SE 8)](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html)
- [맵(자바 플랫폼 SE 8)](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html)