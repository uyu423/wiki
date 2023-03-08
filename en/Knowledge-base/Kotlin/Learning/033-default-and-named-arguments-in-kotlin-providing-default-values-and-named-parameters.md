---
title: 033: Default and Named Arguments in Kotlin: Providing Default Values and Named Parameters
description: 
published: true
date: 2023-02-01T12:04:40.308Z
tags: 
editor: markdown
dateCreated: 2023-02-01T12:04:36.822Z
---

- [033: Kotlin의 기본 및 명명된 인수: 기본값 및 명명된 매개변수 제공***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/033-default-and-named-arguments-in-kotlin-providing-default-values-and-named-parameters)
{.links-list}
- [033：Kotlin 中的默认参数和命名参数：提供默认值和命名参数***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/033-default-and-named-arguments-in-kotlin-providing-default-values-and-named-parameters)
{.links-list}



# 033: Default and Named Arguments in Kotlin: Providing Default Values and Named Parameters

Kotlin's support for default and named arguments makes it easy to provide sensible defaults for function parameters and to specify only the arguments that differ from the defaults.

## Default Arguments

Consider a function that formats a string with a date and time:

```kotlin
fun formatDateTime(
    date: String,
    time: String,
    dateFormat: String = "yyyy-MM-dd",
    timeFormat: String = "HH:mm:ss"
): String {
    return "$date $time"
}
```

This function has four parameters, two of which have default values. When calling the function, we can provide values for the first two parameters, and the default values will be used for the latter two:

```kotlin
formatDateTime("2019-01-01", "12:00:00") // "2019-01-01 12:00:00"
```

We can also provide values for all four parameters:

```kotlin
formatDateTime(
    date = "2019-01-01",
    time = "12:00:00",
    dateFormat = "dd/MM/yy",
    timeFormat = "hh:mm a"
) // "01/01/19 12:00 PM"
```

## Named Arguments

When calling a function with multiple parameters, the order of the parameters is important. This can make the code difficult to read, especially when some of the parameters have default values.

Kotlin's support for named arguments lets us specify the parameter name along with the value, which makes the code easier to read:

```kotlin
fun formatDateTime(
    date: String,
    time: String,
    dateFormat: String = "yyyy-MM-dd",
    timeFormat: String = "HH:mm:ss"
): String {
    return "$date $time"
}
 
formatDateTime(
    time = "12:00:00",
    date = "2019-01-01",
    timeFormat = "hh:mm a",
    dateFormat = "dd/MM/yy"
) // "01/01/19 12:00 PM"
```

In the example above, we've specified the parameter names along with the values. This makes the code easier to read, especially when some of the parameters have default values.

## Specifying Only the Arguments that Differ from the Defaults

When calling a function with multiple parameters, we can specify only the arguments that differ from the defaults. For example, consider the following function:

```kotlin
fun formatDateTime(
    date: String,
    time: String,
    dateFormat: String = "yyyy-MM-dd",
    timeFormat: String = "HH:mm:ss"
): String {
    return "$date $time"
}
```

This function has four parameters, two of which have default values. We can call this function with two arguments, and the default values will be used for the remaining parameters:

```kotlin
formatDateTime("2019-01-01", "12:00:00") // "2019-01-01 12:00:00"
```

We can also specify only the arguments that differ from the defaults:

```kotlin
formatDateTime(
    date = "2019-01-01",
    time = "12:00:00",
    timeFormat = "hh:mm a"
) // "2019-01-01 12:00:00"
```

In the example above, we've specified values for the `date` and `time` parameters, and the default value will be used for the `dateFormat` parameter.

## Conclusion

Kotlin's support for default and named arguments makes it easy to provide sensible defaults for function parameters and to specify only the arguments that differ from the defaults. This can make the code easier to read and understand.