---
title: Kotlin 및 Spring 데이터: 데이터베이스에 연결
description: 
published: true
date: 2023-02-08T09:17:31.308Z
tags: 
editor: markdown
dateCreated: 2023-02-08T09:17:29.679Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and Spring Data: Connecting to a Database***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-spring-data-connecting-to-a-database)
{.links-list}


# 코틀린과 스프링 데이터: 데이터베이스에 연결하기

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어이며 JavaScript 소스 코드로 컴파일할 수도 있습니다. Kotlin은 JetBrains에서 개발했습니다.

Spring Data는 Spring Framework에서 관계형 데이터베이스와 같은 데이터 액세스 기술을 보다 쉽게 사용할 수 있도록 하는 프로젝트입니다.

이 기사에서는 Kotlin 및 Spring Data를 사용하여 데이터베이스에 연결하는 방법을 살펴봅니다.

## 프로젝트 설정

먼저 Spring Initializr를 사용하여 새로운 Kotlin 프로젝트를 생성해야 합니다. 다음 종속성을 선택해야 합니다.

- 웹
- 스프링 데이터 JPA
- H2 데이터베이스

![spring-initializr](https://i.imgur.com/G9dLNcJ.png)

프로젝트가 생성되면 선호하는 IDE로 가져올 수 있습니다. IntelliJ IDEA를 사용하겠습니다.

## 데이터 소스 구성

다음으로 DataSource를 구성해야 합니다. `application.properties` 파일에 다음을 추가하여 이를 수행할 수 있습니다.

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

spring.jpa.generate-ddl=true
spring.jpa.hibernate.ddl-auto=create-drop
```

`spring.datasource.url` 속성은 데이터베이스의 URL을 정의합니다. `spring.datasource.driverClassName` 속성은 드라이버 클래스 이름을 정의합니다. `spring.datasource.username` 속성은 사용자 이름을 정의합니다. `spring.datasource.password` 속성은 비밀번호를 정의합니다.

`spring.jpa.generate-ddl` 속성은 Spring Data에게 데이터베이스 스키마를 생성하도록 지시합니다. `spring.jpa.hibernate.ddl-auto` 속성은 Hibernate에게 데이터베이스 스키마를 생성하고 삭제하도록 지시합니다.

## 엔터티 만들기

다음으로 엔터티를 만들어야 합니다. 엔터티는 데이터베이스의 테이블을 나타내는 클래스입니다. `@Entity` 주석으로 클래스에 주석을 달아 엔티티를 생성할 수 있습니다.

```kotlin
@Entity
class User(
        @Id @GeneratedValue val id: Long,
        val name: String,
        val age: Int
)
```

`@Entity` 주석은 이것이 엔티티임을 나타냅니다. `@Id` 주석은 `id` 속성이 기본 키임을 나타냅니다. `@GeneratedValue` 주석은 `id` 속성이 데이터베이스에서 생성되어야 함을 나타냅니다.

`name` 및 `age` 속성은 데이터베이스의 열에 매핑됩니다.

## 저장소 생성

다음으로 저장소를 만들어야 합니다. 리포지토리는 데이터베이스의 데이터에 대한 액세스를 제공하는 클래스입니다. `@Repository` 주석으로 클래스에 주석을 달아 리포지토리를 만들 수 있습니다.

```kotlin
@Repository
interface UserRepository : CrudRepository<User, Long>
```

`@Repository` 주석은 이것이 저장소임을 나타냅니다. `CrudRepository` 인터페이스는 CRUD 작업을 위한 메서드를 제공합니다.

## 서비스 만들기

다음으로 서비스를 만들어야 합니다. 서비스는 비즈니스 로직을 포함하는 클래스입니다. `@Service` 주석으로 클래스에 주석을 달아 서비스를 만들 수 있습니다.

```kotlin
@Service
class UserService(
        private val userRepository: UserRepository
) {
    fun createUser(user: User): User {
        return userRepository.save(user)
    }

    fun getUserById(id: Long): User? {
        return userRepository.findById(id).orElse(null)
    }

    fun getAllUsers(): List<User> {
        return userRepository.findAll().toList()
    }

    fun updateUser(user: User): User {
        return userRepository.save(user)
    }

    fun deleteUserById(id: Long) {
        userRepository.deleteById(id)
    }
}
```

`@Service` 주석은 이것이 서비스임을 나타냅니다. `createUser` 메소드는 새 사용자를 생성합니다. `getUserById` 메소드는 ID로 사용자를 가져옵니다. `getAllUsers` 메소드는 모든 사용자를 가져옵니다. `updateUser` 메소드는 사용자를 업데이트합니다. `deleteUserById` 메서드는 id로 사용자를 삭제합니다.

## 컨트롤러 만들기

마지막으로 컨트롤러를 만들어야 합니다. 컨트롤러는 HTTP 요청을 처리하는 메서드를 포함하는 클래스입니다. `@RestController` 주석으로 클래스에 주석을 달아 컨트롤러를 만들 수 있습니다.

```kotlin
@RestController
@RequestMapping("/users")
class UserController(
        private val userService: UserService
) {
    @PostMapping
    fun createUser(@RequestBody user: User): User {
        return userService.createUser(user)
    }

    @GetMapping("/{id}")
    fun getUserById(@PathVariable id: Long): User? {
        return userService.getUserById(id)
    }

    @GetMapping
    fun getAllUsers(): List<User> {
        return userService.getAllUsers()
    }

    @PutMapping
    fun updateUser(@RequestBody user: User): User {
        return userService.updateUser(user)
    }

    @DeleteMapping("/{id}")
    fun deleteUserById(@PathVariable id: Long) {
        userService.deleteUserById(id)
    }
}
```

`@RestController` 주석은 이것이 컨트롤러임을 나타냅니다. `@RequestMapping` 주석은 HTTP 요청을 컨트롤러의 메서드에 매핑합니다. `@PostMapping` 주석은 HTTP POST 요청을 `createUser` 메서드에 매핑합니다. `@GetMapping` 주석은 HTTP GET 요청을 `getUserById` 메서드에 매핑합니다. `@PutMapping` 주석은 HTTP PUT 요청을 `updateUser` 메서드에 매핑합니다. `@DeleteMapping` 주석은 HTTP DELETE 요청을 `deleteUserById` 메서드에 매핑합니다.

## 끝점 테스트

curl 또는 Postman을 사용하여 끝점을 테스트할 수 있습니다.

```
$ curl -X POST localhost:8080/users -d '{"name": "John Doe", "age": 42}' -H "Content-Type: application/json"
{"id":1,"name":"John Doe","age":42}

$ curl localhost:8080/users/1
{"id":1,"name":"John Doe","age":42}

$ curl localhost:8080/users
[{"id":1,"name":"John Doe","age":42}]

$ curl -X PUT localhost:8080/users -d '{"id": 1, "name": "Jane Doe", "age": 43}' -H "Content-Type: application/json"
{"id":1,"name":"Jane Doe","age":43}

$ curl -X DELETE localhost:8080/users/1
```

## 결론

이 기사에서는 Kotlin과 Spring Data를 사용하여 데이터베이스에 연결하는 방법을 살펴보았습니다.