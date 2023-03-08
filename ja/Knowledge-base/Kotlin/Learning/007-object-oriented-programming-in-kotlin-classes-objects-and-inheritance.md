---
title: 007: Kotlin でのオブジェクト指向プログラミング: クラス、オブジェクト、および継承
description: 
published: true
date: 2023-01-31T05:10:52.072Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:10:50.473Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [007: Object-Oriented Programming in Kotlin: Classes, Objects, and Inheritance***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/007-object-oriented-programming-in-kotlin-classes-objects-and-inheritance)
{.links-list}




KotlinはJVMで実行される静的に型指定されたプログラミング言語であり、JavaScriptでコンパイルすることもできます。 KotlinはJavaとの相互運用を可能にするように設計されているため、Androidアプリケーションの開発に優れた選択肢です。

オブジェクト指向プログラミングは、データとメソッドの両方を含むデータ構造であるオブジェクト概念に基づくプログラミングパラダイムです。 Kotlinはオブジェクト指向言語なので、クラス、オブジェクト、継承をサポートしています。

## クラス、オブジェクト、継承

Kotlinでは、クラスはオブジェクトを作成するためのテンプレートです。クラスには、メンバとも呼ばれるプロパティとメソッドを含めることができます。プロパティはクラスに関連するデータフラグメントであり、メソッドはオブジェクトから呼び出すことができる関数です。

Kotlinでクラスを作成するには、キーワード「class」を使用し、その後にクラス名を書き込みます。たとえば、次のコードは `Person` というクラスを作成します。

```kotlin
class Person {

}
```

クラスには、メンバとも呼ばれるプロパティとメソッドを含めることができます。プロパティはクラスに関連するデータフラグメントであり、メソッドはオブジェクトから呼び出すことができる関数です。

クラスに属性を追加するには、キーワード `var` または `val` を使用し、その後に属性名とその型を入力します。たとえば、次のコードは型 `String` の `name` という属性を作成します。

```kotlin
class Person {
    var name: String
}
```

メソッドをクラスに追加するには、`fun`キーワードの後にメソッド名とそのパラメータが使用されます。たとえば、次のコードは、 `String`型の `name`パラメータを使用する `greet`というメソッドを生成します。

```kotlin
class Person {
    fun greet(name: String) {
        println("Hello, $name!")
    }
}
```

クラスからオブジェクトを生成するには、キーワード `new` とクラス名が使用されます。たとえば、次のコードは `Person` クラスからオブジェクトを作成します。

```kotlin
val person = Person()
```

オブジェクトからメソッドを呼び出すために `.`演算子が使用され、その後にメソッド名と対応するパラメータが続きます。たとえば、次のコードは、 `person`オブジェクトから `greet`メソッドを呼び出して、挨拶する人の `name`を渡します。

```kotlin
person.greet("John")
```

## 継承

継承は、あるクラスが別のクラスから派生できるメカニズムです。派生するクラスをスーパークラスと呼び、派生するクラスをサブクラスと呼びます。

Kotlinでは、サブクラスは `:`演算子と親クラス名を使用して定義できます。たとえば、次のコードは `Person` クラスから継承する `Student` クラスを定義します。

```kotlin
class Student: Person {

}
```

サブクラスは親クラスのすべてのプロパティとメソッドを継承し、独自のプロパティとメソッドを定義することもできます。

たとえば、 `Student` クラスは独自の `enroll` メソッドを定義できるだけでなく、次のコードのように `Person` クラスの `greet` メソッドをオーバーライドできます。

```kotlin
class Student: Person {
    fun enroll() {
        // enroll student in class
    }

    override fun greet(name: String) {
        println("Hello, $name! I'm a student.")
    }
}
```

##結論

Kotlinは、クラス、オブジェクト、および継承をサポートする静的に型指定されたオブジェクト指向プログラミング言語です。 KotlinはJavaとの相互運用を可能にするように設計されているため、Androidアプリケーションの開発に優れた選択肢です。