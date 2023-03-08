---
title: 024: Spring Boot 애플리케이션에서 페이지 매김 구현
description: 
published: true
date: 2023-02-03T16:32:20.194Z
tags: 
editor: markdown
dateCreated: 2023-02-03T16:32:18.613Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [024: Implementing pagination in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/024-implementing-pagination-in-a-spring-boot-application)
{.links-list}


페이지 매김은 웹 애플리케이션의 일반적인 기능입니다. 큰 데이터 세트를 더 작고 관리하기 쉬운 청크로 나누는 데 사용됩니다. Spring Boot를 사용하면 웹 애플리케이션에서 페이지 매김을 쉽게 구현할 수 있습니다.

이번 포스트에서는 Spring Boot 애플리케이션에서 페이지네이션을 구현하는 방법에 대해 알아보겠습니다. 간단한 Spring Boot 애플리케이션을 만드는 것부터 시작하겠습니다. 그런 다음 응용 프로그램에 페이지 매김 기능을 추가합니다.

스프링 부트 애플리케이션 생성

Spring Initializr를 사용하여 Spring Boot 애플리케이션을 생성합니다. Spring Initializr 웹 사이트로 이동하여 다음 옵션을 선택합니다.

* 프로젝트: 메이븐 프로젝트
* 언어: 자바
* 스프링 부트 버전: 2.1.3

"생성" 버튼을 클릭하여 프로젝트를 생성합니다.

프로젝트가 생성되면 원하는 IDE로 가져옵니다. 이클립스를 사용하고 있습니다.

페이지 매김 기능 추가

org.springframework.data.domain 패키지의 Pageable 인터페이스를 사용하여 애플리케이션에서 페이지 매김을 구현합니다.

먼저 pom.xml 파일에 spring-data-commons 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-commons</artifactId>
    <version>2.1.3.RELEASE</version>
</dependency>
```

다음으로 사용자 목록을 반환하는 메서드를 사용하여 간단한 RestController를 만듭니다.

```java
@RestController
public class UserController {

    @GetMapping("/users")
    public List<User> getUsers() {
        // Return a list of users
    }
}
```

이제 getUsers() 메서드에 페이지 매김 기능을 추가하겠습니다. Pageable 인터페이스를 사용하여 페이지 크기와 페이지 번호를 지정합니다. Pageable 인터페이스에는 PageRequest 및 Slice의 두 가지 구현이 있습니다. 예제에서는 PageRequest 구현을 사용합니다.

```java
@GetMapping("/users")
public List<User> getUsers(Pageable pageable) {
    // Return a list of users
}
```

페이지 크기와 페이지 번호를 쿼리 매개변수로 지정할 수도 있습니다.

```java
@GetMapping("/users")
public List<User> getUsers(
        @RequestParam(name = "page", defaultValue = "0") int page,
        @RequestParam(name = "size", defaultValue = "10") int size) {
    // Return a list of users
}
```

위의 예에서 기본 페이지 크기는 10이고 기본 페이지 번호는 0으로 지정했습니다.

페이지 매김 기능 테스트

페이지 및 크기 쿼리 매개변수를 사용하여 /users 끝점에 GET 요청을 전송하여 페이지 매김 기능을 테스트할 수 있습니다.

예를 들어 다음 요청은 페이지 크기가 10인 사용자의 첫 번째 페이지를 반환합니다.

```
GET /users?page=0&size=10
```

다음 요청은 페이지 크기가 10인 사용자의 두 번째 페이지를 반환합니다.

```
GET /users?page=1&size=10
```

등등.

추가 정보

Pageable 인터페이스에는 페이지 매김 동작을 사용자 정의하는 데 사용할 수 있는 몇 가지 다른 방법이 있습니다. 자세한 내용은 Pageable 인터페이스에 대한 JavaDocs를 참조하십시오.

경고

페이지 매김을 구현할 때 페이지 크기가 너무 크지 않도록 하는 것이 중요합니다. 페이지 크기가 너무 크면 OutOfMemoryErrors가 발생할 수 있습니다.

위험

페이지 매김을 구현할 때 페이지 크기가 너무 작지 않은지 확인하는 것이 중요합니다. 페이지 크기가 너무 작으면 너무 많은 데이터베이스 쿼리가 발생할 수 있습니다.