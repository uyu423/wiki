---
title: Mockito: Spring Boot에서 단위 테스트를 위한 Mocking
description: 
published: true
date: 2023-02-01T17:48:04.870Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:48:00.847Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Mockito: Mocking for Unit Testing in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/mockito-mocking-for-unit-testing-in-spring-boot)
{.links-list}


# Mockito: Spring Boot에서 단위 테스트를 위한 Mocking

모킹은 개발자가 종속성이 아닌 특정 코드 단위의 기능을 테스트하는 데 집중할 수 있도록 하는 단위 테스트의 핵심 개념입니다. Spring Boot 애플리케이션의 컨텍스트에서 Mockito는 전체 Spring 컨텍스트를 시작할 필요 없이 특정 구성 요소의 기능을 테스트하기 위해 bean 및 서비스를 모의하는 데 사용할 수 있습니다.

이 기사에서는 Mockito를 사용하여 Spring Boot 애플리케이션에서 빈과 서비스를 모의하는 방법을 살펴보겠습니다. 또한 Spring 컨텍스트를 자동으로 시작하도록 Mockito를 구성하는 방법도 살펴보겠습니다.

## 모키토란?

Mockito는 Java용으로 널리 사용되는 모의 테스트 프레임워크입니다. Mockito를 사용하면 개발자가 단위 테스트에 사용할 모의 개체를 만들고 구성할 수 있습니다. Mockito는 인터페이스, 클래스, 심지어 최종 클래스와 메서드를 조롱하는 데 사용할 수 있습니다.

## 스프링 부트에서 빈과 서비스 모킹하기

Mockito를 사용하면 Spring Boot의 모킹 빈과 서비스가 쉽습니다. 다음 예제에서는 `myBean`이라는 빈을 조롱합니다.

```java
@MockBean
MyBean myBean;

@Test
public void testMyBean() {
    // configure mock object
    when(myBean.getName()).thenReturn("Mockito");
    
    // invoke method on mock object
    String name = myBean.getName();
    
    // verify results
    assertThat(name).isEqualTo("Mockito");
}
```

위의 예에서 `@MockBean` 주석을 사용하여 `MyBean` 클래스의 목 객체를 만듭니다. 그런 다음 `when` 및 `thenReturn` 메서드를 사용하여 모의 개체를 구성합니다. 마지막으로 모의 개체에서 `getName` 메서드를 호출하고 반환 값이 예상한 대로임을 확인합니다.

## Spring Boot에서 Mockito 설정하기

Mockito는 `mockito-core` 및 `mockito-spring` 종속성을 사용하여 Spring Boot에서 구성할 수 있습니다. `pom.xml` 파일에서 다음 종속성을 추가합니다.

```xml
<dependencies>
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-core</artifactId>
        <version>2.13.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-spring</artifactId>
        <version>1.9.5</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

`mockito-core` 종속성은 Mockito 라이브러리를 포함하고 `mockito-spring` 종속성은 Mockito와 Spring 간의 통합을 포함합니다.

## 결론

이 기사에서는 Mockito를 사용하여 Spring Boot 애플리케이션에서 빈과 서비스를 모의하는 방법을 살펴보았습니다. 또한 Spring 컨텍스트를 자동으로 시작하도록 Mockito를 구성하는 방법도 살펴보았습니다.