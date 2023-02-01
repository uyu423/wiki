---
title: Spring Boot의 CQRS(Command Query Responsibility Segregation) 패턴
description: 
published: true
date: 2023-02-01T10:47:42.511Z
tags: 
editor: markdown
dateCreated: 2023-02-01T10:47:42.511Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [The Command Query Responsibility Segregation (CQRS) Pattern in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-command-query-responsibility-segregation-cqrs-pattern-in-spring-boot)
{.links-list}


# Spring Boot의 CQRS(Command Query Responsibility Segregation) 패턴

명령 쿼리 책임 분리(CQRS)는 데이터 검색 책임(쿼리)과 데이터 수정 책임(명령)을 구분하는 아키텍처 패턴입니다.

기존 애플리케이션에서는 이 두 가지 책임이 단일 모놀리식 애플리케이션으로 결합되었습니다. CQRS는 이러한 두 가지 책임을 쿼리 응용 프로그램과 명령 응용 프로그램이라는 두 가지 별개의 응용 프로그램으로 구분합니다.

쿼리 애플리케이션은 데이터베이스에서 데이터 검색을 담당합니다. 명령 응용 프로그램은 데이터베이스의 데이터 수정을 담당합니다.

CQRS 패턴은 다양한 방식으로 구현될 수 있습니다. 이 기사에서는 Spring Boot 애플리케이션에서 CQRS를 구현하는 방법에 중점을 둘 것입니다.

## 스프링 부트에서 CQRS 구현

Spring Boot에서 CQRS를 구현하는 두 가지 주요 방법은 `@Query` 주석을 사용하거나 전용 쿼리 서비스를 사용하는 것입니다.

### @Query 주석 사용

`@Query` 주석은 Spring Repository의 메소드에 주석을 추가하는 데 사용할 수 있습니다. 이 메서드는 데이터베이스에 대한 쿼리 실행을 담당합니다.

예를 들어 다음 필드가 있는 `User` 엔터티를 고려하십시오.

```java
@Entity
public class User {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    private String email;

    // Getters and setters omitted for brevity
}
```

`@Query` 주석이 달린 쿼리 메서드로 `UserRepository`를 만들 수 있습니다.

```java
public interface UserRepository extends JpaRepository<User, Long> {

    @Query("SELECT u FROM User u WHERE u.email = :email")
    User findByEmail(@Param("email") String email);

}
```

이 쿼리 메서드는 Spring `@Service`에서 호출할 수 있습니다.

```java
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public User findByEmail(String email) {
        return userRepository.findByEmail(email);
    }

}
```

### 전용 쿼리 서비스 사용

Spring Boot에서 CQRS를 구현하는 또 다른 방법은 전용 쿼리 서비스를 사용하는 것입니다. 이 접근 방식에서는 데이터베이스에서 데이터를 검색하기 위해 별도의 `QueryService`를 만듭니다.

예를 들어 다음 `UserQueryService`를 고려하십시오.

```java
@Service
public class UserQueryService {

    @Autowired
    private UserRepository userRepository;

    public User findByEmail(String email) {
        return userRepository.findByEmail(email);
    }

}
```

이 쿼리 서비스는 Spring `@Controller`에서 호출할 수 있습니다.

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @Autowired
    private UserQueryService userQueryService;

    @GetMapping
    public User findByEmail(@RequestParam("email") String email) {
        return userQueryService.findByEmail(email);
    }

}
```

## 결론

이 기사에서는 Spring Boot 애플리케이션에서 CQRS 패턴을 구현하는 방법을 살펴보았습니다. 우리는 `@Query` 주석을 사용하거나 전용 쿼리 서비스를 사용하는 두 가지 접근 방식을 보았습니다.

애플리케이션에 가장 적합한 접근 방식은 특정 요구 사항에 따라 다릅니다. 간단한 쿼리만 실행해야 하는 경우 `@Query` 주석으로 충분할 수 있습니다. 더 복잡한 쿼리를 실행해야 하거나 쿼리와 명령 책임을 별도로 유지하려는 경우 전용 쿼리 서비스가 더 나은 옵션일 수 있습니다.