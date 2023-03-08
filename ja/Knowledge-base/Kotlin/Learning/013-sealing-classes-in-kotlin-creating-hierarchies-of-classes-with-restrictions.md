---
title: 013: Kotlin でクラスを封印する: 制限付きのクラスの階層を作成する
description: 
published: true
date: 2023-01-31T05:43:40.296Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:43:37.794Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [013: Sealing Classes in Kotlin: Creating Hierarchies of Classes with Restrictions***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/013-sealing-classes-in-kotlin-creating-hierarchies-of-classes-with-restrictions)
{.links-list}


Kotlinの人気が高まるにつれて、ますます多くの開発者がプロジェクトでKotlinを使用する方法を探しています。 Kotlinの主な機能の1つは、クラスを封印する機能で制限のあるクラス階層を作成することです。

この記事では、封印クラスとは何か、Kotlinプロジェクトでどのように使用できるかを見てみましょう。また、シーリングクラスが実際にどのように機能するかを知るために、いくつかのコード例を見てみましょう。

シーリングクラスとは何ですか？

封印クラスは、制限付きクラスの階層を作成する方法です。封印されたクラスは、同じファイルで宣言されたクラスによってのみサブクラス化できます。これにより、クラス階層の設計をよりよく制御でき、より強力で信頼性の高いコードにつながります。

シールクラスを使用する理由は何ですか？

Kotlinコードでシールクラスを使用する理由はいくつかあります。

* 密封クラスを使用して、アクセスが制限されたクラスの階層を作成できます。これは、特定のクラスだけが開発者がアクセスできるようにしたいAPIライブラリを作成するのに役立ちます。

*シールクラスはコードをより強力で信頼性の高いものにすることができます。クラスをサブクラス化する方法を制限することで、コード内の予期しない動作やエラーを防ぐことができます。

*シールクラスはコードをより簡潔にすることができます。クラスを封印すると、複数のサブクラスでコードの反復を回避できます。

シーリングクラスはどのように使用しますか？

Kotlinコードでシーリングクラスを使用するには、次の2つのことを行う必要があります。

1. "sealed" キーワードを使用して、封印されたクラスを宣言します。

```kotlin
sealed class Shape {
}
```

2.封印されたクラスと同じファイルでサブクラスを宣言します。

```kotlin
class Circle: Shape() {
}
```

パラメータを使用して封印されたクラスを宣言することもできます。

```kotlin
sealed class Shape(val name: String) {
}

class Circle: Shape("circle") {
}
```

別のファイルで封印されたクラスのサブクラスを宣言しようとすると、エラーが発生します。

```kotlin
// Error: Cannot subclass sealed class Shape

class Square: Shape() {
}
```

コンパニオンオブジェクトを使用してこの問題を解決できます。

```kotlin
class Square: Shape() {
    companion object : Shape() {
    }
}
```

封印クラスを使用する別の方法は、クラスを抽象的に宣言することです。

```kotlin
abstract sealed class Shape {
}

class Circle: Shape() {
}

class Square: Shape() {
}
```

これにより、サブクラスで実装する必要がある封印されたクラスで抽象メソッドを定義できます。

```kotlin
abstract sealed class Shape {
    abstract fun getArea(): Double
}

class Circle(val radius: Double): Shape() {
    override fun getArea(): Double {
        return Math.PI*radius*radius
    }
}

class Square(val side: Double): Shape() {
    override fun getArea(): Double {
        return side * side
    }
}
```

封印されたクラスを使用して列挙型を作成することもできます。

```kotlin
sealed class Shape {
    class Circle(val radius: Double): Shape()
    class Square(val side: Double): Shape()
}

fun getArea(shape: Shape): Double {
    return when(shape) {
        is Shape.Circle - > Math.PI * shape.radius * shape.radius
        is Shape.Square - > shape.side * shape.side
    }
}
```

これにより、任意のデータで列挙型を作成できます。

```kotlin
enum class Shape(val name: String) {
    CIRCLE("circle"),
    SQUARE("square")
}
```

封印されたクラスを使用して封印されたオブジェクトを作成することもできます。

```kotlin
sealed class Shape {
    object Circle: Shape()
    object Square: Shape()
}

fun getArea(shape: Shape): Double {
    return when(shape) {
        is Shape.Circle -> Math.PI * 1.0 * 1.0
        is Shape.Square -> 1.0 * 1.0
    }
}
```

封印されたオブジェクトはシングルトン型で、メモリ内にオブジェクトインスタンスが1つしかないことを意味します。これは、キャッシュやスレッドプールなどのエントリを作成するのに役立ちます。

封印されたオブジェクトの2番目のインスタンスを作成しようとするとエラーが発生します。

```kotlin
// Error: Object 'Shape.Circle' has already been created

val circle = Shape.Circle
```

Kotlin ドキュメントで封印されたクラスに関する詳細情報を見つけることができます。

https://kotlinlang.org/docs/reference/sealed-classes.html

Kotlinのドキュメントでは、シングルトンに関する詳細情報を見つけることができます。

https://kotlinlang.org/docs/reference/object-declarations.html#object-declarations

要約すると、封印クラスは、制限付きクラスの階層を作成する方法です。封印クラスは、特定のクラスだけが開発者がアクセスできるようにしたいAPIライブラリを作成するのに役立ちます。シールクラスはまた、コードをより強力で信頼性の高いものにすることができます。