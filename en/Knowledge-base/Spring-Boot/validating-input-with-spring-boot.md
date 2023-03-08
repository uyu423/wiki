---
title: Validating Input with Spring Boot
description: 
published: true
date: 2023-02-07T04:32:33.270Z
tags: 
editor: markdown
dateCreated: 2023-02-07T04:32:27.469Z
---

- [Validación de entrada con Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/validating-input-with-spring-boot)
{.links-list}
- [使用 Spring Boot 验证输入***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/validating-input-with-spring-boot)
{.links-list}
- [Spring Boot로 입력 유효성 검사***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/validating-input-with-spring-boot)
{.links-list}


# Validating Input with Spring Boot

Validating input is a critical part of any application. Failing to do so can lead to all sorts of security and stability issues.

Spring Boot provides a number of ways to validate input. In this article, we'll take a look at some of the most popular methods.

## JSR-303

The Java Specification Request 303, or JSR-303, is a specification for validation in Java. It's a popular choice for input validation in Spring Boot applications.

To use JSR-303, we first need to add the following dependency to our `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

We can then create a `@Controller` with a `@Valid` annotation on our request mapping:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

The `@Valid` annotation will trigger input validation. We can also use the `@Validated` annotation to trigger validation on specific fields:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Validated({FirstGroup.class, SecondGroup.class}) @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

We can also validate method arguments:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @RequestParam("id") Long id) {
        // ...
    }

}
```

JSR-303 offers a number of powerful features, but it can be quite verbose.

## Hibernate Validator

Hibernate Validator is a JSR-303 compliant validation framework. It's a popular choice for input validation in Spring Boot applications.

To use Hibernate Validator, we first need to add the following dependency to our `pom.xml`:

```xml
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-validator</artifactId>
</dependency>
```

We can then create a `@Controller` with a `@Valid` annotation on our request mapping:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

The `@Valid` annotation will trigger input validation. We can also use the `@Validated` annotation to trigger validation on specific fields:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Validated({FirstGroup.class, SecondGroup.class}) @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

We can also validate method arguments:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @RequestParam("id") Long id) {
        // ...
    }

}
```

Hibernate Validator offers a number of powerful features, but it can be quite verbose.

## Spring Validation

Spring Validation is a validation framework that's built on top of JSR-303 and Hibernate Validator. It's a popular choice for input validation in Spring Boot applications.

To use Spring Validation, we first need to add the following dependency to our `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

We can then create a `@Controller` with a `@Valid` annotation on our request mapping:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

The `@Valid` annotation will trigger input validation. We can also use the `@Validated` annotation to trigger validation on specific fields:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Validated({FirstGroup.class, SecondGroup.class}) @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

We can also validate method arguments:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @RequestParam("id") Long id) {
        // ...
    }

}
```

Spring Validation offers a number of powerful features, but it can be quite verbose.

## Conclusion

There are a number of ways to validate input in Spring Boot applications. In this article, we've looked at some of the most popular methods.