---
title: Using Redis in Nest.js
description: 
published: true
date: 2023-01-29T20:14:53.445Z
tags: 
editor: markdown
dateCreated: 2023-01-29T20:14:53.445Z
---

- [Nest.js에서 Redis 사용**Korean*** version of this document is available*](/ko/Knowledge-base/Backend/using-redis-in-nest-js)
{.links-list}

# Using Redis in Nest.js

Nest.js is a framework for building efficient, scalable Node.js server-side applications. It uses modern JavaScript, is built with TypeScript (preserves compatibility with pure JavaScript) and combines elements of OOP (Object Oriented Programming), FP (Functional Programming), and FRP (Functional Reactive Programming). Under the hood, Nest.js uses Express.js, but also can use Fastify as an alternative.

Redis is an open source (BSD licensed), in-memory data structure store, used as a database, cache and message broker. It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs and geospatial indexes with radius queries. Redis has built-in replication, Lua scripting, LRU eviction, transactions and different levels of on-disk persistence, and provides high availability via Redis Sentinel and automatic partitioning with Redis Cluster.

## Why use Redis with Nest.js?

Nest.js is a great framework for building efficient and scalable server-side applications. However, when it comes to working with data, Nest.js is not the most efficient solution. This is where Redis comes in.

Redis is an in-memory data structure store that is much faster than using a traditional database like MySQL. It also has built-in replication and high availability features. By using Redis with Nest.js, you can improve the performance of your application and make it more scalable.

## How to use Redis with Nest.js?

There are two ways to use Redis with Nest.js:

1. Use the @nestjs/redis module.

2. Use the redis package.

### Using the @nestjs/redis Module

The @nestjs/redis module is a wrapper around the redis package that makes it easy to use Redis with Nest.js. To use the @nestjs/redis module, you first need to install it:

```
npm install @nestjs/redis
```

Once the module is installed, you can use it in your Nest.js application by importing the RedisModule:

```javascript
import { Module } from '@nestjs/common';
import { RedisModule } from '@nestjs/redis';

@Module({
  imports: [
    RedisModule.forRoot({
      host: 'localhost',
      port: 6379,
    }),
  ],
})
export class AppModule {}
```

In the example above, we are configuring the RedisModule to use the local Redis instance. You can also specify a password if your Redis instance is password protected.

Once the RedisModule is imported, you can inject the RedisService into your Nest.js components:

```javascript
import { Component } from '@nestjs/common';
import { RedisService } from '@nestjs/redis';

@Component()
export class SomeComponent {
  constructor(private readonly redisService: RedisService) {}

  someMethod() {
    this.redisService.set('some key', 'some value');
  }
}
```

The RedisService provides methods for all the Redis commands. Refer to the [Redis documentation](https://redis.io/documentation) for a complete list of commands.

### Using the redis Package

If you don't want to use the @nestjs/redis module, you can use the redis package directly. To use the redis package, you first need to install it:

```
npm install redis
```

Once the package is installed, you can use it in your Nest.js application by importing the redis package:

```javascript
import * as redis from 'redis';

const client = redis.createClient({
  host: 'localhost',
  port: 6379,
});

client.set('some key', 'some value');
```

In the example above, we are creating a Redis client and using it to set a key/value pair. Refer to the [redis package documentation](https://www.npmjs.com/package/redis) for a complete list of commands.

## Conclusion

In this article, we have seen how to use Redis with Nest.js. We have also seen two different ways to use Redis with Nest.js: using the @nestjs/redis module or using the redis package directly.