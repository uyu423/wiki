---
title: Spring Boot Testing with Mockito
description: 
published: true
date: 2023-02-02T00:23:25.066Z
tags: 
editor: markdown
dateCreated: 2023-02-02T00:23:20.931Z
---

- [Prueba de arranque de primavera con Mockito***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-testing-with-mockito)
{.links-list}
- [使用 Mockito 进行 Spring Boot 测试***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-testing-with-mockito)
{.links-list}
- [Mockito를 사용한 스프링 부트 테스트***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-testing-with-mockito)
{.links-list}


# Spring Boot Testing with Mockito

Spring Boot provides a great way to write tests for your application. In this article, we'll take a look at how to use Mockito to test your Spring Boot application.

Mockito is a powerful mocking framework for Java. It is very popular in the Spring community. Mockito allows us to write tests that are isolated from the external world. This is very important when we want to test our business logic without relying on external services.

## Set up Mockito

First, we need to add the Mockito dependency to our `pom.xml`:

```xml
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>2.0.0-beta.19</version>
    <scope>test</scope>
</dependency>
```

We can now create a `MockitoJUnitRunner` to run our tests:

```java
import org.junit.runner.RunWith;
import org.mockito.runners.MockitoJUnitRunner;

@RunWith(MockitoJUnitRunner.class)
public class MyTest {
}
```

## Use Mockito with Spring Boot

Mockito is very easy to use with Spring Boot. We can simply annotate our test class with `@MockBean` to create a mock of a Spring Bean:

```java
@RunWith(MockitoJUnitRunner.class)
public class MyTest {

    @MockBean
    private MyService myService;
}
```

We can then use Mockito to stub the methods of `MyService`:

```java
@RunWith(MockitoJUnitRunner.class)
public class MyTest {

    @MockBean
    private MyService myService;

    @Test
    public void testMyService() {
        // given
        given(myService.doSomething()).willReturn("Hello world!");

        // when
        String result = myService.doSomething();

        // then
        assertThat(result).isEqualTo("Hello world!");
    }
}
```

## Conclusion

In this article, we've seen how to use Mockito to test a Spring Boot application. Mockito is a very powerful tool that can help us write better tests.