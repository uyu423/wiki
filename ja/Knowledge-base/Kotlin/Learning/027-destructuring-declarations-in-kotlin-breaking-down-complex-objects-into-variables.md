---
title: 027: Kotlin での宣言の構造化解除: 複雑なオブジェクトを変数に分解する
description: 
published: true
date: 2023-02-01T05:23:38.622Z
tags: 
editor: markdown
dateCreated: 2023-02-01T05:23:36.983Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [027: Destructuring Declarations in Kotlin: Breaking Down Complex Objects into Variables***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/027-destructuring-declarations-in-kotlin-breaking-down-complex-objects-into-variables)
{.links-list}


  #027：KotlinのDestructuring Declarations：複雑なオブジェクトを変数に分解する

複雑なオブジェクトは、ソフトウェア開発で作業するのが難しい場合があります。さまざまな部分で構成される可能性があるため、理解して使用するのは困難です。 Kotlinの構造分解宣言を使用すると、複雑なオブジェクトをより小さく管理しやすいフラグメントに分割できるため、複雑なオブジェクトの操作が簡単になります。

この記事では、構造分解宣言が何で、Kotlinでどのように機能するかを見てみましょう。また、複雑なオブジェクト操作を簡素化するためにどのように使用できるかを学びます。

## Destructuring Declarationとは何ですか？

構造分解宣言は、オブジェクトを変数セットに分解できるKotlin言語機能です。これは、オブジェクトで利用可能な `component1()` ~ `componentN()` 関数を使って行われます。これらの関数はオブジェクトの個々の部分を返し、それらを別々の変数に割り当てることができます。

たとえば、次の `Person` クラスを考えてみましょう。

```kotlin
class Person(val name: String, val age: Int)
```

このクラスのインスタンスを作成し、構造分解宣言を使用して2つの変数に分解できます。

```kotlin
val person = Person("John", 30)

val(name, age) = person

println("$name is $age years old")
```

これにより、次のものが印刷されます。

```
John is 30 years old
```

ご覧のとおり、 `component1()` および `component2()` 関数を使用して `person` オブジェクトの `name` および `age` 属性を取得して別々の変数に割り当てることができました。その後、その変数を独立して使用できます。

## データクラスで Destructuring 宣言を使用する

データクラスは、データを保持するように設計されたKotlinの特別な種類のクラスです。通常、データベースまたは他のストレージシステムのデータを表すために使用されます。

データクラスにはいくつかの特別な機能があり、そのうちの1つは `componentN（）`関数を介して `component1（）`関数を自動的に生成することです。したがって、構造分解宣言で使用するのに理想的です。

たとえば、次のデータクラスを考えます。

```kotlin
data class User(val id: Int, val name: String, val age: Int)
```

このクラスのインスタンスを作成し、分解宣言を使用して別の変数に分解できます。

```kotlin
val user = User(1, "John", 30)

val(id, name, age) = user

println("$name (id=$id) is $age years old")
```

これにより、次のものが印刷されます。

```
John (id=1) is 30 years old
```

ご覧のとおり、 `component1()` から `component3()` 関数を使用して `user` オブジェクトの `id`、`name`、および `age` 属性を取得して割り当てることができました。別の変数。その後、その変数を独立して使用できます。

##地図で宣言を破壊する

マップはソフトウェア開発で共通のデータ構造です。キーと値のペアを格納するために使用され、キーはその値を見つけるために使用されます。

Kotlinの構造分解宣言はマップと共に使用され、マップを別々の変数に分解できます。たとえば、次のマップを考えます。

```kotlin
val map = mapOf("id" to 1, "name" to "John", "age" to 30)
```

このマップを別の変数に分解するには、解体宣言を使用できます。

```kotlin
val(id, name, age) = map

println("$name (id=$id) is $age years old")
```

これにより、次のものが印刷されます。

```
John (id=1) is 30 years old
```

ご覧のとおり、 `component1()` から `component3()` 関数を使用してマップから `id`、`name`、および `age` 値を取得して別の変数に割り当てることができました。その後、その変数を独立して使用できます。

##結論

この記事では、Kotlinの構造分解宣言とは何か、複雑なオブジェクト操作を簡素化するためにどのように使用できるかを見てきました。データクラスとマップで使用して別々の変数に分解する方法を見てきました。

Kotlinの詳細については、[Kotlin言語のウェブサイト]（https://kotlinlang.org/）をご覧ください。