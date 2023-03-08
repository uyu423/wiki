---
title: [C Language] 037: Hash Function
description: 
published: true
date: 2023-02-13T17:32:32.744Z
tags: 
editor: markdown
dateCreated: 2023-02-13T17:32:30.981Z
---

- [[Lenguaje C] 037: función hash***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-037-hash-function)
{.links-list}
- [[C语言]037：哈希函数***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-037-hash-function)
{.links-list}
- [[C언어] 037: 해시함수***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-037-hash-function)
{.links-list}


# Hash Function

A hash function is a mathematical function that converts a value into a hash, which is a fixed-size numerical value. Hash functions are used in various areas of computer science, such as data structures, cryptography, and information theory.

There are many different types of hash functions, but they all have one goal: to take some input data and map it to a small, fixed-size output. The output of a hash function is typically called a hash value, hash code, or simply a hash.

Hash functions are a critical part of many computer science applications. For example, hash tables are data structures that use hash functions to store and retrieve data. Hash functions are also used in cryptography for digital signatures and message authentication codes (MACs).

## How Hash Functions Work

To understand how hash functions work, let's look at a simple example. Suppose we have a list of student names and ID numbers, and we want to store this data in a hash table. We can use a hash function to map each student's name to an ID number.

To do this, we first need to choose a hash function. There are many different hash functions to choose from, but for this example, we'll use the modulo hash function. This function takes an input value and divides it by the size of the hash table. The remainder is the hash value.

For example, suppose the size of our hash table is 10. If we use the modulo hash function to map the student name "John Smith" to a hash value, we get the following:

```
Hash("John Smith") = ("John Smith" % 10) = 2
```

This means that the student name "John Smith" will be stored in slot 2 of the hash table.

We can use the same hash function to map the student name "Mary Johnson" to a hash value:

```
Hash("Mary Johnson") = ("Mary Johnson" % 10) = 3
```

This means that the student name "Mary Johnson" will be stored in slot 3 of the hash table.

## Choosing a Hash Function

There are many different hash functions to choose from. The most important criterion for a hash function is that it should be easy to compute. The modulo hash function we used in the previous example is a simple hash function, but it has some drawbacks.

First, the modulo hash function can only be used if the size of the hash table is a power of two. This is because the modulo operator only works on powers of two.

Second, the modulo hash function can produce a lot of collisions. A collision occurs when two or more input values are mapped to the same hash value. For example, if we use the modulo hash function to map the student names "John Smith" and "Jane Doe" to hash values, we get the following:

```
Hash("John Smith") = ("John Smith" % 10) = 2
Hash("Jane Doe") = ("Jane Doe" % 10) = 2
```

Both "John Smith" and "Jane Doe" are mapped to hash value 2, so we have a collision.

There are many ways to avoid collisions, but the most common way is to use a larger hash table. A larger hash table means that there are more slots for input values to be mapped to, so the chances of a collision are reduced.

## Hash Functions in Cryptography

Hash functions are also used in cryptography. For example, a digital signature is a hash value that is computed from some input data, such as a document. The signature is then encrypted with the sender's private key.

When the receiver gets the signature, they can decrypt it with the sender's public key. They can then compute the hash value of the input data and compare it to the decrypted signature. If the two values match, then the data has not been tampered with and it is safe to use.

Hash functions are also used in message authentication codes (MACs). A MAC is a hash value that is computed from some input data, such as a message, and a secret key. The MAC is then sent along with the message.

When the receiver gets the message, they can compute the MAC from the message and the secret key. They can then compare the computed MAC to the MAC that was sent along with the message. If the two MACs match, then the message has not been tampered with and it is safe to use.

## Conclusion

Hash functions are mathematical functions that map input values to hash values. Hash functions are used in various areas of computer science, such as data structures, cryptography, and information theory.

There are many different types of hash functions, but they all have one goal: to take some input data and map it to a small, fixed-size output. The output of a hash function is typically called a hash value, hash code, or simply a hash.

Hash functions are a critical part of many computer science applications. For example, hash tables are data structures that use hash functions to store and retrieve data. Hash functions are also used in cryptography for digital signatures and message authentication codes (MACs).