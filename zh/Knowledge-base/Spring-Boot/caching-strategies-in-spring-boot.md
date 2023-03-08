---
title: Spring Boot 中的缓存策略
description: 
published: true
date: 2023-01-31T08:07:37.641Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:07:36.075Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Caching Strategies in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/caching-strategies-in-spring-boot)
{.links-list}


# Spring Boot 中的缓存策略

Spring Boot 提供了许多开箱即用的功能来缓存静态和动态数据。本文将探讨 Spring Boot 中使用的最流行的缓存策略，包括每种策略的优缺点。

# # 缓存静态数据

最简单的缓存形式是缓存不经常更改的静态数据。这可以使用 @Cacheable 注释来完成。例如，如果我们有一个返回用户列表的慢速服务，我们可以使用以下代码缓存结果：

```java
@Cacheable(value = "users")
public List<User> getAllUsers() {
  // Slow service call
}
```

这会将服务调用的结果存储在缓存中，键为“users”。下次调用服务时，将返回缓存的结果，而不是进行慢速服务调用。

# # 缓存动态数据

缓存动态数据有点复杂，但对于减少数据库或其他资源的负载非常有用。可以采用几种不同的方法。

# ## 缓存端

缓存端模式是缓存从数据库或其他慢速资源读取的数据的常用方法。基本思想是首先检查请求数据的缓存。如果数据不在缓存中，则从慢速资源中获取数据，然后将其存储在缓存中。可以使用以下代码实现此模式：

```java
@Cacheable(value = "users", key = "#id")
public User getUserById(String id) {
  // Check cache
  User user = cache.get(id);
  
  // If not in cache, fetch from database
  if (user == null) {
    user = database.get(id);
    
    // Store in cache
    cache.put(id, user);
  }
  
  return user;
}
```

这将首先检查具有给定 ID 的用户的缓存。如果用户不在缓存中，将从数据库中获取并存储在缓存中。下次请求同一用户时，将返回缓存的副本。

# ##通读

缓存数据的另一种常见模式是通读缓存。这种模式类似于缓存端模式，但数据总是从慢速资源中获取。然后将结果存储在缓存中并返回给调用者。可以使用以下代码实现此模式：

```java
@Cacheable(value = "users", key = "#id")
public User getUserById(String id) {
  // Fetch from database
  User user = database.get(id);
  
  // Store in cache
  cache.put(id, user);
  
  return user;
}
```

这将从数据库中获取用户并将结果存储在缓存中。下次请求同一用户时，将返回缓存的副本。

# # 选择正确的缓存策略

没有一种适用于所有情况的完美缓存策略。正确的策略取决于缓存的数据、系统的预期负载和其他因素。

# ## 静态数据

对于不经常变化的静态数据，最简单的解决方案是使用@Cacheable 注解。这会将数据存储在缓存中并在后续请求中返回。

# ## 动态数据

对于动态数据，缓存策略的选择取决于很多因素。如果数据读取频繁且系统负载高，则缓存端或读取缓存可能是最佳选择。如果数据读取频率较低或系统负载较低，则缓存端模式可能就足够了。