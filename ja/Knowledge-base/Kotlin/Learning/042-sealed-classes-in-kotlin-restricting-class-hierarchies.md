---
title: 042: Kotlin の封印されたクラス: クラス階層の制限
description: 
published: true
date: 2023-01-31T10:36:17.342Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:36:15.746Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [042: Sealed Classes in Kotlin: Restricting Class Hierarchies***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/042-sealed-classes-in-kotlin-restricting-class-hierarchies)
{.links-list}



#042：Kotlinの封印されたクラス：クラス階層の制限

封印されたクラスは、クラス階層を制限するためのKotlinの強力なツールです。クラスを封印して、他のクラスによって拡張されるのを防ぎます。これはさまざまな状況で役に立ちます。たとえば、同じファイル内のクラスによってのみクラスが拡張されるように制限したい場合です。

封印されたクラスは、封印されたキーワードを使用して宣言されます。

```kotlin
sealed class MySealedClass
```

封印されたクラスは、封印されたクラスと同じファイルで宣言されたクラスを除いて、他のクラスに拡張することはできません。たとえば、次のコードはコンパイルされません。

```kotlin
// MySealedClass.kt

sealed class MySealedClass

class MySubclass : MySealedClass() // Will not compile
```

封印されたクラスを拡張するには、封印されたクラスと同じファイルでサブクラスを宣言する必要があります。これを「ローカル封印クラス」といいます。

```kotlin
// MySealedClass.kt

sealed class MySealedClass

class MySubclass : MySealedClass() // Compiles
```

封印されたクラスは、他のクラスまたはオブジェクトに*入れ子にすることもできます。この場合、封印されたクラスは、同じ親クラスまたはオブジェクト*内部*で宣言されたクラスによってのみ拡張できます。たとえば、

```kotlin
// MyOuterClass.kt

class MyOuterClass {

    sealed class MySealedClass

    class MySubclass : MySealedClass() // Compiles
}

class MyOtherSubclass : MyOuterClass.MySealedClass() // Will not compile
```

封印されたクラスはクラス階層を制限する便利なツールであり、さまざまな状況で使用できます。特に、クラスが同じファイル内のクラスによってのみ拡張できるようにするのに役立ちます。