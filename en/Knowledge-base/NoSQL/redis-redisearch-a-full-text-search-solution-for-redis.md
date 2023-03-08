---
title: Redis RediSearch: A Full-Text Search Solution for Redis
description: 
published: true
date: 2023-03-04T05:32:33.715Z
tags: 
editor: markdown
dateCreated: 2023-03-04T05:32:32.329Z
---

- [Redis RediSearch: Redis용 전체 텍스트 검색 솔루션***Korean** document is available*](/ko/Knowledge-base/NoSQL/redis-redisearch-a-full-text-search-solution-for-redis)
{.links-list}
Redis RediSearch: A Full-Text Search Solution for Redis

Redis is an open-source, in-memory data structure store that is commonly used as a database, cache, and message broker. Redis has gained popularity over the years due to its simplicity, performance, and versatility. One of the most popular Redis modules is RediSearch, which provides robust full-text search capabilities to Redis.

## What is RediSearch?

RediSearch is a Redis module that enables full-text search capabilities on Redis. It is built on top of the Redis engine, which means that RediSearch can take advantage of Redis’s in-memory data structures and fast performance. RediSearch is a powerful and efficient search engine that can handle complex queries and return search results in microseconds.

## Why Use RediSearch?

If you are already using Redis as a database, cache, or message broker, then integrating RediSearch can add valuable full-text search capabilities to your application. RediSearch is particularly useful for applications that need to search and retrieve data quickly, such as e-commerce websites, social networking platforms, and content management systems.

RediSearch is also easy to configure and deploy. Redis already has a wide range of client libraries available in different programming languages, which makes it easy to integrate RediSearch into your existing application. Additionally, RediSearch can be used alongside other Redis modules, such as Redis Streams and Redis Graph, to create powerful data pipelines.

## Features of RediSearch

RediSearch offers several features that make it a great search engine for Redis:

### 1. Full-Text Search

RediSearch supports full-text search, which means that you can search for documents based on the text contained within them. RediSearch uses an inverted index to store the text data, which allows for fast and efficient search queries.

### 2. Auto-Completion

RediSearch also supports auto-completion, which is useful for applications that need to suggest search terms to users as they type. RediSearch can provide suggestions based on the search terms entered so far, making it easier for users to find what they are looking for.

### 3. Numeric Filters

RediSearch can also filter search results based on numeric values. This can be useful for applications that need to search for documents based on price, age, or other numerical data.

### 4. Geo Filtering

RediSearch can also filter search results based on geographical location. This is useful for applications that need to search for documents based on their proximity to a particular location.

### 5. Document Scoring

RediSearch assigns a score to each document based on its relevance to the search query. This can be useful for applications that need to sort or filter search results based on relevance.

## Using RediSearch

To use RediSearch, you first need to install the Redis server and the RediSearch module. You can then create an index and add documents to it. Here is an example of how to create an index and add documents to it using the Redis command-line interface:

```redis
127.0.0.1:6379> FT.CREATE myIndex SCHEMA title TEXT body TEXT
OK
127.0.0.1:6379> FT.ADD myIndex doc1 1.0 FIELDS title "Redis RediSearch" body "Redis RediSearch is a full-text search solution for Redis."
OK
127.0.0.1:6379> FT.ADD myIndex doc2 1.0 FIELDS title "Redis Streams" body "Redis Streams is a new data type introduced in Redis 5.0."
OK
```

In this example, we create an index called “myIndex” with two text fields: “title” and “body”. We then add two documents to the index, each with a unique ID and a score of 1.0.

To search the index, you can use the FT.SEARCH command. Here is an example of how to search the “myIndex” index for documents that contain the word “Redis”:

```redis
127.0.0.1:6379> FT.SEARCH myIndex "Redis"
1) (integer) 2
2) "doc2"
3) 1) "title"
   2) "Redis Streams"
   3) "body"
   4) "Redis Streams is a new data type introduced in Redis 5.0."
4) "doc1"
5) 1) "title"
   2) "Redis RediSearch"
   3) "body"
   4) "Redis RediSearch is a full-text search solution for Redis."
```

In this example, the search query returns two documents that contain the word “Redis”. The documents are ranked in order of relevance, with the most relevant document listed first.

## Conclusion

RediSearch is a powerful and efficient full-text search solution for Redis. It offers several features that make it a great search engine for applications that need to search and retrieve data quickly. RediSearch is easy to configure and deploy, and it can be used alongside other Redis modules to create powerful data pipelines.

If you are already using Redis, then integrating RediSearch into your application can add valuable full-text search capabilities. With its fast performance and robust search capabilities, RediSearch is a great choice for any application that needs to search and retrieve data quickly.

## External Resources

- [RediSearch Documentation](https://oss.redislabs.com/redisearch/)
- [Redis Documentation](https://redis.io/documentation)
- [Redis Gears: A Serverless Engine for Redis](https://redisgears.io/)