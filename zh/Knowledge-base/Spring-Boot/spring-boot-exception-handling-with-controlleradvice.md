---
title: 使用 ControllerAdvice 进行 Spring Boot 异常处理
description: 
published: true
date: 2023-02-07T17:32:29.151Z
tags: 
editor: markdown
dateCreated: 2023-02-07T17:32:27.532Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot Exception Handling with ControllerAdvice***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-exception-handling-with-controlleradvice)
{.links-list}



# 介绍

开发人员在构建应用程序时面临许多不同类型的错误。这些错误可能是由用户输入、代码问题或服务器或数据库问题引起的。

在本文中，我们将了解如何在 Spring Boot 中处理错误。我们将从简要概述可能发生的不同类型的错误开始，然后我们将讨论如何使用 @ControllerAdvice 注释处理它们。

# 错误类型

构建 Spring Boot 应用程序时可能会发生三种主要类型的错误：

* **验证错误：**当用户输入与预期格式不匹配时会发生这些错误。例如，如果用户尝试使用无效的电子邮件地址提交表单，则会发生验证错误。

* **绑定错误：** 当数据绑定过程失败时会发生这些错误。如果用户输入的格式错误，或者输入与目标对象之间的类型不匹配，就会发生这种情况。

* **其他错误：** 这些包括所有其他类型的错误，例如数据库错误、服务器错误等。

# 处理错误

在 Spring Boot 中，可以使用 @ControllerAdvice 注解处理错误。此注释可用于为所有控制器定义全局错误处理程序。

@ControllerAdvice 注释可用于处理验证和绑定错误。要处理其他类型的错误，您可以使用@ExceptionHandler 注释。

# 验证错误

可以使用 @ControllerAdvice 注释处理验证错误。在下面的示例中，我们使用 @ControllerAdvice 注释来处理验证错误：

```java
@ControllerAdvice
public class ValidationErrorHandler {

    @InitBinder
    public void initBinder(WebDataBinder binder) {
        binder.addValidators(new UserValidator());
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<?> handleValidationErrors(MethodArgumentNotValidException ex) {
        // ...
    }

}
```

在上面的示例中，我们使用 @InitBinder 注释为 User 类注册验证器。我们还使用 @ExceptionHandler 注释来处理验证错误。

# 绑定错误

可以使用 @ControllerAdvice 注释处理绑定错误。在下面的示例中，我们使用 @ControllerAdvice 注释来处理绑定错误：

```java
@ControllerAdvice
public class BindingErrorHandler {

    @ExceptionHandler(BindException.class)
    public ResponseEntity<?> handleBindingErrors(BindException ex) {
        // ...
    }

}
```

在上面的示例中，我们使用 @ExceptionHandler 注释来处理绑定错误。

# 其他错误

可以使用 @ExceptionHandler 注释处理其他类型的错误。在下面的示例中，我们使用 @ExceptionHandler 注释来处理数据库错误：

```java
@ControllerAdvice
public class DatabaseErrorHandler {

    @ExceptionHandler(DataAccessException.class)
    public ResponseEntity<?> handleDatabaseErrors(DataAccessException ex) {
        // ...
    }

}
```

在上面的示例中，我们使用 @ExceptionHandler 注释来处理数据库错误。

# 结论

在本文中，我们了解了如何处理 Spring Boot 中的错误。我们首先简要概述了可能发生的不同类型的错误，然后讨论了如何使用 @ControllerAdvice 注释处理它们。