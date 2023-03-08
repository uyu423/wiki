---
title: [C Language] 036: Hash Table
description: 
published: true
date: 2023-02-13T16:32:43.812Z
tags: 
editor: markdown
dateCreated: 2023-02-13T16:32:41.731Z
---

- [[Lenguaje C] 036: tabla hash***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-036-hash-table)
{.links-list}
- [[C语言]036：哈希表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-036-hash-table)
{.links-list}
- [[C언어] 036: 해시 테이블***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-036-hash-table)
{.links-list}


# Hash Table

A hash table is a data structure that stores data in an associative array format, where the keys are used to access the data values. A hash table uses a hashing function to generate a hash value for each key, which is used as an index to store the data value in the table.

Hash tables are used to implement associative arrays, which are data structures that store data in key-value pairs. In an associative array, the key is used to access the data value, much like a variable name is used to access a variable value.

Hash tables are used in many applications, such as database indexing, caches, and hash-based data structures.

## Overview

A hash table is a data structure that stores data in an associative array format, where the keys are used to access the data values.

A hash table uses a hashing function to generate a hash value for each key, which is used as an index to store the data value in the table.

Hash tables are used to implement associative arrays, which are data structures that store data in key-value pairs. In an associative array, the key is used to access the data value, much like a variable name is used to access a variable value.

Hash tables are used in many applications, such as database indexing, caches, and hash-based data structures.

## Hashing

A hash function is a function that takes a data value and generates a hash value, which is a numeric value used to index the data value in a hash table.

A good hash function should have the following properties:

- The hash function should be deterministic, which means that given the same data value, the hash function should always generate the same hash value.

- The hash function should be evenly distributed, which means that it should generate hash values that are evenly distributed across the range of possible values.

- The hash function should be collision resistant, which means that it should be difficult to find two data values that map to the same hash value.

There are many different hashing algorithms, but some of the more common ones are:

- Linear probing: This algorithm probes the hash table for the next available slot to store the data value.

- Quadratic probing: This algorithm probes the hash table using a quadratic function to find the next available slot to store the data value.

- Double hashing: This algorithm uses two hash functions to probe the hash table for the next available slot to store the data value.

## Hash Table Operations

Hash tables support the following operations:

- Insert: This operation inserts a data value into the hash table.

- Delete: This operation deletes a data value from the hash table.

- Search: This operation searches for a data value in the hash table.

- Update: This operation updates a data value in the hash table.

## Hash Table Implementation

Hash tables can be implemented using arrays or linked lists.

Array-based hash tables store the data values in an array, and the keys are used to index into the array.

Linked list-based hash tables store the data values in a linked list, and the keys are used to index into the linked list.

## Hash Table Applications

Hash tables are used in many applications, such as database indexing, caches, and hash-based data structures.

Database indexing is a process of storing data in a database in such a way that it can be retrieved quickly. Hash tables are often used to index data in databases.

Caches are data structures that store data in memory so that it can be accessed quickly. Hash tables are often used to implement caches.

Hash-based data structures are data structures that use hash functions to store data. Some examples of hash-based data structures are hash maps and hash sets.