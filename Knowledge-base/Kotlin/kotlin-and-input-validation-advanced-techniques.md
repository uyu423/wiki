---
title: Kotlin 및 입력 유효성 검사: 고급 기술
description: 
published: true
date: 2023-02-17T18:03:02.720Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:29:33.324Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kotlin and Input Validation: Advanced Techniques***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-input-validation-advanced-techniques)
{.links-list}
 

# Kotlin 및 입력 유효성 검사: 고급 기술

사용자 입력 유효성 검사는 데스크톱 앱, 웹 앱, 모바일 앱 등 모든 애플리케이션에서 중요한 부분입니다. 이 기사에서는 Kotlin에서 입력을 검증하는 몇 가지 고급 기술을 살펴보겠습니다.

입력 유효성 검사의 기본 사항을 검토하는 것으로 시작하겠습니다. 그런 다음 정규식 및 사용자 지정 유효성 검사기 사용을 포함하여 몇 가지 고급 기술을 살펴보겠습니다. 마지막으로 더 유지 관리 및 재사용 가능한 코드를 작성하기 위한 몇 가지 팁으로 마무리하겠습니다.

## 검토: 입력 유효성 검사의 기본 사항

입력 유효성 검사는 사용자가 제공한 데이터가 애플리케이션의 요구 사항을 충족하는지 확인하는 프로세스입니다. 이러한 요구 사항은 데이터 유형(예: 정수만)에서 형식(예: 이메일 주소에는 "@" 기호가 있어야 함), 길이(예: 암호는 8자 이상이어야 함)에 이르기까지 무엇이든 될 수 있습니다.

입력 유효성 검사는 다음 두 가지 주요 이유로 중요합니다.

- **보안:** 잘못된 데이터는 애플리케이션의 취약점을 악용하는 데 사용될 수 있습니다. 예를 들어, 이메일 주소를 확인하지 않는 경우 악의적인 사용자가 `">@example.com<script>alert('xss')</script>"`와 같은 이메일 주소를 입력할 수 있습니다. 그러면 XSS가 생성됩니다. 공격.

- **데이터 품질:** 잘못된 데이터로 인해 애플리케이션이 오작동할 수 있습니다. 예를 들어 필드가 정수인지 확인하지 않으면 데이터에 대해 수학 연산을 수행하려고 할 때 예기치 않은 결과가 발생할 수 있습니다.

Kotlin에는 입력을 검증하는 다양한 방법이 있습니다. 가장 기본적인 방법은 `is` 연산자를 사용하여 변수의 데이터 유형을 확인하는 것입니다.

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

`is` 연산자는 사용자 정의 데이터 유형을 포함하여 모든 데이터 유형과 함께 사용할 수 있습니다. 예를 들어 `User` 데이터 클래스가 있는 경우 `is` 연산자를 사용하여 입력이 `User`인지 확인할 수 있습니다.

```kotlin
fun validateInput(input: Any) {
    if (input is User) {
        // The input is a User, so we can validate its properties, etc.
    } else {
        // The input is not a User, so we can't validate it.
    }
}
```

'is' 연산자 외에도 Kotlin은 입력의 유효성을 검사하는 데 사용할 수 있는 'when' 표현식도 제공합니다. `when` 표현식은 다른 언어의 `switch` 문과 유사하지만 모든 데이터 유형과 일치시킬 수 있기 때문에 더 강력합니다.

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

`is` 연산자와 마찬가지로 `when` 표현식도 사용자 정의 데이터 유형과 함께 사용할 수 있습니다. 예를 들어 `User` 데이터 클래스가 있는 경우 `when` 표현식을 사용하여 입력이 `User`인지 확인할 수 있습니다.

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

## 고급 기술

### 정규 표현식 사용

정규식(regex)은 입력을 검증하는 강력한 도구입니다. Regex는 데이터 유형(예: 정수만), 형식(예: 이메일 주소에는 "@" 기호가 있어야 함) 및 길이(예: 비밀번호는 8자 이상이어야 함)를 검증하는 데 사용할 수 있습니다.

Kotlin에서는 `Regex` 클래스를 사용하여 정규식 패턴을 만들 수 있습니다.

```kotlin
val regexPattern = Regex("^\\d+$") // This regex pattern matches integers only.
```

정규식 패턴이 있으면 `matches` 함수를 사용하여 문자열이 패턴과 일치하는지 확인할 수 있습니다.

```kotlin
fun validateInput(input: String) {
    if (regexPattern.matches(input)) {
        // The input matches the regex pattern, so it's valid.
    } else {
        // The input doesn't match the regex pattern, so it's invalid.
    }
}
```

### 사용자 지정 유효성 검사기 사용

`is` 연산자와 `when` 표현식 외에도 Kotlin은 입력의 유효성을 검사하는 데 사용할 수 있는 `validate` 함수도 제공합니다. 'validate' 함수는 'Validator<T>'를 인수로 사용하며, 여기서 'T'는 입력의 데이터 유형입니다.

'Validator<T>'는 '입력: T'를 인수로 사용하고 'ValidationResult'를 반환하는 'validate' 함수를 포함하는 클래스입니다. 'ValidationResult'는 'Valid' 및 'Invalid'의 두 값을 포함하는 열거형입니다.

다음은 정수가 1-10 범위에 있는지 확인하는 `Validator<Int>`의 예입니다.

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

유효성 검사기를 사용하려면 유효성 검사기 및 입력과 함께 `validate` 함수를 호출합니다.

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

## 유지 관리 및 재사용 가능한 코드 작성을 위한 팁

입력 유효성 검사는 시간이 오래 걸리고 오류가 발생하기 쉬운 프로세스일 수 있습니다. 운 좋게도 삶을 더 쉽게 만들기 위해 할 수 있는 몇 가지 일이 있습니다.

### 기존 라이브러리 사용

입력 유효성 검사를 처리할 수 있는 많은 라이브러리가 있습니다. 가능하면 자체 코드를 작성하는 대신 이러한 라이브러리 중 하나를 사용하십시오.

예를 들어 Kotlin 표준 라이브러리에는 데이터 유형, 형식 및 길이의 유효성을 검사하기 위한 함수 집합이 포함되어 있습니다.

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

### 유지 가능한 코드 작성

입력 유효성 검사 코드를 작성할 때 유지 관리 가능한 코드를 작성하는 것이 중요합니다. 이것은 읽기 쉽고, 이해하기 쉽고, 변경하기 쉬운 코드를 의미합니다.

코드를 보다 유지 관리하기 쉽게 만드는 한 가지 방법은 설명이 포함된 변수 이름을 사용하는 것입니다. 예를 들어 `input`을 사용하는 대신 `emailAddress`와 같이 보다 설명적인 이름을 사용하십시오.

```kotlin
fun validateEmail(emailAddress: String) {
    // Validates that the email address is valid.
}
```

코드를 유지 관리하기 쉽게 만드는 또 다른 방법은 주석을 사용하는 것입니다. 주석은 코드가 수행하는 작업과 수행 이유를 설명하는 데 사용할 수 있습니다. 예를 들어:

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

### 재사용 가능한 코드 작성

재사용 가능한 코드를 작성하는 것도 중요합니다. 이는 변경하지 않고도 여러 곳에서 사용할 수 있는 코드를 의미합니다.

코드를 더 재사용 가능하게 만드는 한 가지 방법은 여러 위치에서 사용할 수 있는 함수와 클래스를 만드는 것입니다. 예를 들어 데이터 유형, 형식 및 길이의 유효성을 검사하는 함수가 포함된 `ValidationUtils` 클래스를 만들 수 있습니다.

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

코드를 더 재사용 가능하게 만드는 또 다른 방법은 확장 기능을 만드는 것입니다. 확장 함수는 기존 데이터 유형에 추가할 수 있는 함수입니다. 예를 들어 문자열이 유효한 이메일 주소인지 확인하는 `String` 데이터 유형에 대한 확장 함수를 만들 수 있습니다.

```kotlin
fun String.isValidEmail(): Boolean {
    // Validates that the input is a valid email address.
    return this.contains("@")
}
```

## 결론

이 기사에서는 Kotlin에서 입력을 검증하는 몇 가지 고급 기술을 살펴보았습니다. 입력 유효성 검사의 기본 사항을 검토하고 정규식 및 사용자 지정 유효성 검사기 사용을 포함하여 몇 가지 고급 기술을 살펴보았습니다. 마지막으로 더 유지 관리 및 재사용 가능한 코드를 작성하기 위한 몇 가지 팁으로 마무리했습니다.