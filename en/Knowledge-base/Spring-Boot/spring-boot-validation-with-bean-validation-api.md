---
title: Spring Boot Validation with Bean Validation API
description: 
published: true
date: 2023-02-07T18:32:50.497Z
tags: 
editor: markdown
dateCreated: 2023-02-07T18:32:44.570Z
---

- [Validación Spring Boot con API de validación de Bean***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-validation-with-bean-validation-api)
{.links-list}
- [使用 Bean 验证 API 进行 Spring Boot 验证***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-validation-with-bean-validation-api)
{.links-list}
- [Bean 유효성 검사 API를 사용한 스프링 부트 유효성 검사***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-validation-with-bean-validation-api)
{.links-list}


# Spring Boot Validation with Bean Validation API

Validating user input is an important part of any application. In this article, we'll take a look at how to use the Bean Validation API to validate user input in a Spring Boot application.

## What is Bean Validation?

Bean Validation is a Java specification for validating the constraints of Java Bean properties. It is part of the Java Enterprise Edition (Java EE) and is available as a standalone library for use in Java SE applications.

## What is the Bean Validation API?

The Bean Validation API is a set of interfaces and classes that define the contracts for implementing a Bean Validation provider. A Bean Validation provider is an implementation of these contracts that can be plugged into a Java EE or Java SE application to provide validation services.

## How Does Bean Validation Work?

Bean Validation defines a set of annotations that can be used to annotate Java Bean properties. These annotations can be used to specify the constraints that should be applied to the property.

When a property is annotated with a constraint annotation, the Bean Validation provider will validate the property against the constraint. If the property is valid, the provider will do nothing. If the property is invalid, the provider will throw a ConstraintViolationException.

## Setting Up Bean Validation in Spring Boot

To use Bean Validation in a Spring Boot application, we need to add the Hibernate Validator dependency to our project. Hibernate Validator is the reference implementation of the Bean Validation API.

```xml
<dependency>
    <groupId>org.hibernate.validator</groupId>
    <artifactId>hibernate-validator</artifactId>
    <version>6.0.17.Final</version>
</dependency>
```

Once we have added the dependency, we can start using Bean Validation in our application.

## Validating User Input

Let's say we have a user registration form with the following fields:

-   Username
-   Password
-   Confirm Password
-   Email

We can validate the form using the following annotations:

-   @NotNull – The field cannot be null.
-   @NotEmpty – The field cannot be empty.
-   @Size – The field must be between the specified size.
-   @Email – The field must be a valid email address.

We can annotate the form fields with these annotations:

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

Now, let's say we have a controller with a method that handles the form submission:

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

The @Valid annotation tells Spring to validate the form. The BindingResult contains the result of the validation. If the form is invalid, the hasErrors() method will return true and we can return the form to the user with the error messages.

## Custom Constraints

In addition to the built-in constraints, we can define our own custom constraints. To do this, we need to create a annotation and a validator class.

Let's say we want to create a custom constraint to check if the password and confirm password fields match. We can create a custom annotation like this:

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

And a validator class like this:

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

We can then annotate the confirm password field with the @PasswordMatches annotation:

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

## Conclusion

In this article, we've seen how to use the Bean Validation API to validate user input in a Spring Boot application. We've also seen how to create custom constraints.