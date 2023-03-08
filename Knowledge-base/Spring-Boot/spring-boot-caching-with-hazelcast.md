---
title: Hazelcast를 사용한 스프링 부트 캐싱
description: 
published: true
date: 2023-01-31T22:18:01.203Z
tags: 
editor: markdown
dateCreated: 2023-01-31T22:17:59.602Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Spring Boot Caching with Hazelcast***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-caching-with-hazelcast)
{.links-list}


# Hazelcast를 사용한 스프링 부트 캐싱

캐싱은 모든 고성능 애플리케이션의 중요한 구성 요소입니다. 응답 시간을 대폭 개선하고 애플리케이션 서버의 로드를 줄일 수 있습니다.

사용 가능한 많은 캐싱 솔루션이 있지만 가장 인기 있는 솔루션 중 하나는 Hazelcast입니다. Hazelcast는 Spring Boot 애플리케이션과 쉽게 통합할 수 있는 오픈 소스 분산 캐싱 솔루션입니다.

이 기사에서는 Spring Boot 애플리케이션에서 캐싱을 위해 Hazelcast를 사용하는 방법을 살펴보겠습니다. 간단한 예제로 시작한 다음 Hazelcast가 제공해야 하는 고급 기능 중 일부를 살펴보겠습니다.

## 헤이즐캐스트 설정

가장 먼저 해야 할 일은 Hazelcast 인스턴스를 설정하는 것입니다. Hazelcast Spring Boot Starter를 사용하여 이 작업을 수행할 수 있습니다.

프로젝트에 스타터를 추가하려면 빌드 파일에 다음 종속성을 추가하기만 하면 됩니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-hazelcast</artifactId>
</dependency>
```

스타터가 프로젝트에 추가되면 응용 프로그램이 실행될 때 Hazelcast가 자동으로 구성되고 시작됩니다.

## Hazelcast로 캐싱

이제 Hazelcast를 시작하고 실행했으므로 이를 캐싱에 사용하는 방법을 살펴보겠습니다.

간단한 예부터 시작하겠습니다. 사용자 목록을 반환하는 서비스가 있다고 가정합니다.

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    );

    public List<User> getUsers() {
        return users;
    }
}
```

이 서비스는 REST 컨트롤러에 의해 호출됩니다.

```java
@RestController
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/users")
    public List<User> getUsers() {
        return userService.getUsers();
    }
}
```

`getUsers` 메서드의 결과를 캐싱하여 이 컨트롤러의 성능을 향상시킬 수 있습니다.

```java
@RestController
public class UserController {

    private final UserService userService;

    private final HazelcastInstance hazelcastInstance;

    public UserController(UserService userService, HazelcastInstance hazelcastInstance) {
        this.userService = userService;
        this.hazelcastInstance = hazelcastInstance;
    }

    @GetMapping("/users")
    public List<User> getUsers() {
        List<User> users = hazelcastInstance.getList("users");
        if (users == null) {
            users = userService.getUsers();
            hazelcastInstance.setList("users", users);
        }
        return users;
    }
}
```

이 예에서는 `목록`을 캐시로 사용하고 있습니다. Hazelcast는 `Map`, `Set` 및 `Queue` 구조도 지원합니다.

개별 메서드의 결과를 캐시할 수도 있습니다.

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    );

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }
}
```

이 경우 캐시를 명시적으로 구성할 필요가 없습니다. Spring Boot는 자동으로 캐시 관리자를 구성하고 `getUsers` 메서드의 결과를 캐시합니다.

## 캐시에서 항목 제거

항목이 캐시되면 명시적으로 제거될 때까지 캐시에 남아 있다는 점을 기억하는 것이 중요합니다. 이로 인해 기본 데이터가 변경되면 오래된 데이터가 반환될 수 있습니다.

`@CacheEvict` 주석을 사용하여 캐시에서 항목을 제거할 수 있습니다.

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    );

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }

    @CacheEvict("users")
    public void evictUsers() {
    }
}
```

이 예에서는 `@CacheEvict`로 `evictUsers` 메서드에 주석을 추가했습니다. 이렇게 하면 메서드가 호출될 때 `users` 캐시가 지워집니다.

`@CacheEvict(allEntries = true)` 주석을 사용하여 모든 캐시에서 모든 항목을 제거할 수도 있습니다.

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    );

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }

    @CacheEvict(allEntries = true)
    public void evictAll() {
    }
}
```

## 캐시된 항목 업데이트

`@CachePut` 주석을 사용하여 캐시된 항목을 업데이트할 수도 있습니다.

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    );

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }

    @CachePut("users")
    public List<User> updateUsers() {
        return users;
    }
}
```

이 예에서 `updateUsers` 메서드는 `@CachePut`으로 주석이 추가됩니다. 이렇게 하면 메서드가 호출될 때 `users` 캐시가 업데이트됩니다.

## 결론

이 기사에서는 Spring Boot 애플리케이션에서 캐싱을 위해 Hazelcast를 사용하는 방법을 살펴보았습니다. Hazelcast를 설정하는 방법과 이를 데이터 캐싱에 사용하는 방법을 살펴보았습니다. 또한 캐시에서 항목을 제거하는 방법과 캐시된 항목을 업데이트하는 방법도 살펴보았습니다.

캐싱은 모든 고성능 애플리케이션의 중요한 구성 요소입니다. Hazelcast를 사용하면 Spring Boot 애플리케이션에 캐싱을 쉽게 추가할 수 있습니다.