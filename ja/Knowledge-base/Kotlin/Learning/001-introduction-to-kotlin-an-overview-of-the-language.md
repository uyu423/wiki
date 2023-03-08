---
title: 001: Kotlin の紹介: 言語の概要
description: 
published: true
date: 2023-01-31T06:04:18.123Z
tags: 
editor: markdown
dateCreated: 2023-01-31T06:04:16.538Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [001: Introduction to Kotlin: An Overview of the Language***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/001-introduction-to-kotlin-an-overview-of-the-language)
{.links-list}



#コトリン

KotlinはJava Virtual Machine（JVM）で実行される静的に型指定されたプログラミング言語であり、JavaScriptソースコードにコンパイルすることもできます。 Kotlinは、IntelliJ IDEA Java IDEを作成した会社JetBrainsによって開発されました。

Kotlinは、型推論機能を備えたクロスプラットフォーム、静的型、汎用プログラミング言語です。 KotlinはJavaと完全に相互運用できるように設計されており、標準ライブラリのJVMバージョンはJavaクラスライブラリに依存していますが、型推論によって構文がより簡潔になります。

## 特徴

Kotlinには次の機能があります。

- **Null安全性**: Kotlinの型システムは、null参照が逆参照されるのを防ぎます。

- **拡張機能**：Kotlinを使用すると、クラスから継承することなく新しい機能でクラスを拡張できます。

- **高次関数とラムダ**：Kotlinは高次関数とラムダをサポートします。

- **データクラス**：Kotlinは、データのみを含むクラスを作成する簡潔な方法を提供します。

- **コンパニオンオブジェクト**：Kotlinを使用すると、コンパニオンオブジェクトでクラスの静的メンバーを定義できます。

- **オブジェクト指向**：Kotlinはオブジェクト指向ですが、関数型プログラミングもサポートしています。

- **Kotlin標準ライブラリ**：Kotlinには、豊富な関数と型のセットを含む標準ライブラリが付属しています。

## 構文

Kotlinは簡単に習得する簡潔な構文を持っています。

```kotlin
// Define a function that takes two Int arguments and returns an Int.
fun sum(a: Int, b: Int): Int {
   return a+b
}

// Define a data class.
data class User(val name: String, val age: Int)

// Define a companion object.
object MyClass {
   fun doSomething() { ... }
}

// Define a higher-order function.
fun MyClass.myFunction(a: Int, b: Int, f: (Int, Int) -> Int): Int {
   return f(a, b)
}

// Use a lambda expression.
val result = MyClass.myFunction(1, 2) { a, b -> a + b }

// Define an extension function.
fun String.toUpperCase(): String {
   return this.toUpperCase()
}
```

##はじめに

Kotlinを起動するには、IntelliJ IDEAまたはEclipse用のKotlinプラグインをダウンロードできます。

Kotlinコマンドラインコンパイラを使用して、KotlinソースコードをJavaScriptまたはJVMバイトコードにコンパイルすることもできます。

Kotlinの詳細については、次のリソースをご覧ください。

- コトリンウェブサイト：https://kotlinlang.org

- Kotlin Koans: https://kotlinlang.org/docs/tutorials/koans.html

- Kotlin標準ライブラリ文書：https://kotlinlang.org/api/latest/jvm/stdlib/

- Kotlinリファレンス：https://kotlinlang.org/docs/reference/

##結論

Kotlinは、JVMで実行され、JavaScriptでコンパイルできるプログラミング言語を使用するのに簡潔で安全で面白いです。