---
title: Mockito: Mocking for Unit Testing in Spring Boot
description: 
published: true
date: 2023-02-01T17:48:02.485Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:48:00.844Z
---

- [Mockito: Spring Boot에서 단위 테스트를 위한 Mocking***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/mockito-mocking-for-unit-testing-in-spring-boot)
{.links-list}
- [Mockito：在 Spring Boot 中模拟单元测试***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/mockito-mocking-for-unit-testing-in-spring-boot)
{.links-list}
- [Mockito: Simulacro para pruebas unitarias en Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/mockito-mocking-for-unit-testing-in-spring-boot)
{.links-list}


# Mockito: Mocking for Unit Testing in Spring Boot

Mocking is a key concept in unit testing that allows developers to focus on testing the functionality of a specific unit of code, rather than its dependencies. In the context of Spring Boot applications, Mockito can be used to mock beans and services to test the functionality of a specific component without the need to launch the entire Spring context.

In this article, we'll take a look at how to use Mockito to mock beans and services in a Spring Boot application. We'll also look at how to configure Mockito to launch the Spring context automatically.

## What is Mockito?

Mockito is a popular mock testing framework for Java. Mockito allows developers to create and configure mock objects to be used in unit tests. Mockito can be used to mock interfaces, classes, and even final classes and methods.

## Mocking Beans and Services in Spring Boot

Mocking beans and services in Spring Boot is easy with Mockito. In the following example, we'll mock a bean named `myBean`:

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

In the example above, we use the `@MockBean` annotation to create a mock object of the `MyBean` class. We then use the `when` and `thenReturn` methods to configure the mock object. Finally, we invoke the `getName` method on the mock object and assert that the return value is as expected.

## Configuring Mockito in Spring Boot

Mockito can be configured in Spring Boot using the `mockito-core` and `mockito-spring` dependencies. In the `pom.xml` file, add the following dependencies:

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

The `mockito-core` dependency contains the Mockito library, while the `mockito-spring` dependency contains the integration between Mockito and Spring.

## Conclusion

In this article, we've looked at how to use Mockito to mock beans and services in a Spring Boot application. We've also seen how to configure Mockito to launch the Spring context automatically.