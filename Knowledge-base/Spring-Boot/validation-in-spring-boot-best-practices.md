---
title: Spring Boot의 유효성 검사: 모범 사례
description: 
published: true
date: 2023-02-01T17:11:36.425Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:11:34.768Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Validation in Spring Boot: Best Practices***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/validation-in-spring-boot-best-practices)
{.links-list}


# Spring Boot의 유효성 검사: 모범 사례

사용자 입력 유효성 검사는 모든 응용 프로그램의 중요한 부분입니다. 데이터 무결성을 보장하고 보안 취약성을 방지하는 데 도움이 됩니다.

Spring Boot에는 유효성 검사를 수행하는 여러 가지 방법이 있습니다. 이 문서에서는 기본 제공 유효성 검사 프레임워크 및 사용자 지정 유효성 검사 사용을 포함하여 Spring Boot의 유효성 검사에 대한 모범 사례를 살펴봅니다.

##내장 유효성 검사

Spring Boot는 사용자 입력의 유효성을 검사하는 데 사용할 수 있는 기본 제공 유효성 검사 프레임워크를 제공합니다. 이 프레임워크는 JavaBeans 유효성 검사(Bean 유효성 검사) 사양을 기반으로 합니다.

기본 제공 유효성 검사 프레임워크를 사용하려면 프로젝트에 다음 종속성을 추가해야 합니다.

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

그런 다음 컨트롤러 메서드에서 @Valid 주석을 사용하여 유효성 검사를 트리거할 수 있습니다. 예를 들어:

```java
@PostMapping
public void create(@Valid @RequestBody User user) {
    // ...
}
```

사용자 입력이 유효하지 않으면 MethodArgumentNotValidException이 발생합니다. 이 예외에는 사용자에게 피드백을 표시하는 데 사용할 수 있는 오류 목록이 포함되어 있습니다.

@Valid 주석을 사용하여 도메인 개체의 유효성을 검사하는 것도 가능합니다. 예를 들어:

```java
@Valid
@Entity
public class User {

    // ...
}
```

##맞춤형 유효성 검사

경우에 따라 기본 제공 유효성 검사 프레임워크가 충분하지 않을 수 있습니다. 예를 들어 사용자 이름이 고유한지 확인해야 할 수 있습니다. 이 경우 사용자 지정 유효성 검사기를 만들 수 있습니다.

사용자 지정 유효성 검사기를 만들려면 ConstraintValidator 인터페이스를 구현하는 클래스를 만들어야 합니다. 이 인터페이스는 두 가지 방법을 정의합니다.

- isValid(): 이 메소드는 제약조건을 검증하기 위한 로직을 포함합니다.
- initialize(): Validator 생성 시 호출되는 메서드입니다. 유효성 검사기를 초기화하는 데 사용할 수 있습니다.

예를 들어 다음은 사용자 이름이 고유한지 확인하기 위한 사용자 지정 유효성 검사기입니다.

```java
public class UniqueUsernameValidator implements ConstraintValidator<UniqueUsername, String> {

    @Autowired
    private UserRepository userRepository;

    @Override
    public void initialize(UniqueUsername constraintAnnotation) {
        // ...
    }

    @Override
    public boolean isValid(String username, ConstraintValidatorContext context) {
        return !userRepository.existsByUsername(username);
    }
}
```

이 유효성 검사기는 @UniqueUsername 주석으로 필드에 주석을 달아 사용할 수 있습니다.

```java
public class User {

    @UniqueUsername
    private String username;

    // ...
}
```

여러 필드의 유효성을 검사해야 하는 경우 다중 필드 유효성 검사기를 만들 수 있습니다. 이렇게 하려면 ConstraintValidator 인터페이스를 구현하는 클래스를 만들고 @Constraint(validatedBy = { /* class1, class2, ... */ }) 주석으로 주석을 추가해야 합니다.

예를 들어 다음은 암호가 충분히 강력한지 확인하기 위한 다중 필드 유효성 검사기입니다.

```java
@Constraint(validatedBy = PasswordValidator.class)
@Target({ ElementType.TYPE, ElementType.FIELD, ElementType.ANNOTATION_TYPE })
@Retention(RetentionPolicy.RUNTIME)
public @interface ValidPassword {

    String message() default "Invalid Password";

    Class<?>[] groups() default {};

    Class<? extends Payload>[] payload() default {};

}
```

```java
public class PasswordValidator implements ConstraintValidator<ValidPassword, String> {

    @Override
    public void initialize(ValidPassword constraintAnnotation) {
        // ...
    }

    @Override
    public boolean isValid(String password, ConstraintValidatorContext context) {
        // ...
    }

}
```

이 유효성 검사기는 @ValidPassword 주석으로 필드에 주석을 달아 사용할 수 있습니다.

```java
public class User {

    @ValidPassword
    private String password;

    // ...
}
```

##결론

유효성 검사는 모든 응용 프로그램의 중요한 부분입니다. Spring Boot에는 기본 제공 유효성 검사 프레임워크 및 사용자 지정 유효성 검사를 포함하여 유효성 검사를 수행하는 여러 가지 방법이 있습니다.

##참조

- [스프링 부트 유효성 검사](https://spring.io/blog/2013/11/01/validation-in-spring-boot)
- [스프링부트에서 폼 입력 확인하기](https://www.baeldung.com/spring-boot-validation)
- [Spring Boot에서 Custom Validators 생성하기](https://www.baeldung.com/spring-boot-custom-validators)