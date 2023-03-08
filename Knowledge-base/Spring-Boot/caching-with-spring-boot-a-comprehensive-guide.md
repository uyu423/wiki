---
title: Spring Boot를 사용한 캐싱: 종합 안내서
description: 
published: true
date: 2023-02-07T03:32:42.023Z
tags: 
editor: markdown
dateCreated: 2023-02-07T03:32:40.423Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Caching with Spring Boot: A Comprehensive Guide***English** document is available*](/en/Knowledge-base/Spring-Boot/caching-with-spring-boot-a-comprehensive-guide)
{.links-list}



# Spring Boot를 사용한 캐싱: 종합 가이드

캐싱은 웹 애플리케이션의 일반적인 성능 최적화 기술입니다. 자주 액세스하는 데이터를 메모리에 저장하여 다음에 필요할 때 빠르게 검색할 수 있도록 하여 응답 속도를 높일 수 있습니다.

Spring Boot는 메소드의 매개변수를 기반으로 캐시 키를 생성하는 데 사용할 수 있는 SimpleKeyGenerator를 포함하여 여러 내장 캐싱 솔루션을 제공합니다. 또한 Ehcache, Hazelcast 및 Redis와 같이 Spring Boot와 함께 사용할 수 있는 여러 타사 캐시 라이브러리가 있습니다.

이 기사에서는 Spring Boot로 캐싱을 구성하는 방법을 살펴보고 데이터 캐싱에 대한 보다 일반적인 사용 사례를 탐색합니다.

## Spring Boot로 캐싱 구성

Spring Boot는 캐싱을 구성하는 여러 가지 방법을 제공합니다. 가장 간단한 방법은 Spring Boot 애플리케이션에 @EnableCaching 주석을 추가하는 것입니다.

```java
@SpringBootApplication
@EnableCaching
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

이렇게 하면 응용 프로그램에서 @Cacheable로 주석이 달린 모든 메서드에 대해 캐싱이 활성화됩니다.

Spring Boot에서 사용할 캐시 관리자를 지정할 수도 있습니다. 예를 들어 Ehcache 캐시 관리자를 사용하려면 다음 속성을 application.properties 파일에 추가할 수 있습니다.

```properties
spring.cache.type=ehcache
```

## 캐싱 데이터

이제 Spring Boot 애플리케이션에서 캐싱을 활성화했으므로 데이터를 캐싱하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

### 캐싱 방법 결과

캐싱의 일반적인 사용 사례 중 하나는 메서드 호출 결과를 캐시하는 것입니다. 이는 메소드에 @Cacheable 주석을 달고 사용할 캐시 이름을 지정하여 수행할 수 있습니다.

```java
@Cacheable("books")
public List<Book> getBooks() {
    // ...
}
```

이 예제에서 getBooks() 메서드의 결과는 "books"라는 캐시에 캐시됩니다.

메서드 결과를 캐싱하는 데 사용할 키를 지정할 수도 있습니다. 예를 들어 책의 ID를 키로 사용하여 getBooks() 메서드의 결과를 캐시하려면 다음 주석을 사용할 수 있습니다.

```java
@Cacheable(value="books", key="#id")
public List<Book> getBooks(Long id) {
    // ...
}
```

### 캐싱 방법 매개변수

캐싱의 또 다른 일반적인 사용 사례는 메서드 매개 변수를 캐시하는 것입니다. 이는 메소드에 @CachePut 주석을 달고 사용할 캐시 이름을 지정하여 수행할 수 있습니다.

```java
@CachePut("books")
public void updateBook(Book book) {
    // ...
}
```

이 예제에서 updateBook() 메서드는 "books" 캐시에 책 개체를 캐시합니다.

메소드 매개변수 캐싱에 사용할 키를 지정할 수도 있습니다. 예를 들어 책의 ID를 키로 사용하여 책 개체를 캐시하려면 다음 주석을 사용할 수 있습니다.

```java
@CachePut(value="books", key="#book.id")
public void updateBook(Book book) {
    // ...
}
```

### 캐싱 메서드 호출

캐싱의 또 다른 일반적인 사용 사례는 메서드 호출의 결과를 캐시하는 것입니다. 이는 메소드에 @Cacheable 주석을 달고 사용할 캐시 이름을 지정하여 수행할 수 있습니다.

```java
@Cacheable("books")
public List<Book> getBooks() {
    // ...
}
```

이 예제에서 getBooks() 메서드의 결과는 "books"라는 캐시에 캐시됩니다.

메서드 결과를 캐싱하는 데 사용할 키를 지정할 수도 있습니다. 예를 들어 책의 ID를 키로 사용하여 getBooks() 메서드의 결과를 캐시하려면 다음 주석을 사용할 수 있습니다.

```java
@Cacheable(value="books", key="#id")
public List<Book> getBooks(Long id) {
    // ...
}
```

## 결론

이 기사에서는 Spring Boot로 캐싱을 구성하는 방법을 살펴보고 데이터 캐싱에 대한 보다 일반적인 사용 사례를 살펴보았습니다. 캐싱은 웹 애플리케이션에 유용한 성능 최적화 기술이 될 수 있습니다. 자주 액세스하는 데이터를 메모리에 저장하여 다음에 필요할 때 빠르게 검색할 수 있도록 하여 응답 속도를 높일 수 있습니다.