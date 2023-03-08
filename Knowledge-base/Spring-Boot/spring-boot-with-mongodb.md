---
title: MongoDB를 사용한 스프링 부트
description: 
published: true
date: 2023-02-07T10:32:36.578Z
tags: 
editor: markdown
dateCreated: 2023-02-07T10:32:34.919Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot with MongoDB***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-with-mongodb)
{.links-list}


# MongoDB로 스프링 부트

Spring Boot는 마이크로서비스 구축에 사용되는 널리 사용되는 Java 기반 프레임워크입니다. "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 응용 프로그램을 만드는 간단한 방법을 제공합니다.

 MongoDB는 문서 지향 데이터 모델을 사용하는 오픈 소스 NoSQL 데이터베이스입니다. 데이터 관리 및 분석을 위한 강력한 도구입니다.

이 기사에서는 Spring Boot를 MongoDB와 연결하는 방법을 보여줍니다.

## 전제 조건

이 문서를 따라 하려면 다음이 필요합니다.

- 자바 8 이상
- 스프링 부트 2.0 이상
- 몽고DB 3.6 이상

## 스프링 부트 프로젝트 생성

Spring Initializr를 사용하여 Spring Boot 프로젝트를 생성합니다.

http://start.spring.io/로 이동하고 다음을 선택합니다.

- 프로젝트: 메이븐 프로젝트
- 언어: 자바
- 스프링 부트: 2.0.3
- 그룹: com.example
- 아티팩트: 데모

**프로젝트 생성**을 클릭합니다.

## 몽고DB 설정

Spring Boot는 `src/main/resources` 디렉토리에서 `application.properties`(또는 `application.yml`)라는 파일을 찾습니다. 여기에서 MongoDB 연결을 구성합니다.

`application.properties` 파일에 다음을 추가합니다.

```
spring.data.mongodb.uri=mongodb://localhost/test
```

그러면 `localhost`에서 `test`라는 MongoDB 데이터베이스에 연결됩니다.

`application.yml`을 사용하는 경우 구성은 다음과 같습니다.

```yaml
spring:
  data:
    mongodb:
      uri: mongodb://localhost/test
```

## MongoDB 저장소 생성

다음으로 MongoDB 데이터베이스에 대한 리포지토리 인터페이스를 생성합니다. 이는 Spring Data MongoDB에서 제공하는 `MongoRepository` 인터페이스를 확장합니다.

```java
package com.example.demo.repository;

import org.springframework.data.mongodb.repository.MongoRepository;

import com.example.demo.model.User;

public interface UserRepository extends MongoRepository<User, String> {

}
```

`UserRepository` 인터페이스는 MongoDB의 `User` 컬렉션에서 CRUD 작업을 수행합니다.

## MongoDB 모델 만들기

이제 `User` 컬렉션의 문서를 나타내는 `User` 클래스를 생성합니다.

```java
package com.example.demo.model;

import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;

@Document
public class User {

    @Id
    private String id;

    private String name;
    private int age;

    // Getters and setters
}
```

`@Document` 주석은 Spring Data MongoDB에 `User` 클래스가 `User` 컬렉션의 문서임을 알려줍니다.

`@Id` 주석은 `id` 필드를 문서의 기본 키로 표시합니다.

## REST 컨트롤러 만들기

이제 MongoDB 리포지토리를 REST API로 노출하는 REST 컨트롤러를 생성합니다.

```java
package com.example.demo.controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

import com.example.demo.model.User;
import com.example.demo.repository.UserRepository;

@RestController
@RequestMapping("/api/v1/users")
public class UserController {

    @Autowired
    private UserRepository userRepository;

    @RequestMapping(method = RequestMethod.GET)
    public List<User> getUsers() {
        return userRepository.findAll();
    }
}
```

`@RestController` 주석은 `UserController` 클래스를 REST 컨트롤러로 표시합니다.

`@RequestMapping` 주석은 HTTP 요청을 컨트롤러의 메서드에 매핑합니다. 이 경우 `/api/v1/users` 경로는 `getUsers()` 메서드에 매핑됩니다.

`@Autowired` 주석은 `UserRepository`를 컨트롤러에 주입합니다.

`getUsers()` 메서드는 MongoDB 데이터베이스에서 사용자 목록을 검색하고 JSON으로 반환합니다.

## 애플리케이션 실행

애플리케이션을 실행하려면 터미널에 다음 명령을 입력하기만 하면 됩니다.

```
./mvnw spring-boot:run
```

다음 출력이 표시되어야 합니다.

```
...
2017-12-01 10:21:59.593  INFO 85511 --- [           main] s.b.c.e.t.TomcatEmbeddedServletContainer : Tomcat started on port(s): 8080 (http)
2017-12-01 10:21:59.596  INFO 85511 --- [           main] com.example.demo.DemoApplication         : Started DemoApplication in 4.166 seconds (JVM running for 4.681)
```

이제 http://localhost:8080/api/v1/users에서 REST API에 액세스할 수 있습니다.

## 결론

이 기사에서는 Spring Boot를 MongoDB와 연결하는 방법을 설명했습니다. MongoDB 데이터베이스에서 CRUD 작업을 위한 간단한 REST API도 만들었습니다.

Spring Boot에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- [스프링 부트 설명서](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/)
- [MongoDB로 스프링 부트 튜토리얼](https://www.baeldung.com/spring-boot-mongodb)

MongoDB에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- [MongoDB 문서](https://docs.mongodb.com/)
- [몽고DB대학교](https://university.mongodb.com/)