---
title: Spring Boot with Redis
description: 
published: true
date: 2023-02-07T11:32:55.267Z
tags: 
editor: markdown
dateCreated: 2023-02-07T11:32:53.569Z
---

- [Bota Primavera con Redis***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-with-redis)
{.links-list}
- [带 Redis 的 Spring Boot***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-with-redis)
{.links-list}
- [Redis를 사용한 스프링 부트***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-with-redis)
{.links-list}


# Spring Boot with Redis

Redis is an open source, in-memory data structure store, used as a database, cache and message broker. It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs and geospatial indexes with radius queries. 

In this article, we will show you how to use Spring Boot with Redis.

## What is Redis?

Redis is an open source (BSD licensed), in-memory data structure store, used as a database, cache and message broker. It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs, and geospatial indexes with radius queries.

Redis has built-in replication, Lua scripting, LRU eviction, transactions and different levels of on-disk persistence, and provides high availability via Redis Sentinel and automatic partitioning with Redis Cluster.

## Spring Boot with Redis

Spring Boot provides first-class support for Redis. In this section, we will show you how to use Spring Boot with Redis.

We will use the [lettuce](https://github.com/lettuce-io/lettuce-core) library for communicating with Redis. Lettuce is a fully non-blocking Redis client based on Netty for handling Redis connections and Spring Data for object mapping.

### Maven Dependencies

First, we need to add the following dependencies to our `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-redis</artifactId>
</dependency>
```

### Redis Configuration

By default, Spring Boot will look for a Redis server at `localhost:6379`. We can change this by setting the `spring.redis.host` and `spring.redis.port` properties in our application.properties file:

```properties
spring.redis.host=localhost
spring.redis.port=6379
```

We can also specify a password for Redis if it is password protected:

```properties
spring.redis.password=secret
```

### Spring Data Redis

Spring Data Redis is the Redis specific implementation of Spring Data. It provides the abstractions of the [Jedis](https://github.com/xetorthio/jedis) and [Lettuce](https://github.com/lettuce-io/lettuce-core) Redis clients and provides a unified object-mapper interface for Redis.

#### RedisTemplate

RedisTemplate is the central class in Spring Data Redis. It defines high-level Redis operations against data types used in Spring applications.

We can configure a RedisTemplate in our Spring application context:

```java
@Bean
public RedisTemplate<String, Object> redisTemplate(
        RedisConnectionFactory factory) {
    RedisTemplate<String, Object> template = new RedisTemplate<>();
    template.setConnectionFactory(factory);
    return template;
}
```

#### StringRedisTemplate

StringRedisTemplate is a specialized RedisTemplate that is meant for handling String-based data in Redis.

We can configure a StringRedisTemplate in our Spring application context:

```java
@Bean
public StringRedisTemplate stringRedisTemplate(
        RedisConnectionFactory factory) {
    StringRedisTemplate template = new StringRedisTemplate();
    template.setConnectionFactory(factory);
    return template;
}
```

### Redis Repositories

Spring Data Redis provides a Redis specific repository abstraction. We can use this abstraction to create Redis repositories.

First, we need to create a Redis specific interface that extends the Repository interface:

```java
public interface PersonRepository extends Repository<Person, String> {

    Person findById(String id);

    List<Person> findAll();

    Person save(Person person);

    void delete(Person person);
}
```

Next, we need to create an implementation of our PersonRepository interface:

```java
@Service
public class PersonRepositoryImpl implements PersonRepository {

    private final RedisTemplate<String, Person> redisTemplate;

    @Autowired
    public PersonRepositoryImpl(RedisTemplate<String, Person> redisTemplate) {
        this.redisTemplate = redisTemplate;
    }

    @Override
    public Person findById(String id) {
        return redisTemplate.opsForValue().get(id);
    }

    @Override
    public List<Person> findAll() {
        return redisTemplate.opsForValue().multiGet(redisTemplate.keys("*"));
    }

    @Override
    public Person save(Person person) {
        redisTemplate.opsForValue().set(person.getId(), person);
        return person;
    }

    @Override
    public void delete(Person person) {
        redisTemplate.delete(person.getId());
    }
}
```

In the above example, we are using the RedisTemplate to interact with Redis.

### Spring Data Redis and Jackson

Spring Data Redis uses Jackson for serializing and deserializing objects to and from JSON. By default, Jackson is configured to use the JAXB annotation introspector.

We can configure Jackson to use the Jackson annotation introspector instead of the JAXB annotation introspector by setting the `spring.jackson.deserialization.USE_JACKSON_ANNOTATIONS` property to `true` in our application.properties file:

```properties
spring.jackson.deserialization.USE_JACKSON_ANNOTATIONS=true
```

We can also configure Jackson to use the Jackson annotation introspector by using a custom ObjectMapper:

```java
@Bean
public ObjectMapper objectMapper() {
    ObjectMapper mapper = new ObjectMapper();
    mapper.configure(DeserializationFeature.USE_JACKSON_ANNOTATIONS, true);
    return mapper;
}
```

## Conclusion

In this article, we have shown you how to use Spring Boot with Redis.