---
title: JUnit을 사용한 스프링 부트 테스트
description: 
published: true
date: 2023-02-07T19:32:31.718Z
tags: 
editor: markdown
dateCreated: 2023-02-07T19:32:25.883Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Testing with JUnit***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-testing-with-junit)
{.links-list}


# JUnit을 사용한 스프링 부트 테스트

테스트는 모든 소프트웨어 개발 프로세스의 중요한 부분입니다. 코드가 예상대로 작동하는지 확인하고 버그를 조기에 발견하는 데 도움이 됩니다.

JUnit은 널리 사용되는 Java용 단위 테스트 프레임워크입니다. Spring Boot는 JUnit 테스트를 위한 최고 수준의 지원을 제공합니다. 이 기사에서는 JUnit으로 Spring Boot 테스트를 설정하고 작성하는 방법을 살펴보겠습니다.

## 설정

시작하려면 `pom.xml`에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

`spring-boot-starter-test` 종속성에는 JUnit, Hamcrest 및 Mockito를 포함하여 테스트 작성에 유용한 여러 라이브러리가 포함되어 있습니다.

## 테스트 작성

Spring Boot 테스트는 JUnit 4 또는 JUnit 5로 작성할 수 있습니다. 이 섹션에서는 각각의 예를 살펴보겠습니다.

### JUnit 4

다음은 JUnit 4 테스트의 간단한 예입니다.

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class MyTest {

    @Test
    public void test() {
        // test code goes here
    }

}
```

`@RunWith` 주석은 사용할 테스트 프레임워크를 지정하는 데 사용됩니다. `@SpringBootTest` 주석은 테스트를 위한 애플리케이션 컨텍스트를 로드하도록 Spring Boot에 지시합니다.

`@Test` 주석은 메서드를 테스트 메서드로 표시하는 데 사용됩니다.

### JUnit 5

JUnit 5 테스트는 JUnit 4 테스트와 비슷해 보이지만 몇 가지 주요 차이점이 있습니다.

```java
@SpringBootTest
public class MyTest {

    @Test
    public void test() {
        // test code goes here
    }

}
```

첫째, `@RunWith` 주석이 더 이상 필요하지 않습니다. 둘째, `@Test` 주석은 이제 `org.junit.jupiter.api` 패키지에 속합니다.

JUnit 5는 또한 `org.junit.jupiter.api.Assertions` 클래스에서 찾을 수 있는 새로운 어설션 집합을 도입합니다. 예를 들어 'assertEquals' 어설션은 다음과 같이 사용할 수 있습니다.

```java
assertEquals(expected, actual);
```

## 테스트SpringBootApplicationTests

Spring Boot는 테스트 작성에 유용한 여러 가지 주석을 제공합니다. 이 섹션에서는 가장 일반적으로 사용되는 몇 가지 주석을 살펴보겠습니다.

### @WebMvcTest

`@WebMvcTest` 주석은 Spring MVC 컨트롤러를 테스트하는 데 사용됩니다. 다음과 같이 사용할 수 있습니다.

```java
@WebMvcTest(MyController.class)
public class MyControllerTest {

    @Autowired
    private MockMvc mvc;

    @Test
    public void test() {
        // test code goes here
    }

}
```

`@WebMvcTest` 주석은 Spring MVC 테스트에 필요한 구성 요소만 로드합니다. 이는 테스트를 위해 애플리케이션 컨텍스트를 로드하는 데 걸리는 시간을 줄이는 데 유용할 수 있습니다.

`@Autowired` 주석은 `MockMvc` 빈을 주입하는 데 사용됩니다. `MockMvc` 빈은 컨트롤러에 HTTP 요청을 보내고 응답을 확인하는 데 사용할 수 있습니다.

### @DataJpa테스트

`@DataJpaTest` 주석은 Spring Data JPA 저장소를 테스트하는 데 사용됩니다. 다음과 같이 사용할 수 있습니다.

```java
@DataJpaTest
public class MyRepositoryTest {

    @Autowired
    private MyRepository repository;

    @Test
    public void test() {
        // test code goes here
    }

}
```

`@DataJpaTest` 주석은 Spring Data JPA 테스트에 필요한 구성 요소만 로드합니다. 이는 테스트를 위해 애플리케이션 컨텍스트를 로드하는 데 걸리는 시간을 줄이는 데 유용할 수 있습니다.

`@Autowired` 주석은 `MyRepository` 빈을 주입하는 데 사용됩니다. 이 bean은 데이터베이스의 데이터에 액세스하는 데 사용할 수 있습니다.

### @RestClientTest

`@RestClientTest` 주석은 Spring RestTemplate 클라이언트를 테스트하는 데 사용됩니다. 다음과 같이 사용할 수 있습니다.

```java
@RestClientTest(MyClient.class)
public class MyClientTest {

    @Autowired
    private MockRestTemplate template;

    @Test
    public void test() {
        // test code goes here
    }

}
```

`@RestClientTest` 주석은 Spring RestTemplate 테스트에 필요한 구성 요소만 로드합니다. 이는 테스트를 위해 애플리케이션 컨텍스트를 로드하는 데 걸리는 시간을 줄이는 데 유용할 수 있습니다.

`@Autowired` 주석은 `MockRestTemplate` 빈을 주입하는 데 사용됩니다. `MockRestTemplate` 빈은 HTTP 요청을 클라이언트에 보내고 응답을 확인하는 데 사용할 수 있습니다.

## 결론

이 기사에서는 Spring Boot 및 JUnit을 사용하여 테스트를 설정하고 작성하는 방법을 살펴보았습니다. 또한 테스트 작성에 가장 일반적으로 사용되는 주석도 보았습니다.