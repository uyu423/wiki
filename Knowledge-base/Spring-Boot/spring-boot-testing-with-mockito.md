---
title: Mockito를 사용한 스프링 부트 테스트
description: 
published: true
date: 2023-02-02T00:23:22.553Z
tags: 
editor: markdown
dateCreated: 2023-02-02T00:23:20.928Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Testing with Mockito***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-testing-with-mockito)
{.links-list}


# Mockito를 사용한 스프링 부트 테스트

Spring Boot는 애플리케이션에 대한 테스트를 작성하는 훌륭한 방법을 제공합니다. 이 기사에서는 Mockito를 사용하여 Spring Boot 애플리케이션을 테스트하는 방법을 살펴보겠습니다.

Mockito는 Java를 위한 강력한 조롱 프레임워크입니다. Spring 커뮤니티에서 매우 인기가 있습니다. Mockito를 사용하면 외부 세계와 격리된 테스트를 작성할 수 있습니다. 이는 외부 서비스에 의존하지 않고 비즈니스 로직을 테스트하려는 경우 매우 중요합니다.

## Mockito 설정

먼저 `pom.xml`에 Mockito 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>2.0.0-beta.19</version>
    <scope>test</scope>
</dependency>
```

이제 'MockitoJUnitRunner'를 생성하여 테스트를 실행할 수 있습니다.

```java
import org.junit.runner.RunWith;
import org.mockito.runners.MockitoJUnitRunner;

@RunWith(MockitoJUnitRunner.class)
public class MyTest {
}
```

## Mockito를 스프링 부트와 함께 사용

Mockito는 Spring Boot와 함께 사용하기 매우 쉽습니다. 테스트 클래스에 `@MockBean`으로 간단하게 주석을 달아 Spring Bean의 모의를 생성할 수 있습니다.

```java
@RunWith(MockitoJUnitRunner.class)
public class MyTest {

    @MockBean
    private MyService myService;
}
```

그런 다음 Mockito를 사용하여 `MyService`의 메소드를 스텁할 수 있습니다.

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

## 결론

이 기사에서는 Mockito를 사용하여 Spring Boot 애플리케이션을 테스트하는 방법을 살펴보았습니다. Mockito는 더 나은 테스트를 작성하는 데 도움이 되는 매우 강력한 도구입니다.