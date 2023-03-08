---
title: [C Language] 038: Collision Resolution Techniques (Chaining, Open Addressing, etc.)
description: 
published: true
date: 2023-02-13T18:32:37.297Z
tags: 
editor: markdown
dateCreated: 2023-02-13T18:32:30.163Z
---

- [[Lenguaje C] 038: Técnicas de resolución de colisiones (encadenamiento, direccionamiento abierto, etc.)***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-038-collision-resolution-techniques-chaining-open-addressing-etc-)
{.links-list}
- [[C语言]038：冲突解决技术（Chaining、Open Addressing等）***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-038-collision-resolution-techniques-chaining-open-addressing-etc-)
{.links-list}
- [[C 언어] 038: 충돌 해결 기술(체인화, 개방 주소 지정 등)***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-038-collision-resolution-techniques-chaining-open-addressing-etc-)
{.links-list}


# Collision Resolution Techniques

## Introduction

In computer science, a collision is when two or more elements collide in a hash table. A hash table is a data structure that is used to store keys and values. When a key is hashed, the hash function will return an index that is used to store the key-value pair in the hash table. However, if two keys are hashed to the same index, then a collision occurs.

There are three main collision resolution techniques: chaining, open addressing, and double hashing. In this post, we will discuss each of these techniques in detail.

## Chaining

Chaining is a collision resolution technique that uses linked lists to store key-value pairs that have collided. When a key is hashed, the hash function will return an index. If the index is empty, then the key-value pair is simply stored at that index. However, if the index is already occupied, then the key-value pair is added to the linked list at that index.

The advantage of chaining is that it is easy to implement. The disadvantage of chaining is that it can lead to poor performance if the hash table becomes too full. This is because the linked lists will become very long, and it will take longer to find a specific key-value pair.

Here is an example of chaining in pseudocode:

```
function insert(key, value)
  index = hash(key)

  if table[index] is empty
    table[index] = key-value pair
  else
    add key-value pair to the linked list at table[index]
```

## Open Addressing

Open addressing is a collision resolution technique that uses probing to find an empty index to store a key-value pair. When a key is hashed, the hash function will return an index. If the index is empty, then the key-value pair is simply stored at that index. However, if the index is already occupied, then the key-value pair is stored at the next empty index.

The advantage of open addressing is that it can be faster than chaining if the hash table is not too full. The disadvantage of open addressing is that it can lead to poor performance if the hash table becomes too full. This is because the probing can become very slow as the hash table becomes full.

Here is an example of open addressing in pseudocode:

```
function insert(key, value)
  index = hash(key)

  while table[index] is occupied
    index = (index + 1) mod table.size

  table[index] = key-value pair
```

## Double Hashing

Double hashing is a collision resolution technique that uses two hash functions to find an empty index to store a key-value pair. When a key is hashed, the first hash function will return an index. If the index is empty, then the key-value pair is simply stored at that index. However, if the index is already occupied, then the key-value pair is hashed again with the second hash function. The second hash function will return another index, and the key-value pair is stored at that index.

The advantage of double hashing is that it can be faster than open addressing if the hash table is not too full. The disadvantage of double hashing is that it can lead to poor performance if the hash table becomes too full. This is because the second hash function can return the same index as the first hash function, which can lead to an infinite loop.

Here is an example of double hashing in pseudocode:

```
function insert(key, value)
  index = hash(key)
  index2 = hash2(key)

  while table[index] is occupied
    index = (index + index2) mod table.size

  table[index] = key-value pair
```

## Conclusion

In this post, we have discussed three collision resolution techniques: chaining, open addressing, and double hashing. Each of these techniques has its own advantages and disadvantages. Choose the technique that is right for your application.