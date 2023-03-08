---
title: 使用 Bean 验证 API 进行 Spring Boot 验证
description: 
published: true
date: 2023-02-07T18:32:46.220Z
tags: 
editor: markdown
dateCreated: 2023-02-07T18:32:44.561Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot Validation with Bean Validation API***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-validation-with-bean-validation-api)
{.links-list}


# 使用 Bean 验证 API 进行 Spring Boot 验证

验证用户输入是任何应用程序的重要组成部分。在本文中，我们将了解如何使用 Bean Validation API 来验证 Spring Boot 应用程序中的用户输入。

## 什么是 Bean 验证？

Bean Validation 是一种 Java 规范，用于验证 Java Bean 属性的约束。它是 Java Enterprise Edition (Java EE) 的一部分，可作为独立库在 Java SE 应用程序中使用。

## 什么是 Bean 验证 API？

Bean Validation API 是一组接口和类，它们定义了用于实现 Bean Validation 提供程序的契约。 Bean Validation provider 是这些契约的实现，可以插入 Java EE 或 Java SE 应用程序以提供验证服务。

## Bean 验证如何工作？

Bean Validation 定义了一组可用于注释 Java Bean 属性的注释。这些注释可用于指定应应用于属性的约束。

当使用约束注解对属性进行注解时，Bean 验证提供程序将根据约束验证该属性。如果该属性有效，则提供者将不执行任何操作。如果该属性无效，提供者将抛出 ConstraintViolationException。

## 在 Spring Boot 中设置 Bean 验证

要在 Spring Boot 应用程序中使用 Bean Validation，我们需要将 Hibernate Validator 依赖项添加到我们的项目中。 Hibernate Validator 是 Bean Validation API 的参考实现。

```xml
<dependency>
    <groupId>org.hibernate.validator</groupId>
    <artifactId>hibernate-validator</artifactId>
    <version>6.0.17.Final</version>
</dependency>
```

一旦我们添加了依赖项，我们就可以开始在我们的应用程序中使用 Bean Validation。

## 验证用户输入

假设我们有一个包含以下字段的用户注册表单：

-   用户名
-   密码
-   确认密码
-   电子邮件

我们可以使用以下注释来验证表单：

- @NotNull – 该字段不能为空。
- @NotEmpty – 该字段不能为空。
- @Size – 该字段必须在指定大小之间。
- @Email – 该字段必须是有效的电子邮件地址。

我们可以使用这些注释来注释表单字段：

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

现在，假设我们有一个控制器，它有一个处理表单提交的方法：

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

@Valid 注解告诉 Spring 验证表单。 BindingResult 包含验证结果。如果表单无效，hasErrors() 方法将返回 true，我们可以将表单连同错误消息一起返回给用户。

## 自定义约束

除了内置约束之外，我们还可以定义自己的自定义约束。为此，我们需要创建一个注解和一个验证器类。

假设我们要创建一个自定义约束来检查密码和确认密码字段是否匹配。我们可以像这样创建自定义注释：

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

和这样的验证器类：

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

然后我们可以使用 @PasswordMatches 注释来注释确认密码字段：

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

## 结论

在本文中，我们了解了如何使用 Bean Validation API 来验证 Spring Boot 应用程序中的用户输入。我们还看到了如何创建自定义约束。