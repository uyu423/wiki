---
title: Bean 유효성 검사 API를 사용한 스프링 부트 유효성 검사
description: 
published: true
date: 2023-02-07T18:32:46.376Z
tags: 
editor: markdown
dateCreated: 2023-02-07T18:32:44.561Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Validation with Bean Validation API***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-validation-with-bean-validation-api)
{.links-list}


# Bean 유효성 검사 API를 사용한 스프링 부트 유효성 검사

사용자 입력 유효성 검사는 모든 응용 프로그램에서 중요한 부분입니다. 이 기사에서는 Bean Validation API를 사용하여 Spring Boot 애플리케이션에서 사용자 입력의 유효성을 검사하는 방법을 살펴보겠습니다.

## 빈 검증이란?

Bean 유효성 검사는 Java Bean 속성의 제약 조건을 유효성 검사하기 위한 Java 사양입니다. Java Enterprise Edition(Java EE)의 일부이며 Java SE 애플리케이션에서 사용하기 위한 독립 실행형 라이브러리로 사용할 수 있습니다.

## Bean Validation API란?

Bean 유효성 검증 API는 Bean 유효성 검증 제공자를 구현하기 위한 계약을 정의하는 인터페이스 및 클래스 세트입니다. Bean 유효성 검사 공급자는 유효성 검사 서비스를 제공하기 위해 Java EE 또는 Java SE 애플리케이션에 연결할 수 있는 이러한 계약의 구현입니다.

## Bean 유효성 검사는 어떻게 작동합니까?

Bean 유효성 검사는 Java Bean 속성에 주석을 추가하는 데 사용할 수 있는 주석 집합을 정의합니다. 이러한 주석을 사용하여 속성에 적용해야 하는 제약 조건을 지정할 수 있습니다.

속성에 제약 조건 주석이 추가되면 Bean 유효성 검사 공급자는 제약 조건에 대해 속성의 유효성을 검사합니다. 속성이 유효한 경우 공급자는 아무 작업도 수행하지 않습니다. 속성이 유효하지 않은 경우 공급자는 ConstraintViolationException을 throw합니다.

## Spring Boot에서 Bean 유효성 검사 설정

Spring Boot 애플리케이션에서 Bean Validation을 사용하려면 프로젝트에 Hibernate Validator 의존성을 추가해야 합니다. Hibernate Validator는 Bean Validation API의 참조 구현입니다.

```xml
<dependency>
    <groupId>org.hibernate.validator</groupId>
    <artifactId>hibernate-validator</artifactId>
    <version>6.0.17.Final</version>
</dependency>
```

종속성을 추가한 후에는 응용 프로그램에서 Bean 유효성 검사를 사용할 수 있습니다.

## 사용자 입력 확인

다음 필드가 있는 사용자 등록 양식이 있다고 가정해 보겠습니다.

-   사용자 이름
-   비밀번호
-   비밀번호 확인
- 이메일

다음 주석을 사용하여 양식의 유효성을 검사할 수 있습니다.

- @NotNull – 필드는 null일 수 없습니다.
- @NotEmpty – 필드는 비워둘 수 없습니다.
- @Size – 필드는 지정된 크기 사이여야 합니다.
- @Email – 필드는 유효한 이메일 주소여야 합니다.

다음 주석으로 양식 필드에 주석을 달 수 있습니다.

```java
public class RegistrationForm {

    @NotNull
    @Size(min = 3, max = 20)
    private String username;

    @NotNull
    @Size(min = 6, max = 40)
    private String password;

    @NotNull
    @Size(min = 6, max = 40)
    private String confirmPassword;

    @NotNull
    @Email
    private String email;
    
    //Getters and setters
}
```

이제 양식 제출을 처리하는 메서드가 있는 컨트롤러가 있다고 가정해 보겠습니다.

```java
@PostMapping("/register")
public String register(@Valid RegistrationForm form, BindingResult bindingResult) {
    //Validate form
    if (bindingResult.hasErrors()) {
        return "register";
    }
    
    //Register user
    return "redirect:/login";
}
```

@Valid 어노테이션은 Spring에게 양식의 유효성을 검증하도록 지시합니다. BindingResult에는 유효성 검사 결과가 포함됩니다. 양식이 유효하지 않은 경우 hasErrors() 메서드는 true를 반환하고 오류 메시지와 함께 양식을 사용자에게 반환할 수 있습니다.

## 사용자 정의 제약

기본 제공 제약 조건 외에도 고유한 사용자 지정 제약 조건을 정의할 수 있습니다. 이렇게 하려면 주석과 유효성 검사기 클래스를 만들어야 합니다.

비밀번호와 비밀번호 확인 필드가 일치하는지 확인하기 위해 사용자 지정 제약 조건을 만들고 싶다고 가정해 보겠습니다. 다음과 같이 사용자 지정 주석을 만들 수 있습니다.

```java
@Documented
@Constraint(validatedBy = PasswordMatchesValidator.class)
@Target({ TYPE, FIELD, ANNOTATION_TYPE })
@Retention(RUNTIME)
public @interface PasswordMatches {
    String message() default "Passwords do not match";
    Class<?>[] groups() default {};
    Class<? extends Payload>[] payload() default {};
}
```

그리고 다음과 같은 유효성 검사기 클래스:

```java
public class PasswordMatchesValidator implements ConstraintValidator<PasswordMatches, Object> {

    @Override
    public void initialize(PasswordMatches constraintAnnotation) {       
    }

    @Override
    public boolean isValid(Object obj, ConstraintValidatorContext context){   
        User user = (User) obj;
        return user.getPassword().equals(user.getConfirmPassword());
    }     
}
```

그런 다음 @PasswordMatches 주석을 사용하여 암호 확인 필드에 주석을 달 수 있습니다.

```java
public class RegistrationForm {

    //...    

    @NotNull
    @Size(min = 6, max = 40)
    @PasswordMatches
    private String confirmPassword;

    //...
}
```

## 결론

이 기사에서는 Bean Validation API를 사용하여 Spring Boot 애플리케이션에서 사용자 입력의 유효성을 검사하는 방법을 살펴보았습니다. 또한 사용자 지정 제약 조건을 만드는 방법도 살펴보았습니다.