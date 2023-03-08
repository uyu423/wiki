---
title: 047: Late-initialized Properties in Kotlin: Initializing Properties Lazy and Safe
description: 
published: true
date: 2023-02-16T14:32:21.381Z
tags: 
editor: markdown
dateCreated: 2023-02-16T14:32:19.419Z
---

- [047: Propiedades de inicialización tardía en Kotlin: inicialización de propiedades perezosas y seguras***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/047-late-initialized-properties-in-kotlin-initializing-properties-lazy-and-safe)
{.links-list}
- [047：Kotlin 中的延迟初始化属性：惰性且安全地初始化属性***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/047-late-initialized-properties-in-kotlin-initializing-properties-lazy-and-safe)
{.links-list}
- [047: Kotlin에서 늦게 초기화된 속성: 지연되고 안전한 속성 초기화***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/047-late-initialized-properties-in-kotlin-initializing-properties-lazy-and-safe)
{.links-list}


# Late-initialized Properties in Kotlin: Initializing Properties Lazy and Safe

Kotlin's late-initialized properties are a great way to initialize properties lazily and safely. In this post, we'll take a look at how to use late-initialized properties to our advantage.

## What are late-initialized properties?

Late-initialized properties are properties that are not initialized during the object's construction. Instead, they are initialized during the first access to the property. This is useful for properties that are expensive to initialize or that are not used often.

## How to use late-initialized properties

To use a late-initialized property, we first need to declare it with the ```lateinit``` keyword:

```kotlin
lateinit var property: Type
```

We can then initialize the property when we first access it:

```kotlin
property = value
```

## Advantages of late-initialized properties

There are two main advantages to using late-initialized properties: performance and safety.

### Performance

Late-initialized properties can improve performance because they are not initialized until they are first accessed. This means that we can avoid initializing properties that are not used often.

### Safety

Late-initialized properties are also safe to use. This is because they are not initialized until they are first accessed. This means that we can avoid using properties that have not been initialized yet.

## Disadvantages of late-initialized properties

There are two main disadvantages to using late-initialized properties: readability and debugging.

### Readability

Late-initialized properties can be more difficult to read because they are not initialized until they are first accessed. This means that we need to be careful to initialize the properties before we use them.

### Debugging

Late-initialized properties can also be more difficult to debug because they are not initialized until they are first accessed. This means that we need to be careful to initialize the properties before we use them.