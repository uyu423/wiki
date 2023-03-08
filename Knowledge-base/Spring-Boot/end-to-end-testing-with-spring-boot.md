---
title: Spring Boot를 사용한 종단 간 테스트
description: 
published: true
date: 2023-02-01T17:40:25.879Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:40:23.615Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [End-to-end Testing with Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/end-to-end-testing-with-spring-boot)
{.links-list}


# Spring Boot로 End-to-End 테스팅

웹 애플리케이션을 구축할 때 종단 간(E2E) 테스트는 개발 프로세스의 핵심 부분입니다. 정의에 따라 E2E 테스트는 처음부터 끝까지 전체 애플리케이션을 다루는 테스트 유형입니다.

전통적인 웹 애플리케이션에서 프런트엔드 코드는 백엔드 서버에 요청을 보낸 다음 요청을 처리하고 응답을 반환합니다. Spring Boot 애플리케이션을 사용하면 프런트 엔드 코드는 여전히 요청을 생성하지만 백엔드 서버는 이제 Spring Boot 애플리케이션입니다.

E2E 테스트는 개발자가 사용자 인터페이스(UI)에서 백엔드 서버에 이르기까지 전체 애플리케이션을 테스트할 수 있기 때문에 중요합니다. 또한 개발자는 응용 프로그램이 프로덕션 환경에 배포될 때 어떻게 작동하는지 테스트할 수 있습니다.

사용 가능한 다양한 E2E 테스트 프레임워크가 있지만 이 기사에서는 Spring Boot 및 Spring Boot에서 제공하는 E2E 테스트 프레임워크에 중점을 둘 것입니다.

## 스프링부트란?

Spring Boot는 개발자가 Spring 기반 애플리케이션을 빠르게 만들고 배포할 수 있게 해주는 프레임워크입니다. 다음과 같이 개발 및 배포를 더 쉽게 만드는 여러 기능을 제공합니다.

- 임베디드 톰캣 서버
- 자동 구성
- 스타터 템플릿

Spring Boot는 Spring 기반 애플리케이션을 쉽게 생성하고 배포할 수 있기 때문에 E2E 테스트 개발에 탁월한 선택입니다.

## E2E 테스트 프레임워크가 무엇인가요?

E2E 테스트 프레임워크는 개발자가 E2E 테스트를 신속하게 생성하고 실행할 수 있는 도구 세트입니다. JUnit 테스트 프레임워크를 기반으로 하며 다음과 같이 E2E 테스트를 더 쉽게 만드는 여러 기능을 제공합니다.

- 테스트를 위해 Spring Boot 애플리케이션을 구성하는 데 사용할 수 있는 @SpringBootTest 주석
- 테스트를 위해 웹 서버를 구성하는 데 사용할 수 있는 @WebIntegrationTest 주석
- Spring 애플리케이션 컨텍스트에서 bean을 조롱하는 데 사용할 수 있는 @MockBean 주석

E2E 테스트 프레임워크는 E2E 테스트를 쉽게 만들고 실행할 수 있기 때문에 E2E 테스트를 개발하기 위한 훌륭한 선택입니다.

## E2E 테스트 만들기

이제 E2E 테스트 프레임워크를 사용하여 E2E 테스트를 만드는 방법을 살펴보겠습니다. 사용자 목록을 반환하는 단일 엔드포인트가 있는 간단한 Spring Boot 애플리케이션을 테스트할 것입니다.

가장 먼저 해야 할 일은 새 JUnit 테스트 클래스를 만들고 @SpringBootTest로 주석을 추가하는 것입니다.

```java
@SpringBootTest
public class UserControllerTest {

}
```

@SpringBootTest 주석은 테스트를 위해 Spring Boot 애플리케이션을 구성하는 데 사용됩니다.

다음으로 테스트 메서드를 만들고 @Test로 주석을 추가해야 합니다.

```java
@Test
public void testGetUsers() {

}
```

@Test 어노테이션은 메소드를 테스트 메소드로 표시하는 데 사용됩니다.

테스트 메서드에서 UserController 인스턴스를 만들고 getUsers() 메서드를 호출해야 합니다.

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
}
```

getUsers() 메서드는 사용자 목록을 반환하므로 목록이 비어 있지 않음을 확인할 수 있습니다.

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
    assertThat(users).isNotEmpty();
}
```

목록에 예상 사용자 수가 포함되어 있다고 주장할 수도 있습니다.

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
    assertThat(users).hasSize(2);
}
```

마지막으로 목록에 예상 사용자가 포함되어 있다고 주장할 수 있습니다.

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
    assertThat(users)
        .contains(new User("user1@example.com", "User 1"),
                  new User("user2@example.com", "User 2"));
}
```

전체 E2E 테스트는 다음과 같습니다.

```java
@SpringBootTest
public class UserControllerTest {

    @Test
    public void testGetUsers() {
        UserController userController = new UserController();
        List<User> users = userController.getUsers();
        assertThat(users)
            .contains(new User("user1@example.com", "User 1"),
                      new User("user2@example.com", "User 2"));
    }
}
```

## E2E 테스트 실행

E2E 테스트를 실행하려면 테스트 클래스를 JUnit 테스트로 실행하기만 하면 됩니다.

```java
@SpringBootTest
public class UserControllerTest {

    @Test
    public void testGetUsers() {
        UserController userController = new UserController();
        List<User> users = userController.getUsers();
        assertThat(users)
            .contains(new User("user1@example.com", "User 1"),
                      new User("user2@example.com", "User 2"));
    }
}
```

## 결론

이 기사에서는 E2E 테스트 프레임워크를 사용하여 E2E 테스트를 만들고 실행하는 방법을 살펴보았습니다. @SpringBootTest 및 @Test 주석을 사용하여 Spring Boot 애플리케이션을 구성하고 메서드를 테스트 메서드로 표시하는 방법도 살펴보았습니다.