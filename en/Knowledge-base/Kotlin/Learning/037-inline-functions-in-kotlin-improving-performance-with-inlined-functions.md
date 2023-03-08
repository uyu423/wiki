---
title: 037: Inline Functions in Kotlin: Improving Performance with Inlined Functions
description: 
published: true
date: 2023-02-16T10:32:29.660Z
tags: 
editor: markdown
dateCreated: 2023-02-16T10:32:21.640Z
---

- [037: Funciones en línea en Kotlin: Mejora del rendimiento con funciones en línea***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/037-inline-functions-in-kotlin-improving-performance-with-inlined-functions)
{.links-list}
- [037：Kotlin 中的内联函数：使用内联函数提高性能***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/037-inline-functions-in-kotlin-improving-performance-with-inlined-functions)
{.links-list}
- [037: Kotlin의 인라인 함수: 인라인 함수로 성능 향상***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/037-inline-functions-in-kotlin-improving-performance-with-inlined-functions)
{.links-list}


## Introduction

Kotlin is a statically typed programming language that runs on the Java Virtual Machine and also can be compiled to JavaScript source code.

In this post, we will take a look at how to improve performance with inlined functions in Kotlin.

## What are Inline Functions?

In Kotlin, inline functions are functions that are expanded in the body of the caller. This is different from non-inline functions, where the function is called as usual.

Inline functions can be used to improve performance by reducing the overhead of function calls. In addition, inline functions can access the variables of the caller, which can also improve performance.

## How to Use Inline Functions

In order to use inline functions, you need to annotate the function with the `inline` keyword.

For example, let's say we have a function `foo()` that we want to inline:

```kotlin
inline fun foo() {
    // do something
}
```

Now, whenever we call `foo()`, the body of the function will be expanded in the caller.

## When to Use Inline Functions

In general, you should only use inline functions when you are sure that inlining the function will improve performance.

In addition, you should only use inline functions if the function is small and simple. This is because inlining a complex function can lead to code bloat and actually decrease performance.

Finally, you should only use inline functions if you are sure that the function will not be called from multiple places. This is because inlining a function can lead to duplicate code if the function is called from multiple places.

## Conclusion

In this post, we have learned about inline functions in Kotlin and how to use them to improve performance. In general, you should only use inline functions when you are sure that inlining the function will improve performance. In addition, you should only use inline functions if the function is small and simple.