---
title: [JavaScript] 038: Collision Resolution Techniques (Chaining, Open Addressing, etc.)
description: 
published: true
date: 2023-02-10T16:32:37.313Z
tags: 
editor: markdown
dateCreated: 2023-02-10T16:32:30.723Z
---

- [[JavaScript] 038: Técnicas de resolución de colisiones (encadenamiento, direccionamiento abierto, etc.)***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-038-collision-resolution-techniques-chaining-open-addressing-etc-)
{.links-list}
- [[JavaScript] 038：冲突解决技术（链接、开放寻址等）***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-038-collision-resolution-techniques-chaining-open-addressing-etc-)
{.links-list}
- [[JavaScript] 038: 충돌 해결 기술(연쇄, 개방 주소 지정 등)***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-038-collision-resolution-techniques-chaining-open-addressing-etc-)
{.links-list}


# JavaScript 038: Collision Resolution Techniques (Chaining, Open Addressing, etc.)

In this post, we will be discussing collision resolution techniques in hash tables. When two keys map to the same hash value, a collision occurs. There are a few ways to resolve collisions, which we will go over in this post.

## Chaining

Chaining is a collision resolution technique where each slot in the hash table is a linked list. When a collision occurs, the key is added to the linked list at that slot.

![Chaining](https://upload.wikimedia.org/wikipedia/commons/6/6d/Hash_table_3_1_1_0_1_0_0_LL.svg)

To search for a key, we hash the key and go to the corresponding slot. Then, we search through the linked list at that slot for the key. The time complexity for both insertion and search is O(n), where n is the number of keys in the hash table.

One advantage of chaining is that it is easy to implement. Another advantage is that the hash table can be resized easily. To resize the hash table, we simply create a new hash table and insert all of the keys from the old hash table into the new hash table.

## Open Addressing

Open addressing is a collision resolution technique where keys are stored in the hash table itself. There are a few different methods for open addressing, which we will go over.

### Linear Probing

Linear probing is a method of open addressing where we look for the next empty slot in the hash table until we find an empty slot. If we reach the end of the hash table, we wrap around and continue from the beginning of the hash table.

![Linear Probing](https://upload.wikimedia.org/wikipedia/commons/d/d5/Hash_table_4_1_1_1_1_1_1_LP.svg)

To search for a key, we hash the key and go to the corresponding slot. If that slot is empty, we know the key is not in the hash table. If the slot is not empty, we compare the key at that slot to the key we are searching for. If they are not equal, we continue searching for the next slot. The time complexity for insertion is O(1), but the time complexity for search is O(n), where n is the number of keys in the hash table.

One advantage of linear probing is that it is easy to implement. Another advantage is that keys are evenly distributed in the hash table, so there are no empty slots.

### Quadratic Probing

Quadratic probing is a method of open addressing where we look for the next empty slot by adding 1, 4, 9, 16, 25, etc. to the hash value.

![Quadratic Probing](https://upload.wikimedia.org/wikipedia/commons/5/5f/Hash_table_5_1_1_1_1_1_1_QP.svg)

To search for a key, we hash the key and go to the corresponding slot. If that slot is empty, we know the key is not in the hash table. If the slot is not empty, we compare the key at that slot to the key we are searching for. If they are not equal, we continue searching for the next slot. The time complexity for insertion is O(1), but the time complexity for search is O(n), where n is the number of keys in the hash table.

One advantage of quadratic probing is that it is easy to implement. Another advantage is that keys are evenly distributed in the hash table, so there are no empty slots.

### Double Hashing

Double hashing is a method of open addressing where we use two hash functions to calculate the next slot.

![Double Hashing](https://upload.wikimedia.org/wikipedia/commons/4/4a/Hash_table_5_1_1_1_1_1_1_DH.svg)

To search for a key, we hash the key and go to the corresponding slot. If that slot is empty, we know the key is not in the hash table. If the slot is not empty, we compare the key at that slot to the key we are searching for. If they are not equal, we continue searching for the next slot. The time complexity for insertion is O(1), but the time complexity for search is O(n), where n is the number of keys in the hash table.

One advantage of double hashing is that it is easy to implement. Another advantage is that keys are evenly distributed in the hash table, so there are no empty slots.

## Conclusion

In this post, we discussed collision resolution techniques in hash tables. We went over chaining, linear probing, quadratic probing, and double hashing. Chaining is a technique where each slot in the hash table is a linked list. Open addressing is a technique where keys are stored in the hash table itself. Linear probing, quadratic probing, and double hashing are all methods of open addressing.