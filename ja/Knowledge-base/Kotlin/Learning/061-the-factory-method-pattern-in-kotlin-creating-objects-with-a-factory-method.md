---
title: 061: Kotlin のファクトリー メソッド パターン: ファクトリー メソッドでオブジェクトを作成する
description: 
published: true
date: 2023-01-31T09:04:58.712Z
tags: 
editor: markdown
dateCreated: 2023-01-31T09:04:57.098Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [061: The Factory Method Pattern in Kotlin: Creating Objects with a Factory Method***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/061-the-factory-method-pattern-in-kotlin-creating-objects-with-a-factory-method)
{.links-list}




#061：Kotlinのファクトリメソッドパターン：ファクトリメソッドでオブジェクトを作成する

ソフトウェア開発では、ファクトリメソッドパターンは、ファクトリメソッドを使用して生成されるオブジェクトの正確なクラスを指定することなく、オブジェクト生成の問題を処理する生成設計パターンです。これは、コンストラクタを呼び出すのではなく、ファクトリメソッドを介してオブジェクトを生成することによって行われます。

この記事では、ファクトリメソッドパターンとそれをKotlinで使用してオブジェクトを作成する方法について説明します。また、このパターンを実際にどのように使用できるかを示すために、いくつかのコード例を見てみましょう。

# # ファクトリメソッドパターンとは？

ファクトリメソッドパターンは、生成されるオブジェクトの正確なクラスを指定することなく、オブジェクト生成の問題を処理するためにファクトリメソッドを使用する生成デザインパターンです。これは、コンストラクタを呼び出すのではなく、ファクトリメソッドを介してオブジェクトを生成することによって行われます。

ファクトリメソッドパターンは、仮想コンストラクタパターンおよびファクトリパターンとも呼ばれます。オブジェクト生成の詳細を抽象化し、クラス名をハードコーディングすることなく新しいオブジェクトを生成できるようにするために使用されます。

## ファクトリメソッドパターンはどのように機能しますか？

ファクトリメソッドパターンは、動作するために継承に依存します。オブジェクトを生成するためのインタフェースまたは抽象クラスを定義し、インタフェースを実装するか、抽象クラスから継承して実際にオブジェクトを生成する具体的なサブクラスを定義します。

Factory Method Patternによって生成されたオブジェクトを使用するクライアントコードは、オブジェクトを生成するために使用される特定のクラスを知ったり気にする必要はなく、インターフェイスまたは抽象クラスだけを知ることができます。

## ファクトリメソッドパターンを使用する場合

ファクトリメソッドパターンは、次の状況で使用できます。

- 生成するオブジェクトがあらかじめ分からない場合
- 生成するオブジェクトを使用するコードの他の部分で生成する必要がある場合
- ランタイムまで不明なデータから生成するオブジェクトを生成する必要がある場合

## ファクトリメソッドパターンの利点

ファクトリメソッドパターンには次の利点があります。

- クラス名をハードコーディングせずにオブジェクトを作成できます。
- オブジェクトが使用されるコードの他の部分からオブジェクトを生成できます。
- ランタイムまで未知のデータからオブジェクトを生成できます。

## ファクトリメソッドパターンの欠点

ファクトリメソッドパターンには、次の欠点があります。

- コードを読みやすく理解しにくくすることができます。
- コードをデバッグしにくくすることができます。
- 多くのコードの重複が発生する可能性があります。

## コートリンの実装

KotlinはFactory Method Patternをデフォルトでサポートしていませんが、Kotlinで実装できます。

KotlinでFactory Method Patternを実装する1つの方法は、コンパニオンオブジェクトを使用することです。コンパニオンオブジェクトは、クラスに関連付けられたオブジェクトです。クラスはコンパニオンオブジェクトを1つだけ持つことができ、その逆も同様です。

コンパニオンオブジェクトは、次のようにファクトリメソッドパターンを実装するために使用できます。

```kotlin
interface Shape {
    fun draw()
}

class Circle: Shape {
    override fun draw() {
        println("Circle.draw()")
    }
}

class Rectangle: Shape {
    override fun draw() {
        println("Rectangle.draw()")
    }
}

class Triangle: Shape {
    override fun draw() {
        println("Triangle.draw()")
    }
}

object ShapeFactory {
    fun getShape(shapeType: String): Shape? {
        if(shapeType == null) {
            return null
        }
        if(shapeType.equals("CIRCLE", ignoreCase = true)) {
            return Circle()
        } else if(shapeType.equals("RECTANGLE", ignoreCase = true)) {
            return Rectangle()
        } else if(shapeType.equals("TRIANGLE", ignoreCase = true)) {
            return Triangle()
        }
        return null
    }
}
```

上記のコードでは、ShapeインタフェースとShapeインタフェースを実装する3つの具体的なクラスを定義しました。また、ファクトリメソッドgetShape（）を含むコンパニオンオブジェクトShapeFactoryを定義しました。このファクトリメソッドは文字列パラメータshapeTypeを使用し、Shape型のオブジェクトを返します。

次のように ShapeFactory 同伴オブジェクトを使用できます。

```kotlin
val circle = ShapeFactory.getShape("CIRCLE")
circle?.draw()

val rectangle = ShapeFactory.getShape("RECTANGLE")
rectangle?.draw()

val triangle = ShapeFactory.getShape("TRIANGLE")
triangle?.draw()
```

上記のコードでは、ShapeFactoryコンパニオンオブジェクトを使用して、各タイプごとに1つずつ3つのオブジェクトを作成しました。次に、各オブジェクトに対してdraw（）メソッドを呼び出してその型を表示しました。

あるいは、オブジェクト宣言を使用して、次のようにFactoryメソッドパターンを実装できます。

```kotlin
interface Shape {
    fun draw()
}

class Circle: Shape {
    override fun draw() {
        println("Circle.draw()")
    }
}

class Rectangle: Shape {
    override fun draw() {
        println("Rectangle.draw()")
    }
}

class Triangle: Shape {
    override fun draw() {
        println("Triangle.draw()")
    }
}

object ShapeFactory {
    fun getShape(shapeType: String): Shape? {
        if(shapeType == null) {
            return null
        }
        if(shapeType.equals("CIRCLE", ignoreCase = true)) {
            return Circle()
        } else if(shapeType.equals("RECTANGLE", ignoreCase = true)) {
            return Rectangle()
        } else if(shapeType.equals("TRIANGLE", ignoreCase = true)) {
            return Triangle()
        }
        return null
    }
}

fun main(args: Array<String>) {
    val circle = ShapeFactory.getShape("CIRCLE")
    circle?.draw()

    val rectangle = ShapeFactory.getShape("RECTANGLE")
    rectangle?.draw()

    val triangle = ShapeFactory.getShape("TRIANGLE")
    triangle?.draw()
}
```

上記のコードでは、ファクトリメソッドgetShape（）を含むオブジェクト宣言ShapeFactoryを定義しました。このファクトリメソッドは文字列パラメータshapeTypeを使用し、Shape型のオブジェクトを返します。

次のように ShapeFactory オブジェクトを使用できます。

```kotlin
val circle = ShapeFactory.getShape("CIRCLE")
circle?.draw()

val rectangle = ShapeFactory.getShape("RECTANGLE")
rectangle?.draw()

val triangle = ShapeFactory.getShape("TRIANGLE")
triangle?.draw()
```

上記のコードでは、ShapeFactoryオブジェクトを使用して各タイプごとに1つずつ3つのオブジェクトを作成しました。次に、各オブジェクトに対してdraw（）メソッドを呼び出してその型を表示しました。

## 抽象ファクトリーパターンとの比較

抽象ファクトリパターンはファクトリメソッドパターンと似ていますが、目的は異なります。抽象ファクトリパターンは関連オブジェクトまたは依存オブジェクトのファミリを生成するために使用され、ファクトリメソッドパターンは個々のオブジェクトを生成するために使用されます。

抽象ファクトリパターンは、ファクトリメソッドパターンよりも複雑です。抽象ファクトリパターンには1つ以上の具体的なファクトリが必要ですが、ファクトリメソッドパターンには1つの具体的なファクトリのみが必要です。

## 結論

この記事では、ファクトリメソッドパターンとKotlinでそれを使用してオブジェクトを作成する方法について説明しました。また、このパターンを実際にどのように使用できるかを示すために、いくつかのコード例を見ました。