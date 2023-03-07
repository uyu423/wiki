---
title: Redis JSON Data Structures: Storing and Querying JSON Data in Redis
description: 
published: true
date: 2023-03-07T22:32:53.849Z
tags: 
editor: markdown
dateCreated: 2023-03-07T22:32:53.849Z
---

- [Redis JSON 데이터 구조: Redis에서 JSON 데이터 저장 및 쿼리***Korean** document is available*](/ko/Knowledge-base/NoSQL/redis-json-data-structures-storing-and-querying-json-data-in-redis)
{.links-list}

Redis JSON Data Structures: Storing and Querying JSON Data in Redis

Redis is an in-memory data structure store that can be used as a database, cache, and message broker. Redis JSON is a module that provides native support for JSON data structures in Redis. With Redis JSON, storing and querying JSON data in Redis has become easier than ever before. 

In this article, we will explore Redis JSON data structures and how they can be used to store and query JSON data in Redis.

## What is Redis JSON?

Redis JSON is a Redis module that adds support for JSON data structures in Redis. It allows you to store and query JSON data in Redis without having to serialize or deserialize it. 

The Redis JSON module provides a set of commands that can be used to manipulate JSON data structures. These commands allow you to store, retrieve, update, and delete JSON data in Redis. 

## Redis JSON Data Structures

Redis JSON data structures allow you to store JSON data in Redis as native data types. The Redis JSON module supports two types of JSON data structures:

- JSON Object
- JSON Array

### JSON Object

A JSON object is a collection of key-value pairs. In Redis JSON, a JSON object is stored as a Redis hash. Each key-value pair in the JSON object is stored as a field-value pair in the Redis hash.

To store a JSON object in Redis, you can use the `JSON.SET` command. The following example shows how to store a JSON object in Redis using the `JSON.SET` command:

```{python}
JSON.SET user:id1234 '{"name":"John Doe","email":"johndoe@example.com"}'
```

In the above example, we are storing a JSON object that represents a user in Redis. The JSON object has two key-value pairs: `name` and `email`. The `JSON.SET` command is used to store this JSON object in Redis as a hash with the key `user:id1234`.

To retrieve a JSON object from Redis, you can use the `JSON.GET` command. The following example shows how to retrieve the JSON object we stored earlier using the `JSON.GET` command:

```{python}
JSON.GET user:id1234
```

In the above example, the `JSON.GET` command is used to retrieve the JSON object we stored earlier. The output of the command will be the JSON object as a string.

### JSON Array

A JSON array is an ordered list of values. In Redis JSON, a JSON array is stored as a Redis list. Each value in the JSON array is stored as an element in the Redis list.

To store a JSON array in Redis, you can use the `JSON.SET` command. The following example shows how to store a JSON array in Redis using the `JSON.SET` command:

```{python}
JSON.SET users '["John Doe","Jane Doe","Bob Smith"]'
```

In the above example, we are storing a JSON array that represents a list of users in Redis. The JSON array has three values: `John Doe`, `Jane Doe`, and `Bob Smith`. The `JSON.SET` command is used to store this JSON array in Redis as a list with the key `users`.

To retrieve a JSON array from Redis, you can use the `JSON.GET` command. The following example shows how to retrieve the JSON array we stored earlier using the `JSON.GET` command:

```{python}
JSON.GET users
```

In the above example, the `JSON.GET` command is used to retrieve the JSON array we stored earlier. The output of the command will be the JSON array as a string.

## Querying Redis JSON Data Structures

Redis JSON provides a set of commands that can be used to query JSON data structures in Redis. These commands allow you to search for and retrieve specific values from JSON data structures.

### JSON.GET

The `JSON.GET` command can be used to retrieve a JSON object or a JSON array from Redis. The command takes a key as an argument and returns the JSON data structure as a string.

### JSON.MGET

The `JSON.MGET` command can be used to retrieve multiple JSON objects or JSON arrays from Redis. The command takes multiple keys as arguments and returns the JSON data structures as an array of strings.

### JSON.TYPE

The `JSON.TYPE` command can be used to determine the type of a JSON data structure in Redis. The command takes a key as an argument and returns the type of the JSON data structure as a string (`object` or `array`).

### JSON.NUMBEROF

The `JSON.NUMBEROF` command can be used to retrieve the number of elements in a JSON array in Redis. The command takes a key as an argument and returns the number of elements as an integer.

### JSON.ARRINDEX

The `JSON.ARRINDEX` command can be used to retrieve the index of a value in a JSON array in Redis. The command takes a key, a value, and an optional starting index as arguments and returns the index of the value as an integer.

### JSON.OBJKEYS

The `JSON.OBJKEYS` command can be used to retrieve the keys of a JSON object in Redis. The command takes a key as an argument and returns the keys as an array of strings.

### JSON.OBJLEN

The `JSON.OBJLEN` command can be used to retrieve the number of fields in a JSON object in Redis. The command takes a key as an argument and returns the number of fields as an integer.

### JSON.OBJKEYEXISTS

The `JSON.OBJKEYEXISTS` command can be used to determine if a key exists in a JSON object in Redis. The command takes a key and a field as arguments and returns `true` if the field exists and `false` otherwise.

## Conclusion

Redis JSON is a powerful module that provides native support for JSON data structures in Redis. It allows you to store and query JSON data in Redis without having to serialize or deserialize it. Redis JSON data structures allow you to store JSON data in Redis as native data types, which makes it easy to manipulate JSON data in Redis. 

We hope this article has provided you with a good understanding of Redis JSON data structures and how they can be used to store and query JSON data in Redis. 

## External Resources

- [Redis JSON Documentation](https://redislabs.com/redis-json/)
- [Redis JSON API Reference](https://oss.redislabs.com/redisjson/commands/)
- [Redis Documentation](https://redis.io/documentation)