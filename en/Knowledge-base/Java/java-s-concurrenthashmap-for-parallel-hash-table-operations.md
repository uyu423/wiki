---
title: Java's ConcurrentHashMap for Parallel Hash Table Operations
description: 
published: true
date: 2023-02-25T07:33:08.803Z
tags: 
editor: markdown
dateCreated: 2023-02-25T07:33:07.379Z
---

- [병렬 해시 테이블 작업을 위한 Java의 ConcurrentHashMap***Korean** document is available*](/ko/Knowledge-base/Java/java-s-concurrenthashmap-for-parallel-hash-table-operations)
{.links-list}


# Java's ConcurrentHashMap for Parallel Hash Table Operations

Java's `ConcurrentHashMap` class provides a concurrent hash table implementation that is suitable for use in multi-threaded applications. This class offers better performance than the `synchronized` `HashMap` class in most situations, and can be used in a wide variety of concurrent applications.

## Overview

A hash table is a data structure that stores key-value pairs in an array, and uses a hash function to calculate the index at which each key should be stored. A hash function is a function that takes a key and calculates a numeric value, called a hash code, that can be used to index the array.

A concurrent hash table is a hash table that can be safely accessed by multiple threads concurrently. A concurrent hash table must be able to handle simultaneous updates by multiple threads without corrupting the data.

Java's `ConcurrentHashMap` class provides a concurrent hash table implementation. This class is a member of the `java.util.concurrent` package.

## Usage

### Creating a ConcurrentHashMap

You can create a `ConcurrentHashMap` by using the `ConcurrentHashMap` constructor, or by using the `of` method in the `java.util.Map` interface.

The `ConcurrentHashMap` constructor takes two parameters:

- The initial capacity of the map (i.e. the number of key-value pairs that can be stored in the map)
- The load factor of the map (i.e. the maximum number of key-value pairs that can be stored in the map before it is resized)

The `of` method takes a variable number of key-value pairs and returns a `Map` object that contains those key-value pairs.

```java
// Construct a ConcurrentHashMap with an initial capacity of 10 and a load factor of 0.75
ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>(10, 0.75);

// Construct a ConcurrentHashMap with the key-value pairs {"A", 1}, {"B", 2}, and {"C", 3}
Map<String, Integer> map = Map.of("A", 1, "B", 2, "C", 3);
```

### Adding Data to a ConcurrentHashMap

You can add data to a `ConcurrentHashMap` by using the `put` or `putIfAbsent` methods.

The `put` method adds a key-value pair to the map, and returns the previous value associated with the key, or `null` if there was no previous value.

The `putIfAbsent` method adds a key-value pair to the map only if the key is not already present in the map. This method returns the previous value associated with the key, or `null` if there was no previous value.

```java
// Add the key-value pair ("A", 1) to the map
map.put("A", 1);

// Add the key-value pair ("B", 2) to the map only if the key "B" is not already present
map.putIfAbsent("B", 2);
```

### Retrieving Data from a ConcurrentHashMap

You can retrieve data from a `ConcurrentHashMap` by using the `get` or `getOrDefault` methods.

The `get` method returns the value associated with a given key, or `null` if the key is not present in the map.

The `getOrDefault` method returns the value associated with a given key, or a default value if the key is not present in the map.

```java
// Get the value associated with the key "A"
int value = map.get("A");

// Get the value associated with the key "B", or return 0 if the key is not present
int value = map.getOrDefault("B", 0);
```

### Updating Data in a ConcurrentHashMap

You can update data in a `ConcurrentHashMap` by using the `replace` or `compute` methods.

The `replace` method replaces the value associated with a given key with a new value. This method returns the previous value associated with the key, or `null` if there was no previous value.

The `compute` method takes a key and a function, and uses the function to compute a new value for the key. This method returns the new value.

```java
// Replace the value associated with the key "A" with the new value 2
int oldValue = map.replace("A", 2);

// Compute a new value for the key "B"
int newValue = map.compute("B", (k, v) -> (v == null) ? 1 : v + 1);
```

### Checking for the Presence of a Key or Value

You can check for the presence of a key or value in a `ConcurrentHashMap` by using the `containsKey` or `containsValue` methods.

The `containsKey` method returns `true` if the map contains a given key, and `false` otherwise.

The `containsValue` method returns `true` if the map contains a given value, and `false` otherwise.

```java
// Check if the key "A" is present in the map
boolean containsKey = map.containsKey("A");

// Check if the value 1 is present in the map
boolean containsValue = map.containsValue(1);
```

### Iterating Over a ConcurrentHashMap

You can iterate over the key-value pairs in a `ConcurrentHashMap` by using the `forEach` method.

The `forEach` method takes a function that takes a key and a value, and applies that function to each key-value pair in the map.

```java
// Iterate over the key-value pairs in the map and print each pair
map.forEach((k, v) -> System.out.println(k + "=" + v));
```

## Example

The following example demonstrates how to use the `ConcurrentHashMap` class to implement a simple multi-threaded dictionary. The dictionary is populated with English words and their definitions, and can be queried for the definition of a given word. The dictionary can be updated with new words and definitions.

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

## References

- [ConcurrentHashMap (Java Platform SE 8)](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentHashMap.html)
- [HashMap (Java Platform SE 8)](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html)
- [Map (Java Platform SE 8)](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html)