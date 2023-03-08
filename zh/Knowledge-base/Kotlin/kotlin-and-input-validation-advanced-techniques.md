---
title: Kotlin 和输入验证：高级技术
description: 
published: true
date: 2023-02-17T18:03:06.935Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:29:33.407Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Kotlin and Input Validation: Advanced Techniques***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-input-validation-advanced-techniques)
{.links-list}
 

# Kotlin 和输入验证：高级技术

验证用户输入是任何应用程序的关键部分，无论是桌面应用程序、Web 应用程序还是移动应用程序。在本文中，我们将了解一些在 Kotlin 中验证输入的高级技术。

我们将从回顾输入验证的基础知识开始。然后我们将研究一些更高级的技术，包括使用正则表达式和自定义验证器。最后，我们将总结一些编写更可维护和可重用代码的技巧。

## 回顾：输入验证的基础知识

输入验证是确保用户提供的数据满足应用程序要求的过程。这些要求可以是从数据类型（例如仅整数）到格式（例如电子邮件地址必须有一个“@”符号）到长度（例如密码必须至少为 8 个字符）的任何内容。

输入验证很重要，主要有两个原因：

- **安全性：**无效数据可用于利用应用程序中的漏洞。例如，如果您不验证电子邮件地址，恶意用户可能会输入类似 `">@example.com<script>alert('xss')</script>"` 的电子邮件地址，这将导致 XSS攻击。

- **数据质量：**无效数据可能会导致您的应用程序出现故障。例如，如果您不验证字段是否为整数，则在尝试对数据执行数学运算时可能会得到意想不到的结果。

在 Kotlin 中，有很多方法可以验证输入。最基本的方法是使用 is 运算符来检查变量的数据类型：

```kotlin
fun validateInput(input: Any) {
    if (input is String) {
        // The input is a string, so we can validate its length, format, etc.
    } else if (input is Int) {
        // The input is an integer, so we can validate that it's in the correct range, etc.
    } else {
        // The input is not a string or an integer, so we can't validate it.
    }
}
```

`is` 运算符可用于任何数据类型，包括自定义数据类型。例如，如果您有一个“User”数据类，您可以使用“is”运算符来检查输入是否为“User”：

```kotlin
fun validateInput(input: Any) {
    if (input is User) {
        // The input is a User, so we can validate its properties, etc.
    } else {
        // The input is not a User, so we can't validate it.
    }
}
```

除了 is 运算符之外，Kotlin 还提供了 when 表达式，可用于验证输入。 when 表达式类似于其他语言中的 switch 语句，但它更强大，因为它可以匹配任何数据类型：

```kotlin
fun validateInput(input: Any) {
    when (input) {
        is String -> {
            // The input is a string, so we can validate its length, format, etc.
        }
        is Int -> {
            // The input is an integer, so we can validate that it's in the correct range, etc.
        }
        else -> {
            // The input is not a string or an integer, so we can't validate it.
        }
    }
}
```

与 is 运算符一样，when 表达式也可以与自定义数据类型一起使用。例如，如果您有一个“User”数据类，您可以使用“when”表达式来检查输入是否为“User”：

```kotlin
fun validateInput(input: Any) {
    when (input) {
        is User -> {
            // The input is a User, so we can validate its properties, etc.
        }
        else -> {
            // The input is not a User, so we can't validate it.
        }
    }
}
```

## 更高级的技术

### 使用正则表达式

正则表达式（regex）是验证输入的强大工具。正则表达式可用于验证数据类型（例如仅整数）、格式（例如电子邮件地址必须有一个“@”符号）和长度（例如密码必须至少为 8 个字符）。

在 Kotlin 中，您可以使用 `Regex` 类来创建正则表达式模式：

```kotlin
val regexPattern = Regex("^\\d+$") // This regex pattern matches integers only.
```

一旦有了正则表达式模式，就可以使用“matches”函数来检查字符串是否与该模式匹配：

```kotlin
fun validateInput(input: String) {
    if (regexPattern.matches(input)) {
        // The input matches the regex pattern, so it's valid.
    } else {
        // The input doesn't match the regex pattern, so it's invalid.
    }
}
```

### 使用自定义验证器

除了 is 运算符和 when 表达式之外，Kotlin 还提供了一个可用于验证输入的 validate 函数。 `validate` 函数将 `Validator<T>` 作为参数，其中 `T` 是输入的数据类型。

`Validator<T>` 是一个包含 `validate` 函数的类，该函数接受 `input: T` 作为参数并返回 `ValidationResult`。 `ValidationResult` 是一个包含两个值的枚举：`Valid` 和 `Invalid`。

下面是验证整数是否在 1-10 范围内的“Validator<Int>”示例：

```kotlin
class IntRangeValidator(val min: Int, val max: Int) : Validator<Int> {
    override fun validate(input: Int): ValidationResult {
        return if (input in min..max) {
            ValidationResult.Valid
        } else {
            ValidationResult.Invalid
        }
    }
}
```

要使用验证器，您可以使用验证器和输入调用“validate”函数：

```kotlin
fun validateInput(input: Int) {
    val validationResult = validate(IntRangeValidator(1, 10), input)
    if (validationResult == ValidationResult.Valid) {
        // The input is valid.
    } else {
        // The input is invalid.
    }
}
```

## 编写可维护和可重用代码的技巧

验证输入可能是一个耗时且容易出错的过程。幸运的是，您可以做一些事情让您的生活更轻松。

### 使用现有库

有许多库可以为您处理输入验证。如果可能，请使用这些库之一而不是编写您自己的代码。

例如，Kotlin 标准库包含一组用于验证数据类型、格式和长度的函数：

```kotlin
fun validateString(input: String) {
    // Validates that the input is a string.
}

fun validateEmail(input: String) {
    // Validates that the input is a valid email address.
}

fun validatePassword(input: String) {
    // Validates that the input is a valid password.
}
```

### 编写可维护的代码

在编写输入验证代码时，编写可维护的代码很重要。这意味着代码易于阅读、易于理解和易于更改。

使代码更易于维护的一种方法是使用描述性变量名。例如，不使用 `input`，而是使用更具描述性的名称，例如 `emailAddress`：

```kotlin
fun validateEmail(emailAddress: String) {
    // Validates that the email address is valid.
}
```

使代码更易于维护的另一种方法是使用注释。注释可用于解释您的代码在做什么以及为什么要这样做。例如：

```kotlin
// This regex pattern matches email addresses that contain a '@' symbol.
val regexPattern = Regex("^[^@]+@[^@]+$")

fun validateEmail(input: String) {
    if (regexPattern.matches(input)) {
        // The input is a valid email address.
    } else {
        // The input is not a valid email address.
    }
}
```

### 编写可重用代码

编写可重用的代码也很重要。这意味着无需更改即可在多个地方使用的代码。

使代码更易于重用的一种方法是创建可在多个地方使用的函数和类。例如，您可以创建一个“ValidationUtils”类，其中包含用于验证数据类型、格式和长度的函数：

```kotlin
class ValidationUtils {
    fun validateString(input: String) {
        // Validates that the input is a string.
    }

    fun validateEmail(input: String) {
        // Validates that the input is a valid email address.
    }

    fun validatePassword(input: String) {
        // Validates that the input is a valid password.
    }
}
```

另一种使代码更可重用的方法是创建扩展函数。扩展函数是可以添加到现有数据类型的函数。例如，您可以为“字符串”数据类型创建一个扩展函数，以验证字符串是否为有效的电子邮件地址：

```kotlin
fun String.isValidEmail(): Boolean {
    // Validates that the input is a valid email address.
    return this.contains("@")
}
```

## 结论

在本文中，我们了解了一些在 Kotlin 中验证输入的高级技术。我们回顾了输入验证的基础知识，并研究了一些更高级的技术，包括使用正则表达式和自定义验证器。最后，我们总结了一些编写更易于维护和可重用代码的技巧。