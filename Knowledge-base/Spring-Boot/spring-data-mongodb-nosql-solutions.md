---
title: Spring Data MongoDB: NoSQL 솔루션
description: 
published: true
date: 2023-02-17T18:02:14.406Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:02:43.545Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Spring Data MongoDB: NoSQL Solutions***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-data-mongodb-nosql-solutions)
{.links-list}


# Spring Data MongoDB: NoSQL 솔루션

MongoDB는 C++로 작성된 오픈 소스 문서 지향 데이터베이스 관리 시스템(DBMS)입니다. 데이터 관리 및 분석을 위한 강력한 도구입니다. Spring Data MongoDB는 MongoDB에 대한 높은 수준의 추상화를 제공하는 라이브러리입니다.

이 기사에서는 Spring Data MongoDB를 사용하여 NoSQL 솔루션을 개발하는 방법에 대해 설명합니다. 다음 주제를 다룰 것입니다.

* MongoDB 데이터베이스 설정
* Spring Data MongoDB 저장소 개발
* Spring Data MongoDB로 데이터 쿼리하기

## MongoDB 데이터베이스 설정

Spring Data MongoDB 리포지토리 개발을 시작하기 전에 MongoDB 데이터베이스를 설정해야 합니다. Docker를 사용하여 이 작업을 수행할 수 있습니다.

```
$ docker run -d -p 27017:27017 --name mongodb mongo
```

이렇게 하면 MongoDB 컨테이너가 시작되고 호스트 시스템에서 MongoDB 포트(27017)가 노출됩니다.

## Spring Data MongoDB 저장소 개발

이제 MongoDB 데이터베이스가 가동되어 실행 중이므로 Spring Data MongoDB 리포지토리 개발을 시작할 수 있습니다.

다음 종속성을 사용하여 Maven 프로젝트를 생성하는 것으로 시작합니다.

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.data</groupId>
        <artifactId>spring-data-mongodb</artifactId>
        <version>2.1.11.RELEASE</version>
    </dependency>
</dependencies>
```

다음으로 Spring Data MongoDB 리포지토리를 구성해야 합니다. `application.properties` 파일에 다음을 추가하여 이를 수행할 수 있습니다.

```properties
spring.data.mongodb.uri=mongodb://localhost/test
```

이렇게 하면 Spring Data MongoDB 리포지토리가 MongoDB 데이터베이스에 연결되도록 구성됩니다.

이제 Spring Data MongoDB 리포지토리가 구성되었으므로 Entity 클래스 개발을 시작할 수 있습니다. 먼저 `User` 클래스를 생성합니다:

```java
@Document
public class User {
 
    @Id
    private String id;
 
    private String name;
 
    private int age;
 
    // Getters and setters
}
```

`@Document` 주석은 이 클래스가 문서임을 Spring Data MongoDB에 알려줍니다. `@Id` 주석은 Spring Data MongoDB에 `id` 필드가 이 문서의 기본 키임을 알려줍니다.

이제 `User` 클래스를 정의했으므로 `UserRepository` 인터페이스를 만들 수 있습니다.

```java
@Repository
public interface UserRepository extends MongoRepository<User, String> {
 
    User findByName(String name);
 
}
```

`@Repository` 주석은 Spring에게 이것이 저장소임을 알려줍니다. `MongoRepository` 확장 인터페이스는 `User` 클래스에 대한 기본 CRUD 작업을 제공합니다. `findByName` 메서드는 우리가 정의한 사용자 지정 쿼리입니다.

이제 `UserRepository` 인터페이스가 정의되었으므로 서비스 클래스를 작성할 수 있습니다.

```java
@Service
public class UserService {
 
    @Autowired
    private UserRepository userRepository;
 
    public User createUser(User user) {
        return userRepository.save(user);
    }
 
    public User findUserById(String id) {
        return userRepository.findById(id).orElse(null);
    }
 
    public User findUserByName(String name) {
        return userRepository.findByName(name);
    }
 
}
```

`@Service` 주석은 이것이 서비스 클래스임을 Spring에 알려줍니다. `@Autowired` 주석은 이 클래스에 `UserRepository`를 주입하도록 Spring에 지시합니다.

`createUser` 메서드는 `User` 문서를 MongoDB 데이터베이스에 저장합니다. `findUserById` 및 `findUserByName` 메서드는 MongoDB 데이터베이스에서 `User` 문서를 쿼리합니다.

이제 서비스 클래스를 정의했으므로 컨트롤러 클래스를 작성할 수 있습니다.

```java
@RestController
public class UserController {
 
    @Autowired
    private UserService userService;
 
    @PostMapping("/user")
    public User createUser(@RequestBody User user) {
        return userService.createUser(user);
    }
 
    @GetMapping("/user/{id}")
    public User findUserById(@PathVariable String id) {
        return userService.findUserById(id);
    }
 
    @GetMapping("/user/name/{name}")
    public User findUserByName(@PathVariable String name) {
        return userService.findUserByName(name);
    }
 
}
```

`@RestController` 주석은 이것이 컨트롤러 클래스임을 Spring에 알려줍니다. `@Autowired` 주석은 Spring이 이 클래스에 `UserService`를 주입하도록 지시합니다.

`@PostMapping` 주석은 `createUser` 메서드를 `POST /user` 엔드포인트에 매핑합니다. `@GetMapping` 주석은 `findUserById` 및 `findUserByName` 메서드를 각각 `GET /user/{id}` 및 `GET /user/name/{name}` 엔드포인트에 매핑합니다.

## Spring Data MongoDB로 데이터 쿼리하기

이제 Spring Data MongoDB 리포지토리를 정의했으므로 데이터 쿼리를 시작할 수 있습니다.

`사용자` 문서를 생성하여 시작하겠습니다.

```java
User user = new User();
user.setName("John Doe");
user.setAge(30);
 
userService.createUser(user);
```

그러면 MongoDB 데이터베이스에 "John Doe"라는 이름과 나이가 30인 `User` 문서가 생성됩니다.

`findUserById` 및 `findUserByName` 메서드를 사용하여 이 `User` 문서에 대해 MongoDB 데이터베이스를 쿼리할 수 있습니다.

```java
User user = userService.findUserById("123");
 
User user = userService.findUserByName("John Doe");
```

이 두 가지 방법 모두 이름이 "John Doe"이고 연령이 30인 `User` 문서를 반환합니다.

또한 `MongoRepository` 인터페이스를 사용하여 데이터를 쿼리할 수 있습니다. `MongoRepository` 인터페이스는 다음 메서드를 제공합니다.

* `save` - 문서를 MongoDB 데이터베이스에 저장합니다.
* `삽입` - MongoDB 데이터베이스에 문서를 삽입합니다.
* `findById` - id로 문서를 찾습니다.
* `findAll` - 모든 문서를 찾습니다.
* `findAllById` - ID로 모든 문서를 찾습니다.
* `count` - 문서의 수를 센다.
* `deleteById` - 해당 ID로 문서를 삭제합니다.
* `delete` - 문서를 삭제합니다.
* `deleteAll` - 모든 문서를 삭제합니다.

이러한 방법을 사용하여 보다 유연한 방식으로 데이터를 쿼리할 수 있습니다.

## 결론

이 기사에서는 Spring Data MongoDB를 사용하여 NoSQL 솔루션을 개발하는 방법에 대해 설명했습니다. 우리는 다음 주제를 다루었습니다.

* MongoDB 데이터베이스 설정
* Spring Data MongoDB 저장소 개발
* Spring Data MongoDB로 데이터 쿼리하기