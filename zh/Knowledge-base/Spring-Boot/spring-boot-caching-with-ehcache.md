---
title: 使用 EhCache 进行 Spring Boot 缓存
description: 
published: true
date: 2023-02-07T16:32:42.008Z
tags: 
editor: markdown
dateCreated: 2023-02-07T16:32:36.250Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot Caching with EhCache***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-caching-with-ehcache)
{.links-list}


# 使用 EhCache 进行 Spring Boot 缓存

缓存是提高应用程序性能和可伸缩性的常用技术。它可用于将频繁访问的数据缓存在内存中，以便无需查询数据库即可快速检索。

使用 Spring Boot 时，我们可以使用 @EnableCaching 注解在我们的应用程序中启用 EhCache。在本文中，我们将了解如何在 Spring Boot 中配置和使用 EhCache。

## 配置 EhCache

要配置 EhCache，我们需要在 src/main/resources 目录下创建一个 ehcache.xml 文件。该文件的内容应如下所示：

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

在 ehcache.xml 文件中，我们配置了一个名为“defaultCache”的缓存。我们的应用程序将使用此缓存来缓存数据。缓存配置为使用本地磁盘存储溢出，并使 120 秒内未访问的条目过期。

## 使用 Spring Boot 进行缓存

现在我们已经配置了 EhCache，我们可以在我们的 Spring Boot 应用程序中使用它。首先，我们需要在 Application 类中添加 @EnableCaching 注解：

```java
@SpringBootApplication
@EnableCaching
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

接下来，我们需要使用@Cacheable 注释来注释我们要缓存的服务类中的方法：

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

在上面的代码中，我们用 @Cacheable 注释了 getUsers() 方法。这告诉 Spring 将此方法的结果缓存在“用户”缓存中。

现在，当我们调用 getUsers() 方法时，它会第一次查询数据库并返回结果。第二次调用它时，它会从缓存中返回结果。

## 更新缓存数据

需要注意的是，当数据库中的数据更新时，缓存的数据不会自动更新。要更新缓存，我们需要使用@CacheEvict 注解：

```java
@Service
public class UserService {

    @CacheEvict(value = "users", allEntries = true)
    public void updateUser(User user) {
        // update user in database
    }
}
```

在上面的代码中，我们用 @CacheEvict 注释了 updateUser() 方法。这告诉 Spring 在调用此方法时从“用户”缓存中删除所有条目。

现在，当我们调用 updateUser() 方法时，缓存将被清除，下次调用 getUsers() 方法时，它将查询数据库并返回更新的结果。

## 结论

在本文中，我们了解了如何在 Spring Boot 中配置和使用 EhCache。缓存是提高应用程序性能的好方法。通过在内存中缓存经常访问的数据，可以避免每次都查询数据库。