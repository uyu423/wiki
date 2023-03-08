---
title: 使用 Spring Boot 进行缓存：综合指南
description: 
published: true
date: 2023-02-07T03:32:42.004Z
tags: 
editor: markdown
dateCreated: 2023-02-07T03:32:40.422Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Caching with Spring Boot: A Comprehensive Guide***English** document is available*](/en/Knowledge-base/Spring-Boot/caching-with-spring-boot-a-comprehensive-guide)
{.links-list}



# 使用 Spring Boot 进行缓存：综合指南

缓存是 Web 应用程序常用的性能优化技术。它可以通过将经常访问的数据存储在内存中来加快响应速度，以便在下次需要时可以快速检索。

Spring Boot 提供了几种内置的缓存解决方案，包括 SimpleKeyGenerator，它可用于根据方法的参数生成缓存键。还有一些可以与 Spring Boot 一起使用的第三方缓存库，例如 Ehcache、Hazelcast 和 Redis。

在本文中，我们将了解如何使用 Spring Boot 配置缓存，并探索一些更常见的缓存数据用例。

## 使用 Spring Boot 配置缓存

Spring Boot 提供了几种不同的方式来配置缓存。最简单的方法是在 Spring Boot 应用程序中添加 @EnableCaching 注解：

```java
@SpringBootApplication
@EnableCaching
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

这将为应用程序中所有使用@Cacheable 注释的方法启用缓存。

也可以指定 Spring Boot 使用的缓存管理器。例如，要使用 Ehcache 缓存管理器，可以将以下属性添加到 application.properties 文件中：

```properties
spring.cache.type=ehcache
```

## 缓存数据

现在我们已经在 Spring Boot 应用程序中启用了缓存，让我们看一些如何缓存数据的示例。

### 缓存方法结果

缓存的一个常见用例是缓存方法调用的结果。这可以通过使用 @Cacheable 注释方法并指定要使用的缓存的名称来完成：

```java
@Cacheable("books")
public List<Book> getBooks() {
    // ...
}
```

在此示例中，getBooks() 方法的结果将缓存在名为“books”的缓存中。

也可以指定用于缓存方法结果的键。例如，要缓存使用书的 id 作为键的 getBooks() 方法的结果，可以使用以下注解：

```java
@Cacheable(value="books", key="#id")
public List<Book> getBooks(Long id) {
    // ...
}
```

### 缓存方法参数

缓存的另一个常见用例是缓存方法参数。这可以通过使用 @CachePut 注释方法并指定要使用的缓存的名称来完成：

```java
@CachePut("books")
public void updateBook(Book book) {
    // ...
}
```

在此示例中，updateBook() 方法会将图书对象缓存在“books”缓存中。

也可以指定用于缓存方法参数的键。例如，要缓存以书的 id 为键的书对象，可以使用如下注解：

```java
@CachePut(value="books", key="#book.id")
public void updateBook(Book book) {
    // ...
}
```

### 缓存方法调用

缓存的另一个常见用例是缓存方法调用的结果。这可以通过使用 @Cacheable 注释方法并指定要使用的缓存的名称来完成：

```java
@Cacheable("books")
public List<Book> getBooks() {
    // ...
}
```

在此示例中，getBooks() 方法的结果将缓存在名为“books”的缓存中。

也可以指定用于缓存方法结果的键。例如，要缓存使用书的 id 作为键的 getBooks() 方法的结果，可以使用以下注解：

```java
@Cacheable(value="books", key="#id")
public List<Book> getBooks(Long id) {
    // ...
}
```

## 结论

在本文中，我们研究了如何使用 Spring Boot 配置缓存，并探索了一些更常见的缓存数据用例。缓存可以成为 Web 应用程序的一种有用的性能优化技术。它可以通过将经常访问的数据存储在内存中来加快响应速度，以便在下次需要时可以快速检索。