---
title: 带 Redis 的 Spring Boot
description: 
published: true
date: 2023-02-07T11:32:59.252Z
tags: 
editor: markdown
dateCreated: 2023-02-07T11:32:53.562Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot with Redis***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-with-redis)
{.links-list}


# 使用 Redis 的 Spring Boot

Redis 是一种开源的内存数据结构存储，用作数据库、缓存和消息代理。它支持数据结构，例如字符串、散列、列表、集合、带范围查询的排序集合、位图、hyperloglogs 和带半径查询的地理空间索引。

在本文中，我们将向您展示如何将 Spring Boot 与 Redis 结合使用。

## 什么是 Redis？

Redis 是一种开源（BSD 许可）内存数据结构存储，用作数据库、缓存和消息代理。它支持数据结构，例如字符串、散列、列表、集合、带范围查询的排序集合、位图、hyperloglogs 和带半径查询的地理空间索引。

Redis 具有内置复制、Lua 脚本、LRU 逐出、事务和不同级别的磁盘持久性，并通过 Redis Sentinel 和 Redis Cluster 自动分区提供高可用性。

## 使用 Redis 的 Spring Boot

Spring Boot 为 Redis 提供一流的支持。在本节中，我们将向您展示如何将 Spring Boot 与 Redis 结合使用。

我们将使用 [lettuce](https://github.com/lettuce-io/lettuce-core) 库与 Redis 通信。 Lettuce 是一个完全非阻塞的 Redis 客户端，基于用于处理 Redis 连接的 Netty 和用于对象映射的 Spring Data。

### Maven 依赖项

首先，我们需要将以下依赖项添加到我们的 pom.xml 中：

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

### Redis配置

默认情况下，Spring Boot 会在 localhost:6379 寻找 Redis 服务器。我们可以通过在 application.properties 文件中设置 `spring.redis.host` 和 `spring.redis.port` 属性来改变它：

```properties
spring.redis.host=localhost
spring.redis.port=6379
```

如果受密码保护，我们还可以为 Redis 指定密码：

```properties
spring.redis.password=secret
```

### 春季数据Redis

Spring Data Redis 是 Spring Data 的 Redis 具体实现。它提供了[Jedis](https://github.com/xetorthio/jedis)和[Lettuce](https://github.com/lettuce-io/lettuce-core)Redis客户端的抽象，并提供了一个统一的对象-Redis 的映射器接口。

#### Redis模板

RedisTemplate 是 Spring Data Redis 中的中心类。它针对 Spring 应用程序中使用的数据类型定义了高级 Redis 操作。

我们可以在我们的 Spring 应用上下文中配置一个 RedisTemplate：

```java
@Bean
public RedisTemplate<String, Object> redisTemplate(
        RedisConnectionFactory factory) {
    RedisTemplate<String, Object> template = new RedisTemplate<>();
    template.setConnectionFactory(factory);
    return template;
}
```

#### 字符串Redis模板

StringRedisTemplate 是专门用于处理 Redis 中基于字符串的数据的 RedisTemplate。

我们可以在我们的 Spring 应用程序上下文中配置一个 StringRedisTemplate：

```java
@Bean
public StringRedisTemplate stringRedisTemplate(
        RedisConnectionFactory factory) {
    StringRedisTemplate template = new StringRedisTemplate();
    template.setConnectionFactory(factory);
    return template;
}
```

### Redis 存储库

Spring Data Redis 提供了一个 Redis 特定的存储库抽象。我们可以使用这个抽象来创建 Redis 存储库。

首先，我们需要创建一个扩展 Repository 接口的 Redis 特定接口：

```java
public interface PersonRepository extends Repository<Person, String> {

    Person findById(String id);

    List<Person> findAll();

    Person save(Person person);

    void delete(Person person);
}
```

接下来，我们需要创建 PersonRepository 接口的实现：

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

在上面的示例中，我们使用 RedisTemplate 与 Redis 进行交互。

### Spring Data Redis 和 Jackson

Spring Data Redis 使用 Jackson 将对象序列化和反序列化为 JSON。默认情况下，Jackson 配置为使用 JAXB 注释内省器。

我们可以通过在 application.properties 文件中将 `spring.jackson.deserialization.USE_JACKSON_ANNOTATIONS` 属性设置为 `true` 来配置 Jackson 使用 Jackson 注释内省器而不是 JAXB 注释内省器：

```properties
spring.jackson.deserialization.USE_JACKSON_ANNOTATIONS=true
```

我们还可以通过使用自定义 ObjectMapper 将 Jackson 配置为使用 Jackson 注释内省器：

```java
@Bean
public ObjectMapper objectMapper() {
    ObjectMapper mapper = new ObjectMapper();
    mapper.configure(DeserializationFeature.USE_JACKSON_ANNOTATIONS, true);
    return mapper;
}
```

## 结论

在本文中，我们向您展示了如何将 Spring Boot 与 Redis 结合使用。