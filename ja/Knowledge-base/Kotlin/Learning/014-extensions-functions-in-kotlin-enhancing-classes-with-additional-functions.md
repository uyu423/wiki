---
title: 014: Kotlin の拡張機能: 追加機能によるクラスの拡張
description: 
published: true
date: 2023-01-31T16:57:24.945Z
tags: 
editor: markdown
dateCreated: 2023-01-31T16:57:23.406Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [014: Extensions Functions in Kotlin: Enhancing Classes with Additional Functions***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/014-extensions-functions-in-kotlin-enhancing-classes-with-additional-functions)
{.links-list}



#14：Kotlinの拡張機能：アドオンでクラスを強化

Kotlinは、JVM、Android、およびブラウザ用の静的型プログラミング言語です。相互運用性、安全性、ツールサポート、簡潔な構文で有名です。

Kotlinの最も強力な機能の1つは拡張機能です。拡張関数は、既存のクラスから継承されずに追加される関数です。つまり、クラス自体を変更しなくても、既存のクラスに新しい機能を追加できます。

この記事では、拡張機能の作成方法と既存のクラスの拡張に使用できる方法について説明します。

## 拡張機能の作成

拡張機能を作成するのは簡単です。関数名の前に拡張したいクラス名を付けてからピリオドを取るだけです。たとえば、 `string` クラスに `print()` メソッドを追加する拡張関数を作成するには、次のようにします。

```kotlin
fun String.print() {
    println(this)
}
```

これで、すべての文字列で `print()` メソッドを呼び出すことができます。

```kotlin
"Hello, world!".print() // prints "Hello, world!"
```

ご覧のとおり、拡張関数は既存のクラスに新しい機能を追加する良い方法です。

## 拡張機能の使用

拡張関数は、制御できないクラスに新しいメソッドを追加したい場合に特に便利です。たとえば、 `User` クラスを持つライブラリを使用していますが、ここに `getFullName()` メソッドを追加したいとします。拡張機能を使用すると、 `User`クラス自体を変更することなくこれを行うことができます。

まず `User` クラスを定義しましょう。

```kotlin
class User(val firstName: String, val lastName: String)
```

これで、`User`クラスに`getFullName（）`メソッドを追加する拡張関数を作成できるようになりました。

```kotlin
fun User.getFullName(): String {
    return "$firstName $lastName"
}
```

これで `User` オブジェクトを作成し、ここで `getFullName()` メソッドを呼び出すことができます。

```kotlin
val user = User("John", "Smith")
println(user.getFullName()) // プリント "John Smith"
```

ご覧のとおり、拡張機能は、クラス自体を変更せずに既存のクラスに新しいメソッドを追加するのに最適な方法です。

##結論

この記事では、Kotlinの拡張機能について説明しました。拡張関数を作成する方法と、拡張関数を使用して既存のクラスに新しいメソッドを追加する方法について説明しました。