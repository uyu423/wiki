---
title: Redis Geo: A Guide to Storing and Querying Geospatial Data in Redis
description: 
published: true
date: 2023-03-06T13:32:39.910Z
tags: 
editor: markdown
dateCreated: 2023-03-06T13:32:32.666Z
---

- [Redis Geo: Redis에서 지리 공간 데이터를 저장하고 쿼리하기 위한 가이드***Korean** document is available*](/ko/Knowledge-base/NoSQL/redis-geo-a-guide-to-storing-and-querying-geospatial-data-in-redis)
{.links-list}

Redis Geo: A Guide to Storing and Querying Geospatial Data in Redis

Redis is a key-value store that is widely used for caching and other applications. Redis is known for its high performance and scalability. Redis Geo is a module available in Redis that allows you to store and query geospatial data. In this guide, we will explore the Redis Geo module and how it can be used to store and query geospatial data in Redis.

## What is Redis Geo?

Redis Geo is a module available in Redis that provides geospatial indexing and querying capabilities. It allows you to store and query points on a map, and search for points within a certain distance of a given point. Redis Geo uses the Haversine formula to calculate distances between points on the earth's surface.

## How to use Redis Geo

To use Redis Geo, you need to enable the module in Redis. You can do this by adding the following line to your Redis configuration file:

```
# Load the Redis Geo module
loadmodule /path/to/redis-geo.so
```

Once you have enabled the module, you can start using the Redis Geo commands to store and query geospatial data.

### Storing geospatial data

To store geospatial data in Redis, you need to use the `GEOADD` command. The `GEOADD` command takes a key name, longitude, latitude, and member name as arguments. Here is an example:

```redis
GEOADD cities -122.4194 37.7749 SanFrancisco
```

In this example, we are storing the city of San Francisco with the longitude and latitude coordinates of -122.4194 and 37.7749, respectively. The key name is "cities", and the member name is "SanFrancisco".

You can also store multiple points at once. Here is an example:

```redis
GEOADD cities -122.4194 37.7749 SanFrancisco -118.2437 34.0522 LosAngeles
```

In this example, we are storing the cities of San Francisco and Los Angeles.

### Querying geospatial data

To query geospatial data in Redis, you need to use the `GEORADIUS` command. The `GEORADIUS` command takes a key name, longitude, latitude, radius, and unit as arguments. Here is an example:

```redis
GEORADIUS cities -122.4194 37.7749 1000 km
```

In this example, we are querying the cities within a radius of 1000 kilometers from the point (-122.4194, 37.7749). The key name is "cities".

The `GEORADIUS` command returns the members that are within the specified radius in a sorted order based on their distance from the specified point. You can also specify additional options such as the number of results to return and whether to include the coordinates of the members in the result.

## Conclusion

Redis Geo is a powerful module that provides geospatial indexing and querying capabilities in Redis. With Redis Geo, you can store and query geospatial data with ease. Redis Geo is easy to use and provides high performance and scalability. If you are working with geospatial data in Redis, Redis Geo is definitely worth checking out.

## External resources

- [Redis Geo official documentation](https://redis.io/commands#geo)
- [Redis Geo tutorial](https://www.tutorialspoint.com/redis/redis_geo.htm)
- [Redis Geo examples](https://github.com/RedisLabs/redis-geo)