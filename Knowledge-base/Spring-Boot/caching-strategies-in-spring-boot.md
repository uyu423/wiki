---
title: Spring Boot의 캐싱 전략
description: 
published: true
date: 2023-01-31T08:11:49.982Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:07:36.073Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Caching Strategies in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/caching-strategies-in-spring-boot)
{.links-list}


# Spring Boot의 캐싱 전략

Spring Boot는 정적 및 동적 데이터 캐싱을 위해 즉시 사용 가능한 여러 기능을 제공합니다. 이 기사에서는 각각의 장단점을 포함하여 Spring Boot에서 사용되는 가장 인기 있는 캐싱 전략을 살펴봅니다.

## 정적 데이터 캐싱

캐싱의 가장 간단한 형태는 자주 변경되지 않는 정적 데이터를 캐싱하는 것입니다. 이것은 @Cacheable 주석을 사용하여 수행할 수 있습니다. 예를 들어 사용자 목록을 반환하는 느린 서비스가 있는 경우 다음 코드를 사용하여 결과를 캐시할 수 있습니다.

```java
@Cacheable(value = "users")
public List<User> getAllUsers() {
  // Slow service call
}
```

그러면 서비스 호출 결과가 "users" 키와 함께 캐시에 저장됩니다. 다음에 서비스를 호출하면 느린 서비스 호출을 하는 대신 캐시된 결과가 반환됩니다.

## 동적 데이터 캐싱

동적 데이터 캐싱은 좀 더 복잡하지만 데이터베이스 또는 기타 리소스에 대한 로드를 줄이는 데 매우 유용할 수 있습니다. 취할 수 있는 몇 가지 접근 방식이 있습니다.

### 캐시 제외

캐시 배제 패턴은 데이터베이스 또는 기타 느린 리소스에서 읽은 데이터를 캐싱하기 위한 일반적인 접근 방식입니다. 기본 아이디어는 먼저 요청된 데이터의 캐시를 확인하는 것입니다. 데이터가 캐시에 없으면 느린 리소스에서 가져온 다음 캐시에 저장됩니다. 이 패턴은 다음 코드를 사용하여 구현할 수 있습니다.

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

먼저 주어진 ID를 가진 사용자의 캐시를 확인합니다. 사용자가 캐시에 없으면 데이터베이스에서 가져와 캐시에 저장됩니다. 다음에 동일한 사용자가 요청되면 캐시된 복사본이 반환됩니다.

### 읽어보기

데이터 캐싱의 또 다른 일반적인 패턴은 읽기 캐시입니다. 이 패턴은 캐시 배제 패턴과 유사하지만 데이터는 항상 느린 리소스에서 가져옵니다. 결과는 캐시에 저장되고 호출자에게 반환됩니다. 이 패턴은 다음 코드를 사용하여 구현할 수 있습니다.

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

이렇게 하면 데이터베이스에서 사용자를 가져오고 결과를 캐시에 저장합니다. 다음에 동일한 사용자가 요청되면 캐시된 복사본이 반환됩니다.

## 올바른 캐싱 전략 선택

모든 상황에 대해 완벽한 캐싱 전략은 없습니다. 올바른 전략은 캐시되는 데이터, 시스템의 예상 로드 및 기타 요인에 따라 다릅니다.

### 정적 데이터

자주 변경되지 않는 정적 데이터의 경우 가장 간단한 솔루션은 @Cacheable 주석을 사용하는 것입니다. 이렇게 하면 데이터가 캐시에 저장되고 후속 요청에서 반환됩니다.

### 동적 데이터

동적 데이터의 경우 캐싱 전략의 선택은 여러 요인에 따라 달라집니다. 데이터를 자주 읽고 시스템의 부하가 높은 경우 캐시 배제 또는 읽기 캐시가 최선의 선택일 수 있습니다. 데이터 읽기 빈도가 낮거나 시스템 부하가 낮은 경우 캐시 배제 패턴으로 충분할 수 있습니다.