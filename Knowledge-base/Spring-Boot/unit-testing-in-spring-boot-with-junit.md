---
title: JUnit을 사용하여 Spring Boot에서 단위 테스트
description: 
published: true
date: 2023-02-01T17:27:43.166Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:27:41.268Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Unit Testing in Spring Boot with JUnit***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/unit-testing-in-spring-boot-with-junit)
{.links-list}


# JUnit을 사용하여 Spring Boot에서 단위 테스트

단위 테스트는 소프트웨어의 개별 단위/구성 요소를 테스트하여 각 단위가 예상대로 작동하는지 확인하는 소프트웨어 테스트 방법입니다. 단위는 응용 프로그램에서 테스트할 수 있는 가장 작은 부분입니다. Spring Boot에서 단위 테스트는 일반적으로 JUnit을 사용하여 작성됩니다.

JUnit은 널리 사용되는 Java용 테스트 프레임워크입니다. Github에서 호스팅되는 오픈 소스 프로젝트입니다. JUnit은 테스트 기반 개발의 개발에서 중요했으며 SUnit에서 시작된 xUnit으로 통칭되는 단위 테스트 프레임워크 제품군 중 하나입니다.

이 기사에서는 JUnit을 사용하여 Spring Boot 애플리케이션을 단위 테스트하는 방법을 살펴보겠습니다. RestController 끝점을 테스트하는 간단한 테스트를 작성합니다. 이 기사의 예제 코드는 Github에서 찾을 수 있습니다.

## 프로젝트 설정

간단한 Spring Boot 프로젝트를 설정하는 것으로 시작하겠습니다. Spring Initializr를 사용하여 프로젝트를 생성합니다. 다음 종속성을 선택합니다.

- 웹
- JPA
- H2 데이터베이스
- 롬복

Lombok은 Java 애플리케이션에서 상용구 코드를 줄이는 데 사용할 수 있는 라이브러리입니다. 테스트를 위해 작성해야 하는 코드의 양을 줄이는 데 사용할 것입니다.

프로젝트가 생성되면 선택한 IDE로 가져올 수 있습니다. IntelliJ IDEA를 사용하겠습니다.

## 단위 테스트 작성

이제 프로젝트가 설정되었으므로 단위 테스트를 작성할 수 있습니다. 먼저 테스트를 위한 새 패키지인 `com.example.demo.controller`를 생성합니다. 이 패키지에서 우리는 `DemoControllerTest`라는 새로운 클래스를 생성할 것입니다.

이 클래스는 `@RunWith(SpringRunner.class)` 및 `@WebMvcTest(DemoController.class)`로 주석 처리됩니다. `@RunWith` 주석은 JUnit에게 `SpringRunner` 클래스를 사용하여 테스트를 실행하도록 지시합니다. `@WebMvcTest` 주석은 Spring MVC 컨트롤러를 테스트하는 데 사용됩니다. Spring MVC를 자동 구성하고 전체 자동 구성을 비활성화합니다.

`DemoControllerTest` 클래스에서 `MockMvc` 개체에 대한 `@Autowired` 필드를 생성합니다. `MockMvc`는 컨트롤러에 대한 HTTP 요청을 수행하고 응답을 주장하는 데 사용됩니다. 또한 `@BeforeEach`로 주석이 달린 `@Before` 메서드도 생성합니다. 이 메서드는 `MockMvc` 개체를 초기화하는 데 사용됩니다.

```java
@RunWith(SpringRunner.class)
@WebMvcTest(DemoController.class)
public class DemoControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @BeforeEach
    public void setup() {
        mockMvc = MockMvcBuilders.webAppContextSetup(webApplicationContext)
                .build();
    }
}
```

`setup` 메소드에서 `MockMvcBuilders` 정적 팩토리 메소드를 사용하여 `MockMvc` 인스턴스를 생성합니다. `webAppContextSetup` 메서드를 사용하고 `WebApplicationContext`를 전달합니다. 그러면 `WebApplicationContext`가 지원하는 `MockMvc` 인스턴스가 생성됩니다.

이제 `MockMvc` 개체가 설정되었으므로 테스트 메서드를 작성할 수 있습니다. 메소드에 `@Test`로 주석을 달 것입니다. 테스트 방법에서는 `MockMvc` 객체를 사용하여 `/demo` 엔드포인트에 대한 HTTP `GET` 요청을 수행합니다. 그런 다음 응답 상태가 '200 OK'이고 응답 내용에 문자열 'Hello, world!'가 포함되어 있다고 주장합니다.

```java
@Test
public void testDemoEndpoint() throws Exception {
    mockMvc.perform(get("/demo"))
            .andExpect(status().isOk())
            .andExpect(content().string(containsString("Hello, world!")));
}
```

HTTP 요청을 수행하기 위해 `MockMvc` 객체에서 `perform` 메소드를 사용합니다. `get` 메소드를 사용하여 `GET` 요청을 생성합니다. 그런 다음 `andExpect` 메서드를 사용하여 응답 상태와 내용을 확인합니다.

## 테스트 실행

이제 테스트를 실행할 수 있습니다. `./mvnw test` 명령을 사용하여 명령줄에서 테스트를 실행할 수 있습니다. IDE 내에서 테스트를 실행할 수도 있습니다.

## 결론

이 기사에서는 JUnit을 사용하여 Spring Boot 애플리케이션을 단위 테스트하는 방법을 살펴보았습니다. 우리는 RestController 엔드포인트를 테스트하기 위한 간단한 테스트를 작성했습니다.