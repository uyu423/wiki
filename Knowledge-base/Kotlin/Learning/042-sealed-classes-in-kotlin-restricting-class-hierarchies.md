---
title: 042: Kotlin의 봉인된 클래스: 클래스 계층 구조 제한
description: 
published: true
date: 2023-01-31T10:36:17.235Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:36:15.739Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [042: Sealed Classes in Kotlin: Restricting Class Hierarchies***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/042-sealed-classes-in-kotlin-restricting-class-hierarchies)
{.links-list}



# 042: Kotlin의 봉인된 클래스: 클래스 계층 구조 제한

봉인된 클래스는 클래스 계층 구조를 제한하기 위한 Kotlin의 강력한 도구입니다. 클래스를 봉인하여 다른 클래스에 의해 확장되는 것을 방지할 수 있습니다. 이는 여러 상황에서 유용할 수 있습니다. 예를 들어 같은 파일의 클래스에 의해서만 클래스가 확장되도록 제한하려는 경우입니다.

봉인된 클래스는 봉인된 키워드를 사용하여 선언됩니다.

```kotlin
sealed class MySealedClass
```

봉인된 클래스는 봉인된 클래스와 동일한 파일에 선언된 클래스를 제외하고는 다른 클래스로 확장할 수 없습니다. 예를 들어 다음 코드는 컴파일되지 않습니다.

```kotlin
// MySealedClass.kt

sealed class MySealedClass

class MySubclass : MySealedClass() // Will not compile
```

봉인된 클래스를 확장하기 위해서는 봉인된 클래스와 동일한 파일에 하위 클래스가 선언되어야 합니다. 이를 *로컬 봉인 클래스*라고 합니다.

```kotlin
// MySealedClass.kt

sealed class MySealedClass

class MySubclass : MySealedClass() // Compiles
```

봉인된 클래스는 다른 클래스나 개체 안에 *중첩*될 수도 있습니다. 이 경우 봉인된 클래스는 동일한 상위 클래스 또는 개체 *내부*에서 선언된 클래스에 의해서만 확장될 수 있습니다. 예를 들어:

```kotlin
// MyOuterClass.kt

class MyOuterClass {

    sealed class MySealedClass

    class MySubclass : MySealedClass() // Compiles
}

class MyOtherSubclass : MyOuterClass.MySealedClass() // Will not compile
```

봉인된 클래스는 클래스 계층을 제한하는 유용한 도구이며 다양한 상황에서 사용할 수 있습니다. 특히 클래스가 동일한 파일의 클래스에 의해서만 확장될 수 있도록 하는 데 도움이 될 수 있습니다.