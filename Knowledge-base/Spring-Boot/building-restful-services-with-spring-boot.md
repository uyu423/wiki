---
title: Spring Boot로 RESTful 서비스 구축
description: 
published: true
date: 2023-01-31T16:38:08.795Z
tags: 
editor: markdown
dateCreated: 2023-01-31T16:38:07.161Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Building RESTful Services with Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/building-restful-services-with-spring-boot)
{.links-list}


# Spring Boot로 RESTful 서비스 구축

이 기사에서는 Spring Boot로 RESTful 웹 서비스를 구축하기 위한 몇 가지 모범 사례를 살펴보겠습니다.

다음 주제를 다룹니다.

* REST API 설계
* RESTful 엔드포인트 설계를 위한 모범 사례
* Spring Boot로 REST API 구현
* REST API 테스트
* REST API 보안

## REST API 설계

REST API를 설계할 때 다음 요소를 고려하는 것이 중요합니다.

* API가 공개할 리소스
* 해당 리소스에서 수행할 수 있는 작업
* 리소스 간의 관계

API는 개발자가 쉽게 사용할 수 있는 방식으로 설계되어야 합니다. 이해하고 사용하기 쉬워야 하며 일관성이 있어야 합니다.

API의 끝점을 설계할 때 일관된 명명 규칙을 사용해야 합니다. 예를 들어 다음 규칙을 사용할 수 있습니다.

```
/{resource}/{id}
```

여기서 {resource}는 리소스의 이름이고 {id}는 리소스의 식별자입니다.

일관된 방식으로 HTTP 메서드를 사용하는 것도 좋은 생각입니다. 예를 들어 다음 규칙을 사용할 수 있습니다.

```
GET /{resource}/{id}
POST /{resource}
PUT /{resource}/{id}
DELETE /{resource}/{id}
```

여기서 GET은 리소스를 검색하는 데 사용되고 POST는 리소스를 만드는 데 사용되며 PUT은 리소스를 업데이트하는 데 사용되며 DELETE는 리소스를 삭제하는 데 사용됩니다.

## RESTful 엔드포인트 설계를 위한 모범 사례

API에 대한 엔드포인트를 설계할 때 염두에 두어야 할 몇 가지 모범 사례가 있습니다.

* 리소스에 대한 복수 이름 사용
* 하이픈을 사용하여 단어 구분
* 소문자 사용
* 일관된 방식으로 HTTP 메서드 사용
* 일관된 방식으로 HTTP 상태 코드 사용

## Spring Boot로 REST API 구현

이제 REST API 설계를 위한 몇 가지 모범 사례를 다루었으므로 Spring Boot로 REST API를 구현하는 방법을 살펴보겠습니다.

Spring Boot를 사용하면 "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다. Spring Boot를 사용하여 단일 리소스를 노출하는 간단한 API를 생성합니다.

### 종속성

먼저 프로젝트에 다음 종속성을 추가해야 합니다.

* spring-boot-starter-data-rest
* spring-boot-starter-data-jpa
* 스프링 부트 스타터 웹

### 엔터티

엔터티를 생성하여 시작하겠습니다. 엔터티 이름에 다음 규칙을 사용합니다.

```
{resource}_{operation}
```

여기서 {resource}는 리소스의 이름이고 {operation}은 리소스에서 수행 중인 작업입니다.

이 예에서는 `user_create`라는 엔티티를 생성합니다.

```java
@Entity
@Table(name = "user_create")
public class UserCreate {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "name")
    private String name;

    @Column(name = "email")
    private String email;

    // getters and setters
}
```

### 저장소

다음으로 엔터티에 대한 리포지토리를 만듭니다. 리포지토리 이름에 다음 규칙을 사용합니다.

```
{resource}Repository
```

여기서 {resource}는 리소스의 이름입니다.

이 예에서는 `UserCreateRepository`라는 리포지토리를 만듭니다.

```java
public interface UserCreateRepository extends JpaRepository<UserCreate, Long> {

}
```

### 서비스

이제 엔터티에 대한 서비스를 만듭니다. 서비스 이름에 다음 규칙을 사용합니다.

```
{resource}Service
```

여기서 {resource}는 리소스의 이름입니다.

이 예에서는 `UserCreateService`라는 서비스를 만듭니다.

```java
@Service
public class UserCreateService {

    @Autowired
    private UserCreateRepository userCreateRepository;

    public UserCreate create(UserCreate userCreate) {
        return userCreateRepository.save(userCreate);
    }
}
```

### 컨트롤러

마지막으로 엔터티에 대한 컨트롤러를 만듭니다. 컨트롤러 이름에 다음 규칙을 사용합니다.

```
{resource}Controller
```

여기서 {resource}는 리소스의 이름입니다.

이 예에서는 `UserCreateController`라는 컨트롤러를 만듭니다.

```java
@RestController
@RequestMapping("/user-creates")
public class UserCreateController {

    @Autowired
    private UserCreateService userCreateService;

    @PostMapping
    public UserCreate create(@RequestBody UserCreate userCreate) {
        return userCreateService.create(userCreate);
    }
}
```

이것이 Spring Boot로 간단한 REST API를 생성하기 위해 해야 할 전부입니다.

## REST API 테스트

REST API를 테스트할 때 염두에 두어야 할 몇 가지 사항이 있습니다.

* 끝점에 액세스할 수 있어야 합니다.
* 엔드포인트는 예상 데이터를 반환해야 합니다.
* 엔드포인트는 예상되는 HTTP 상태 코드를 반환해야 합니다.

예제 API를 테스트하기 위해 다음 curl 명령을 사용할 수 있습니다.

```
# create a user
curl -X POST -H "Content-Type: application/json" -d '{"name":"John Doe","email":"john.doe@example.com"}' http://localhost:8080/user-creates

# get a user
curl -X GET http://localhost:8080/user-creates/1

# update a user
curl -X PUT -H "Content-Type: application/json" -d '{"name":"John Doe","email":"john.doe@example.com"}' http://localhost:8080/user-creates/1

# delete a user
curl -X DELETE http://localhost:8080/user-creates/1
```

## REST API 보안

REST API를 보호할 때 염두에 두어야 할 몇 가지 사항이 있습니다.

* 인증
* 승인
* 속도 제한

인증은 사용자의 ID를 확인하는 프로세스입니다. 권한 부여는 사용자가 수행할 수 있는 작업을 결정하는 프로세스입니다. 속도 제한은 사용자가 만들 수 있는 요청 수를 제한하는 프로세스입니다.

REST API를 보호하는 방법에는 여러 가지가 있지만 가장 널리 사용되는 방법 중 하나는 JWT(JSON 웹 토큰)를 사용하는 것입니다.

JWT로 예제 API를 보호하기 위해 다음 curl 명령을 사용할 수 있습니다.

```
# login
curl -X POST -H "Content-Type: application/json" -d '{"username":"john.doe","password":"password"}' http://localhost:8080/auth/login

# get a user
curl -X GET -H "Authorization: Bearer <token>" http://localhost:8080/user-creates/1

# logout
curl -X POST -H "Authorization: Bearer <token>" http://localhost:8080/auth/logout
```

## 결론

이 기사에서는 Spring Boot로 RESTful 웹 서비스를 구축하기 위한 몇 가지 모범 사례를 다루었습니다. REST API를 설계하는 방법, Spring Boot로 REST API를 구현하는 방법, REST API를 테스트하는 방법 및 REST API를 보호하는 방법을 살펴보았습니다.