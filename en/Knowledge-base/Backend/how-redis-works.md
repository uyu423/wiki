---
title: How Redis works
description: 
published: true
date: 2023-01-29T20:05:04.358Z
tags: 
editor: markdown
dateCreated: 2023-01-29T20:05:04.358Z
---


Redis is a high performance in-memory key-value data store. It is often referred to as a data structure server since keys can contain strings, hashes, lists, sets and sorted sets. 

Redis is written in ANSI C and works in most POSIX systems like Linux, *BSD, OS X without external dependencies. A Redis server can also be installed and used on Windows with the help of Win32 port of Redis. 

Redis can be used as a database, cache and message broker and supports various programming languages such as C, C++, Java, Node.js, Python, Ruby, Go, and many more. 

> **Note:**
> Redis is not a relational database. It does not support SQL. 

## How Redis Works

Redis works in a simple way. It stores data in the form of key-value pairs. A key is a unique identifier for a value. A value can be a string, hash, list, set, or sorted set. 

When you set a key-value pair, Redis stores the value in its memory. When you get a value from Redis, it returns the value from its memory. 

Redis also supports various data structures such as lists, sets, and sorted sets. 

> **Note:**
> You can think of Redis as a giant hash table where you can store data in the form of key-value pairs. 

## How to Use Redis

Redis can be used as a database, cache, or message broker. It supports various programming languages such as C, C++, Java, Node.js, Python, Ruby, Go, and many more. 

To use Redis, you need to install the Redis server and client. The Redis server is written in ANSI C and works in most POSIX systems. The Redis client is available for various programming languages. 

Once you have installed the Redis server and client, you can start using Redis. 

> **Note:**
> You can find the installation instructions for the Redis server and client on the official website of Redis. 

## Commands in Redis

Redis supports various commands that can be used to store and retrieve data. 

Some of the most commonly used commands are SET, GET, EXPIRE, and KEYS. 

SET is used to set a key-value pair. 

GET is used to get the value of a key. 

EXPIRE is used to set a time limit for a key. After the time limit expires, the key is automatically deleted. 

KEYS is used to get a list of all keys. 

You can find the full list of commands on the official website of Redis. 

> **Warning:**
> Redis is a powerful tool. It is important to be familiar with the commands before using Redis. 

## Conclusion

Redis is a high performance in-memory key-value data store. It is often referred to as a data structure server. Redis is written in ANSI C and works in most POSIX systems. It can be used as a database, cache, or message broker. Redis supports various programming languages.