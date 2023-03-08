---
title: 010: Spring Boot 및 Redis로 캐싱 구현
description: 
published: true
date: 2023-02-03T08:43:41.420Z
tags: 
editor: markdown
dateCreated: 2023-02-03T08:43:36.492Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [010: Implementing caching with Spring Boot and Redis***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/010-implementing-caching-with-spring-boot-and-redis)
{.links-list}


# Spring Boot와 Redis로 캐싱 구현하기

이 게시물에서는 Spring Boot 및 Redis로 캐싱을 구현하는 방법을 다룰 것입니다. 캐싱에 대한 간략한 개요와 캐싱이 유용한 이유부터 시작하겠습니다. 그런 다음 캐싱에 Redis를 사용하도록 Spring Boot를 구성하는 방법을 살펴보겠습니다. 마지막으로 캐싱을 위해 Redis를 사용하는 방법을 보여주는 간단한 Spring Boot 애플리케이션을 작성합니다.

## 캐싱이란?

캐싱은 해당 데이터에 대한 후속 액세스 속도를 높이기 위해 임시 메모리 위치에 데이터를 저장하는 기술입니다. 데이터가 캐시되면 데이터가 이미 메모리에 있으므로 해당 데이터에 대한 향후 요청을 훨씬 빠르게 처리할 수 있습니다.

캐싱에는 애플리케이션 캐싱과 데이터베이스 캐싱의 두 가지 주요 유형이 있습니다. 애플리케이션 캐싱은 애플리케이션 메모리에 데이터를 캐시하는 데 사용되는 반면 데이터베이스 캐싱은 데이터베이스 메모리에 데이터를 캐시하는 데 사용됩니다.

## 캐싱을 사용하는 이유는 무엇입니까?

캐싱은 데이터베이스와 같은 느린 저장 매체에서 데이터를 읽는 횟수를 줄여 애플리케이션의 성능을 향상시키는 데 사용할 수 있습니다. 캐싱은 메모리와 같은 더 빠른 저장 매체에 데이터 복사본을 저장하여 느린 저장 매체에서 읽어야 하는 데이터의 양을 줄이는 데에도 사용할 수 있습니다.

## 캐싱에 Redis를 사용하도록 Spring Boot 구성

Spring Boot는 Redis에 대한 내장 지원을 제공하므로 캐싱을 위해 Redis를 쉽게 구성할 수 있습니다. 캐싱에 Redis를 사용하도록 Spring Boot를 구성하려면 프로젝트에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

또한 application.properties 파일에서 Redis 서버 호스트 및 포트를 구성해야 합니다.

```properties
spring.redis.host=localhost
spring.redis.port=6379
```

## 캐싱을 위해 Redis를 사용하도록 Spring Boot 애플리케이션 작성

캐싱에 Redis를 사용하도록 Spring Boot를 구성했으므로 Redis를 캐싱에 사용하는 방법을 보여주는 간단한 Spring Boot 애플리케이션을 작성해 보겠습니다.

사용자를 나타내는 간단한 데이터 모델을 만드는 것으로 시작하겠습니다.

```java
public class User {

    private Long id;
    private String name;
    private Integer age;

    // getters and setters
}
```

다음으로 사용자를 관리하기 위해 단일 REST 컨트롤러가 있는 간단한 Spring Boot 애플리케이션을 생성합니다.

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        // code to get user from database
    }

    @PostMapping
    public User createUser(@RequestBody User user) {
        // code to create user in database
    }

    @PutMapping("/{id}")
    public User updateUser(@PathVariable Long id, @RequestBody User user) {
        // code to update user in database
    }

    @DeleteMapping("/{id}")
    public void deleteUser(@PathVariable Long id) {
        // code to delete user from database
    }
}
```

이제 이 컨트롤러를 사용하여 데이터베이스의 사용자를 관리할 수 있습니다. 그러나 getUser() 메서드를 호출할 때마다 데이터베이스에서 사용자를 가져오기 위해 데이터베이스 쿼리가 실행됩니다. 특히 데이터베이스가 큰 경우 속도가 느릴 수 있습니다.

Redis를 사용하여 getUser() 메서드의 결과를 캐싱하여 애플리케이션의 성능을 향상시킬 수 있습니다. 이를 위해 getUser() 메서드에 @Cacheable 주석을 추가합니다.

```java
@Cacheable("users")
@GetMapping("/{id}")
public User getUser(@PathVariable Long id) {
    // code to get user from database
}
```

이 주석은 "users"라는 Redis 캐시에서 getUser() 메소드의 결과를 캐시하도록 Spring에 지시합니다. 다음에 동일한 ID로 getUser() 메서드를 호출하면 데이터베이스 쿼리를 실행하는 대신 캐시된 결과가 반환됩니다.

@CacheEvict 주석을 사용하여 캐시된 항목을 제거할 수도 있습니다.

```java
@CacheEvict("users")
@DeleteMapping("/{id}")
public void deleteUser(@PathVariable Long id) {
    // code to delete user from database
}
```

이 주석은 deleteUser() 메서드가 호출될 때 주어진 ID를 가진 사용자에 대해 캐시된 항목을 제거하도록 Spring에 지시합니다.

## 결론

이 게시물에서는 Spring Boot 및 Redis로 캐싱을 구현하는 방법을 다루었습니다. 우리는 캐싱에 Redis를 사용하도록 Spring Boot를 구성하는 방법을 보았고 캐싱에 Redis를 사용하는 방법을 보여주기 위해 간단한 Spring Boot 애플리케이션을 작성했습니다.