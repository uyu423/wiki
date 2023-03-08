---
title: Spring Boot 中的验证：最佳实践
description: 
published: true
date: 2023-02-01T17:11:36.388Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:11:34.766Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Validation in Spring Boot: Best Practices***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/validation-in-spring-boot-best-practices)
{.links-list}


# Spring Boot 中的验证：最佳实践

验证用户输入是任何应用程序的关键部分。它有助于确保数据完整性并防止安全漏洞。

在 Spring Boot 中，有几种方法可以执行验证。本文将探索 Spring Boot 中验证的最佳实践，包括使用内置验证框架和自定义验证。

##内置验证

Spring Boot 提供了一个内置的验证框架，可用于验证用户输入。此框架基于 JavaBeans 验证 (Bean Validation) 规范。

要使用内置的验证框架，您需要在项目中添加以下依赖项：

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

然后，您可以在控制器方法上使用 @Valid 注释来触发验证。例如：

```java
@PostMapping
public void create(@Valid @RequestBody User user) {
    // ...
}
```

如果用户输入无效，将抛出 MethodArgumentNotValidException。此异常包含可用于向用户显示反馈的错误列表。

也可以使用 @Valid 注释来验证您的域对象。例如：

```java
@Valid
@Entity
public class User {

    // ...
}
```

##自定义验证

在某些情况下，内置的验证框架可能还不够。例如，您可能需要验证用户名是否唯一。在这种情况下，您可以创建自定义验证器。

要创建自定义验证器，您需要创建一个实现 ConstraintValidator 接口的类。该接口定义了两个方法：

- isValid()：此方法包含验证约束的逻辑。
- initialize()：创建验证器时调用此方法。它可用于初始化验证器。

例如，这是一个自定义验证器，用于验证用户名是否唯一：

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

可以通过使用 @UniqueUsername 注释对字段进行注释来使用此验证器：

```java
public class User {

    @UniqueUsername
    private String username;

    // ...
}
```

如果需要验证多个字段，可以创建一个多字段验证器。为此，您需要创建一个实现 ConstraintValidator 接口的类，并使用 @Constraint(validatedBy = { /* class1, class2, ... */ }) 注释对其进行注释。

例如，这是一个用于验证密码是否足够强的多字段验证器：

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

可以通过使用 @ValidPassword 注释对字段进行注释来使用此验证器：

```java
public class User {

    @ValidPassword
    private String password;

    // ...
}
```

＃＃结论

验证是任何应用程序的关键部分。在 Spring Boot 中，有多种方法可以执行验证，包括使用内置验证框架和自定义验证。

＃＃参考

- [Spring Boot 验证](https://spring.io/blog/2013/11/01/validation-in-spring-boot)
- [在 Spring Boot 中验证表单输入](https://www.baeldung.com/spring-boot-validation)
- [在 Spring Boot 中创建自定义验证器](https://www.baeldung.com/spring-boot-custom-validators)