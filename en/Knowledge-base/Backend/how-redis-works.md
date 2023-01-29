---
title: How Redis works
description: 
published: true
date: 2023-01-29T20:06:42.024Z
tags: 
editor: markdown
dateCreated: 2023-01-29T20:06:42.024Z
---


Redis is an open source, in-memory data structure store, used as a database, cache, and message broker. It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs, and geospatial indexes with radius queries. 

Redis has built-in replication, Lua scripting, LRU eviction, transactions, and different levels of on-disk persistence, and provides high availability via Redis Sentinel and automatic partitioning with Redis Cluster. 

### How Redis works

Redis works in a very simple way. It is an in-memory key-value store. You can think of it as a hash table or a dictionary. You can set a key and a value, and later retrieve the value by using the key. 

Redis also supports more complex data structures such as lists and sets. You can push values to a list or add members to a set. You can also retrieve values from a list or set by using their index or members.

Redis is very fast because it works in memory. This also means that it is not suitable for storing large amounts of data. For large amounts of data, you can use Redis in conjunction with a database such as MySQL.

Redis is also very simple to use. There are only a few commands that you need to learn in order to start using it. 

### Installation

Redis is very easy to install. You can download it from the official website or use a package manager such as apt-get.

Once you have installed Redis, you can start the server by running the redis-server command.

You can also use a Redis client to connect to the server. The redis-cli is the official Redis client.

### Commands

Redis supports a wide range of commands. The most basic commands are SET, GET, and DEL.

SET is used to set a key and a value. 

GET is used to retrieve the value of a key. 

DEL is used to delete a key.

Redis also supports more complex commands such as LPUSH, RPUSH, LRANGE, and SADD.

LPUSH is used to push a value to a list. 

RPUSH is used to push a value to a list from the right. 

LRANGE is used to retrieve a range of values from a list. 

SADD is used to add a member to a set.

You can find a full list of commands on the official website.

### Conclusion

Redis is a very simple, yet powerful, in-memory data structure store. It is easy to install and use. It supports a wide range of commands.