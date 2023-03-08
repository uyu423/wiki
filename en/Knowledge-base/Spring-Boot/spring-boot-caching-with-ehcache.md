---
title: Spring Boot Caching with EhCache
description: 
published: true
date: 2023-02-07T16:32:37.860Z
tags: 
editor: markdown
dateCreated: 2023-02-07T16:32:36.254Z
---

- [Caché Spring Boot con EhCache***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-caching-with-ehcache)
{.links-list}
- [使用 EhCache 进行 Spring Boot 缓存***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-caching-with-ehcache)
{.links-list}
- [EhCache를 사용한 스프링 부트 캐싱***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-caching-with-ehcache)
{.links-list}


# Spring Boot Caching with EhCache

Caching is a common technique for improving the performance and scalability of applications. It can be used to cache frequently accessed data in memory so that it can be quickly retrieved without having to query the database.

When using Spring Boot, we can use the @EnableCaching annotation to enable EhCache in our application. In this article, we'll take a look at how to configure and use EhCache with Spring Boot.

## Configuring EhCache

To configure EhCache, we need to create a ehcache.xml file in the src/main/resources directory. The contents of the file should look like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="ehcache.xsd"
         updateCheck="true"
         monitoring="autodetect"
         dynamicConfig="true">
    <diskStore path="java.io.tmpdir"/>
    <cache name="defaultCache"
           maxElementsInMemory="10000"
           overflowToDisk="true"
           eternal="false"
           timeToIdleSeconds="120"
           timeToLiveSeconds="120"
           diskPersistent="false"
           diskExpiryThreadIntervalSeconds="120"
           memoryStoreEvictionPolicy="LRU">
        <persistence strategy="localTempSwap"/>
    </cache>
</ehcache>
```

In the ehcache.xml file, we've configured a cache named "defaultCache". This cache will be used by our application to cache data. The cache is configured to use a local disk store for overflow and to expire entries that have not been accessed in 120 seconds.

## Caching with Spring Boot

Now that we have EhCache configured, we can use it in our Spring Boot application. First, we need to add the @EnableCaching annotation to our Application class:

```java
@SpringBootApplication
@EnableCaching
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

Next, we need to annotate the methods in our service classes that we want to cache with the @Cacheable annotation:

```java
@Service
public class UserService {

    @Cacheable(value = "users")
    public List<User> getUsers() {
        // query database for users
        return users;
    }
}
```

In the code above, we've annotated the getUsers() method with @Cacheable. This tells Spring to cache the results of this method in the "users" cache.

Now, when we call the getUsers() method, the first time it will query the database and return the results. The second time we call it, it will return the results from the cache.

## Updating Cached Data

It's important to note that when data in the database is updated, the cached data will not be updated automatically. To update the cache, we need to use the @CacheEvict annotation:

```java
@Service
public class UserService {

    @CacheEvict(value = "users", allEntries = true)
    public void updateUser(User user) {
        // update user in database
    }
}
```

In the code above, we've annotated the updateUser() method with @CacheEvict. This tells Spring to remove all entries from the "users" cache when this method is called.

Now, when we call the updateUser() method, the cache will be cleared and the next time we call the getUsers() method, it will query the database and return the updated results.

## Conclusion

In this article, we've looked at how to configure and use EhCache with Spring Boot. Caching can be a great way to improve the performance of your application. By caching frequently accessed data in memory, you can avoid having to query the database each time.