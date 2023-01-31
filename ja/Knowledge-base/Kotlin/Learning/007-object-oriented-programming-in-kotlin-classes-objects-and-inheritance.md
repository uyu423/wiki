---
title: 007: Kotlin でのオブジェクト指向プログラミング: クラス、オブジェクト、および継承
description: 
published: true
date: 2023-01-31T04:57:35.319Z
tags: 
editor: markdown
dateCreated: 2023-01-31T04:57:35.319Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [007: Object-Oriented Programming in Kotlin: Classes, Objects, and Inheritance***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/007-object-oriented-programming-in-kotlin-classes-objects-and-inheritance)
{.links-list}
 

#007：Kotlinのオブジェクト指向プログラミング：クラス、オブジェクト、継承

KotlinはJVM上で動作する静的型プログラミング言語です。簡潔で安全で、Javaと完全に相互運用可能な最新の言語です。 Kotlinはオブジェクト指向言語なので、開発者ははるかにモジュール化された方法でプログラムを書くことができます。

Kotlinでは、IntやStringなどの基本型を含むすべてがオブジェクトです。これは、これらの型のメソッドを呼び出すことができ、クラスを定義して独自の型を作成できることを意味します。この記事では、Kotlinでクラスを定義し、オブジェクトを作成し、継承を実行する方法について説明します。

## クラス定義

Kotlinでは、「クラス」とキーワード：

「コトリン
クラスマイクラス{

}
```

We can also specify the class' primary constructor when we define the class:

「コトリン
クラスMyClass（値名：文字列）{

}
```

If we need to define a class that doesn't have a primary constructor, we can use the ```constructor '' keyword:

「コトリン
クラスマイクラス{
    コンストラクタ（名前：文字列）{

    }
}
```

## Creating Objects

To create an object of a class, we use the ``new'' keyword:

「コトリン
val myObject = MyClass("ゾーン")
```

We can also create objects without using the "new" keyword:

「コトリン
val myObject = MyClass.create("ゾーン")
```

## Inheritance

Kotlin supports single inheritance, meaning that a class can only inherit from one other class. We use the ``:````operator to specify the superclass:

「コトリン
class MyClass : MySuperclass() {

}
```

If the superclass has a primary constructor, we need to call it from the subclass:

「コトリン
class MyClass（名前：文字列）：MySuperclass（名前）{

}
```

We can also override methods from the superclass:

「コトリン
class MyClass : MySuperclass() {
    オーバーライドの楽しみ myMethod() {
        //何か
    }
}
```

If we need to access the superclass implementation of a method, we use the ``super```keyword:

「コトリン
class MyClass : MySuperclass() {
    オーバーライドの楽しみ myMethod() {
        super.myMethod()
        //何か
    }
}
```

##結論

この記事では、Kotlinでクラスを定義し、オブジェクトを作成し、継承を実行する方法について説明しました。 Kotlinのオブジェクト指向機能により、開発者ははるかにモジュール化された方法でプログラムを書くことができます。