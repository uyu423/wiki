---
title: [JavaScript] 036: Hash Table
description: 
published: true
date: 2023-02-10T14:33:11.430Z
tags: 
editor: markdown
dateCreated: 2023-02-10T14:33:04.739Z
---

- [[JavaScript] 036: tabla hash***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-036-hash-table)
{.links-list}
- [[JavaScript] 036：哈希表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-036-hash-table)
{.links-list}
- [[JavaScript] 036: 해시 테이블***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-036-hash-table)
{.links-list}


# JavaScript 036: Hash Table

In this post we will be discussing hash tables, a data structure that is used to store key-value pairs. We will cover the concept and theory behind hash tables, look at some code examples, and finish with some related exercises.

## What is a Hash Table?

A hash table is a data structure that stores key-value pairs. It is similar to an array, but the key is used to index the location of the value instead of a numerical index.

Hash tables are used to implement maps and sets. They are also used in many other applications such as caching, fast lookups, and more.

## How do Hash Tables Work?

Hash tables use a hash function to map keys to values. A hash function is a function that takes a key and maps it to a location in the hash table.

The location is called a bucket. A bucket is simply an array index.

The hash function is used to calculate the bucket for a given key. The function takes the key and calculates an array index based on the key. This index is used to store the value in the array.

## Why use Hash Tables?

Hash tables are fast. They have constant time insertion and lookup. This means that the time it takes to insert or lookup a value is independent of the size of the hash table.

Hash tables are also flexible. They can be used to implement many different data structures such as maps, sets, and more.

## Code Examples

Here is a simple hash table implementation in JavaScript.


```javascript
function HashTable(size) {
  this.buckets = new Array(size);
  this.numBuckets = this.buckets.length;
}

function HashNode(key, value, next) {
  this.key = key;
  this.value = value;
  this.next = next || null;
}

HashTable.prototype.hash = function(key) {
  var total = 0;
  for (var i = 0; i < key.length; i++) {
    total += key.charCodeAt(i);
  }
  var bucket = total % this.numBuckets;
  return bucket;
};

HashTable.prototype.insert = function(key, value) {
  var bucket = this.hash(key);
  if (!this.buckets[bucket]) {
    this.buckets[bucket] = new HashNode(key, value);
  }
  else if (this.buckets[bucket].key === key) {
    this.buckets[bucket].value = value;
  }
  else {
    var currentNode = this.buckets[bucket];
    while (currentNode.next) {
      if (currentNode.next.key === key) {
        currentNode.next.value = value;
        return;
      }
      currentNode = currentNode.next;
    }
    currentNode.next = new HashNode(key, value);
  }
};

HashTable.prototype.get = function(key) {
  var bucket = this.hash(key);
  if (!this.buckets[bucket]) {
    return null;
  }
  else {
    var currentNode = this.buckets[bucket];
    while (currentNode) {
      if (currentNode.key === key) {
        return currentNode.value;
      }
      currentNode = currentNode.next;
    }
    return null;
  }
};

HashTable.prototype.retrieveAll = function() {
  var allValues = [];
  for (var i = 0; i < this.numBuckets; i++) {
    var currentNode = this.buckets[i];
    while (currentNode) {
      allValues.push(currentNode.value);
      currentNode = currentNode.next;
    }
  }
  return allValues;
};

var myHT = new HashTable(30);

myHT.insert('dean', 'dean@gmail.com');
myHT.insert('megan', 'megan@gmail.com');
myHT.insert('dave', 'dave@gmail.com');
myHT.insert('jane', 'jane@gmail.com');
myHT.insert('mike', 'mike@gmail.com');
myHT.insert('sarah', 'sarah@gmail.com');
myHT.insert('john', 'john@gmail.com');

console.log(myHT.retrieveAll());
// ['dean@gmail.com', 'megan@gmail.com', 'dave@gmail.com', 'jane@gmail.com', 'mike@gmail.com', 'sarah@gmail.com', 'john@gmail.com']
```

In the code example above, we have created a HashTable class and a HashNode class. The HashTable class has a size property which is used to initialize the array. It also has a numBuckets property which is used to store the size of the array.

The HashNode class has a key, value, and next property. The key is used to store the key of the node, the value is used to store the value of the node, and the next property is used to store the next node in the linked list.

The HashTable class has a hash function which takes a key and maps it to a location in the array. The location is called a bucket. A bucket is simply an array index.

The HashTable class also has an insert function which takes a key and a value. It uses the hash function to calculate the bucket for the given key. If the bucket is empty, it creates a new HashNode and stores it in the bucket. If the bucket is not empty, it checks if the key already exists. If the key exists, it updates the value. If the key does not exist, it adds the new HashNode to the end of the linked list.

The HashTable class also has a get function which takes a key and returns the value for the given key. If the key does not exist, it returns null.

The HashTable class also has a retrieveAll function which returns an array of all values in the hash table.

## Exercises

1. Implement a hash table in your favorite programming language.

2. Write a function that takes a key and a value and inserts it into a hash table.

3. Write a function that takes a key and returns the value for the given key.

4. Write a function that returns an array of all values in the hash table.