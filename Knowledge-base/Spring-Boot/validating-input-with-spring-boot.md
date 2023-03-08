---
title: Spring Boot로 입력 유효성 검사
description: 
published: true
date: 2023-02-07T04:32:29.125Z
tags: 
editor: markdown
dateCreated: 2023-02-07T04:32:27.465Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Validating Input with Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/validating-input-with-spring-boot)
{.links-list}


# Spring Boot로 입력 유효성 검사

입력 유효성 검사는 모든 애플리케이션의 중요한 부분입니다. 그렇게 하지 않으면 모든 종류의 보안 및 안정성 문제가 발생할 수 있습니다.

Spring Boot는 입력을 검증하는 다양한 방법을 제공합니다. 이 기사에서는 가장 널리 사용되는 몇 가지 방법을 살펴보겠습니다.

## JSR-303

Java 사양 요청 303 또는 JSR-303은 Java의 유효성 검사 사양입니다. Spring Boot 애플리케이션의 입력 유효성 검사에 널리 사용되는 선택입니다.

JSR-303을 사용하려면 먼저 `pom.xml`에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

그런 다음 요청 매핑에 `@Valid` 주석이 있는 `@Controller`를 만들 수 있습니다.

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

`@Valid` 주석은 입력 유효성 검사를 트리거합니다. 또한 `@Validated` 주석을 사용하여 특정 필드에 대한 유효성 검사를 트리거할 수 있습니다.

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Validated({FirstGroup.class, SecondGroup.class}) @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

메서드 인수의 유효성을 검사할 수도 있습니다.

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @RequestParam("id") Long id) {
        // ...
    }

}
```

JSR-303은 많은 강력한 기능을 제공하지만 매우 장황할 수 있습니다.

## 최대 절전 유효성 검사기

Hibernate Validator는 JSR-303 호환 검증 프레임워크입니다. Spring Boot 애플리케이션의 입력 유효성 검사에 널리 사용되는 선택입니다.

Hibernate Validator를 사용하려면 먼저 `pom.xml`에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-validator</artifactId>
</dependency>
```

그런 다음 요청 매핑에 `@Valid` 주석이 있는 `@Controller`를 만들 수 있습니다.

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

`@Valid` 주석은 입력 유효성 검사를 트리거합니다. 또한 `@Validated` 주석을 사용하여 특정 필드에 대한 유효성 검사를 트리거할 수 있습니다.

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Validated({FirstGroup.class, SecondGroup.class}) @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

메서드 인수의 유효성을 검사할 수도 있습니다.

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @RequestParam("id") Long id) {
        // ...
    }

}
```

Hibernate Validator는 다수의 강력한 기능을 제공하지만 매우 장황할 수 있습니다.

## 스프링 유효성 검사

Spring Validation은 JSR-303 및 Hibernate Validator 위에 구축된 유효성 검사 프레임워크입니다. Spring Boot 애플리케이션의 입력 유효성 검사에 널리 사용되는 선택입니다.

Spring Validation을 사용하려면 먼저 `pom.xml`에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

그런 다음 요청 매핑에 `@Valid` 주석이 있는 `@Controller`를 만들 수 있습니다.

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

`@Valid` 주석은 입력 유효성 검사를 트리거합니다. 또한 `@Validated` 주석을 사용하여 특정 필드에 대한 유효성 검사를 트리거할 수 있습니다.

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Validated({FirstGroup.class, SecondGroup.class}) @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

메서드 인수의 유효성을 검사할 수도 있습니다.

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @RequestParam("id") Long id) {
        // ...
    }

}
```

Spring Validation은 많은 강력한 기능을 제공하지만 매우 장황할 수 있습니다.

## 결론

Spring Boot 애플리케이션에서 입력의 유효성을 검사하는 방법에는 여러 가지가 있습니다. 이 기사에서는 가장 널리 사용되는 몇 가지 방법을 살펴보았습니다.