---
title: 063: JUnit과 Mockito로 Spring Boot 애플리케이션 테스트하기
description: 
published: true
date: 2023-02-05T01:32:27.858Z
tags: 
editor: markdown
dateCreated: 2023-02-05T01:32:25.522Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [063: Testing a Spring Boot Application with JUnit and Mockito***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/063-testing-a-spring-boot-application-with-junit-and-mockito)
{.links-list}


# 063: JUnit 및 Mockito로 Spring Boot 애플리케이션 테스트

이 게시물에서는 JUnit 및 Mockito를 사용하여 Spring Boot 애플리케이션을 테스트하는 방법을 배웁니다.

Spring Boot를 사용하면 "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다. 이 예제에서는 작업을 더 쉽게 하기 위해 Spring Boot를 사용할 것입니다.

JUnit은 널리 사용되는 Java용 테스트 프레임워크입니다. Mockito는 모의 개체와 스텁 메서드를 만들 수 있는 Java용 모의 프레임워크입니다.

## 프로젝트 설정

먼저 [Spring Initializr](https://start.spring.io/)를 사용하여 새로운 Spring Boot 프로젝트를 생성합니다. 프로젝트 이름을 `spring-boot-junit-mockito-example`로 지정합니다.

![스프링 이니셜라이저](https://i.imgur.com/HgflTDz.png)

다음으로 `Web` 및 `Actuator` 종속성을 선택합니다. '웹' 종속성은 웹 애플리케이션에 대한 지원을 추가하고 '액추에이터' 종속성은 애플리케이션 모니터링 및 관리에 대한 지원을 추가합니다.

![Spring Initializr 종속성](https://i.imgur.com/sA6qEjK.png)

프로젝트가 생성되면 선호하는 IDE로 가져올 수 있습니다. [IntelliJ IDEA](https://www.jetbrains.com/idea/)를 사용하고 있습니다.

## 테스트 작성

이제 프로젝트가 설정되었으므로 테스트 작성을 시작할 수 있습니다. 새로운 `src/test/java` 디렉토리를 생성하고 새로운 `SpringBootJunitMockitoExampleApplicationTests.java` 파일을 추가합니다.

이 파일에서 Spring Boot 애플리케이션을 시작할 수 있는지 확인하는 간단한 테스트를 추가합니다.

    @RunWith(SpringRunner.class)
    @SpringBootTest
    공개 클래스 SpringBootJunitMockitoExampleApplicationTests {
    
        @시험
        공공 무효 contextLoads() {
        }
    
    }

`@RunWith(SpringRunner.class)` 및 `@SpringBootTest`로 테스트 클래스에 주석을 추가합니다. `@RunWith` 주석은 JUnit에게 `SpringRunner` 클래스를 사용하여 테스트를 실행하도록 지시합니다. `@SpringBootTest` 주석은 Spring Boot가 애플리케이션 컨텍스트를 로드하도록 지시합니다.

`contextLoads()` 테스트 메서드는 컨텍스트를 로드할 수 있는지 확인합니다.

`mvn test` 명령을 사용하여 테스트를 실행할 수 있습니다.

![테스트 실행](https://i.imgur.com/VkzcTGi.png)

## 단위 테스트 작성

이제 애플리케이션을 시작할 수 있음을 확인했으므로 단위 테스트를 작성할 수 있습니다. 단위 테스트는 메서드와 같은 단일 코드 단위의 동작을 확인하는 테스트입니다.

새 `src/test/java` 디렉토리를 만들고 새 `CalculatorTest.java` 파일을 추가합니다. 이 파일에서 `Calculator` 클래스의 `add()` 메서드에 대한 테스트를 추가합니다.

    @RunWith(MockitoJUnitRunner.class)
    공개 클래스 CalculatorTest {
    
        @InjectMocks
        개인 계산기 계산기;
    
        @시험
        공공 무효 testAdd() {
            assertEquals(5, calculator.add(2, 3));
        }
    
    }

`@RunWith(MockitoJUnitRunner.class)`로 테스트 클래스에 주석을 답니다. 이것은 Mockito에게 `MockitoJUnitRunner` 클래스를 사용하여 테스트를 실행하도록 지시합니다.

`@InjectMocks` 주석은 목 객체를 `Calculator` 클래스에 주입합니다. `@Test` 주석은 JUnit에게 `testAdd()` 메서드가 테스트임을 알려줍니다.

`testAdd()` 메서드에서 `assertEquals()` 메서드를 사용하여 `add()` 메서드가 예상 값을 반환하는지 확인합니다.

`mvn test` 명령을 사용하여 테스트를 실행할 수 있습니다.

![테스트 실행](https://i.imgur.com/5BQ7UgI.png)

## 통합 테스트 작성하기

이제 `Calculator` 클래스가 예상대로 작동하는지 확인했으므로 통합 테스트를 작성할 수 있습니다. 통합 테스트는 두 개 이상의 코드 단위 동작을 확인하는 테스트입니다.

새 `src/test/java` 디렉토리를 만들고 새 `CalculatorIntegrationTest.java` 파일을 추가합니다. 이 파일에서 `Calculator` 클래스의 `add()` 메서드에 대한 테스트를 추가합니다.

    @RunWith(SpringRunner.class)
    @SpringBootTest
    공개 클래스 CalculatorIntegrationTest {
    
        @Autowired
        개인 계산기 계산기;
    
        @시험
        공공 무효 testAdd() {
            assertEquals(5, calculator.add(2, 3));
        }
    
    }

`@RunWith(SpringRunner.class)` 및 `@SpringBootTest`로 테스트 클래스에 주석을 추가합니다. `@RunWith` 주석은 JUnit에게 `SpringRunner` 클래스를 사용하여 테스트를 실행하도록 지시합니다. `@SpringBootTest` 주석은 Spring Boot가 애플리케이션 컨텍스트를 로드하도록 지시합니다.

`@Autowired` 주석은 `Calculator` 빈을 테스트 클래스에 주입합니다. `@Test` 주석은 JUnit에게 `testAdd()` 메서드가 테스트임을 알려줍니다.

`testAdd()` 메서드에서 `assertEquals()` 메서드를 사용하여 `add()` 메서드가 예상 값을 반환하는지 확인합니다.

`mvn test` 명령을 사용하여 테스트를 실행할 수 있습니다.

![테스트 실행](https://i.imgur.com/p7Aj0bU.png)

## 결론

이번 포스트에서는 JUnit과 Mockito로 Spring Boot 애플리케이션을 테스트하는 방법을 배웠습니다. 또한 단위 테스트 및 통합 테스트를 작성하는 방법도 살펴보았습니다.