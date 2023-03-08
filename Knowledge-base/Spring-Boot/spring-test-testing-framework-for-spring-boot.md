---
title: Spring 테스트: Spring Boot용 테스트 프레임워크
description: 
published: true
date: 2023-02-17T18:16:55.674Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:57:36.262Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Spring Test: Testing Framework for Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-test-testing-framework-for-spring-boot)
{.links-list}


# 스프링 테스트: 스프링 부트를 위한 테스트 프레임워크

이 기사에서는 Spring Boot용 Spring Test 테스트 프레임워크를 살펴보겠습니다. 프레임워크에 대한 간략한 개요부터 시작하여 사용 방법에 대한 자습서를 제공합니다. 그런 다음 프레임워크의 고급 기능에 대해 설명합니다.

## 개요

Spring Test는 Spring Boot용 테스트 프레임워크입니다. Spring Boot 애플리케이션에 대한 테스트를 작성하는 데 도움이 되도록 설계되었습니다. Spring Test는 Spring Boot 애플리케이션에 대한 테스트를 작성하는 편리한 방법을 제공합니다. 또한 응용 프로그램에 대한 테스트를 쉽게 작성할 수 있는 여러 기능을 제공합니다.

## 튜토리얼

이 튜토리얼에서는 Spring Test를 사용하여 Spring Boot 애플리케이션에 대한 테스트를 작성하는 방법을 보여줍니다. 숫자의 계승을 계산하는 간단한 응용 프로그램의 예를 사용할 것입니다.

먼저 프로젝트에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

다음으로 테스트 케이스를 작성해야 합니다. @Test 주석을 사용하여 테스트 사례를 표시합니다.

```java
@Test
public void testFactorial() {
    ...
}
```

테스트 사례에서는 애플리케이션에 필요한 종속성을 주입해야 합니다. @Autowired 주석을 사용하여 이를 수행할 수 있습니다.

```java
@Autowired
private FactorialService service;
```

이제 테스트 케이스를 작성할 수 있습니다. 테스트 사례에서는 FactorialService 클래스의 factorial() 메서드를 호출합니다. 우리는 결과가 정확하다고 주장할 것입니다.

```java
@Test
public void testFactorial() {
    int result = service.factorial(5);
    assertThat(result, is(120));
}
```

이제 다음 명령을 사용하여 테스트 사례를 실행할 수 있습니다.

```
$ mvn test
```

테스트 사례가 통과하면 다음과 같은 결과가 표시됩니다.

```
Results :

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

[INFO] 
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ spring-boot-test-example ---
[INFO] 
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running com.example.test.ExampleTest
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.002 sec
[INFO] 
[INFO] Results:
[INFO] 
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO] 
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 2.142 s
[INFO] Finished at: 2015-05-27T16:33:21+0530
[INFO] Final Memory: 10M/155M
[INFO] ------------------------------------------------------------------------
```

## 어설션

Spring Test는 테스트 사례에서 사용할 수 있는 여러 어설션 메서드를 제공합니다. 이러한 어설션 메서드는 org.springframework.test.util.AssertionErrors 클래스에서 정의됩니다.

다음은 가장 일반적으로 사용되는 어설션 방법 중 일부입니다.

* assertTrue(조건)
* assertFalse(조건)
* assertEquals(예상, 실제)
* assertNotEquals(예상, 실제)
* assertNull(객체)
* assertNotNull(객체)

AssertionErrors 클래스에 대한 JavaDoc에서 어설션 메서드의 전체 목록을 찾을 수 있습니다.

## 예외 처리

@Test(expected = Exception.class) 주석을 사용하여 테스트 사례에서 예상되는 예외를 처리할 수 있습니다.

예를 들어 입력이 음수일 때 factorial() 메서드가 IllegalArgumentException을 발생시킬 것으로 예상되는 경우 다음 테스트 사례를 작성할 수 있습니다.

```java
@Test(expected = IllegalArgumentException.class)
public void testFactorialNegative() {
    service.factorial(-1);
}
```

## 자바 8 람다 지원

Spring Test는 Java 8 람다 표현식을 지원합니다. 람다 식을 사용하여 간결하고 읽기 쉬운 테스트 사례를 작성할 수 있습니다.

예를 들어 다음 테스트 사례는 숫자 목록이 정렬되어 있는지 확인합니다.

```java
@Test
public void testSort() {
    List<Integer> numbers = Arrays.asList(5, 4, 3, 2, 1);
    Collections.sort(numbers);
    assertThat(numbers, is(Arrays.asList(1, 2, 3, 4, 5)));
}
```

## 가정

Assume 클래스를 사용하여 애플리케이션의 상태를 가정할 수 있습니다. 가정이 충족되지 않으면 테스트를 건너뛰는 데 가정이 사용됩니다.

예를 들어 다음 테스트 사례는 숫자가 양수인지 확인합니다. 숫자가 음수이면 테스트 케이스를 건너뜁니다.

```java
@Test
public void testPositive() {
    int number = -1;
    Assume.assumeTrue(number > 0);
    assertThat(number, is(greaterThan(0)));
}
```

## 테스트 컨텍스트

TestContext 프레임워크는 테스트 사례에서 사용할 수 있는 여러 기능을 제공합니다. 이러한 기능에는 다음이 포함됩니다.

* 테스트 실행 리스너
* 테스트 지원
* 테스트 이벤트 게시
* 테스트 인스턴스 사후 처리
* 테스트 클래스에 대한 종속성 주입

이러한 기능을 사용하여 애플리케이션에 대한 정교한 테스트 사례를 작성할 수 있습니다.

##결론

이 기사에서는 Spring Boot용 Spring Test 테스트 프레임워크를 살펴보았습니다. 프레임워크를 사용하여 애플리케이션에 대한 테스트를 작성하는 방법을 살펴보았습니다. 우리는 또한 프레임워크의 고급 기능 중 일부를 보았습니다.