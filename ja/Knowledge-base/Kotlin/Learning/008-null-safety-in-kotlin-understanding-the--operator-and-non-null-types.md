---
title: 008: Kotlin の Null 安全性: ? を理解する演算子と非 null 型
description: 
published: true
date: 2023-01-31T05:24:38.876Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:24:37.195Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [008: Null Safety in Kotlin: Understanding the ? Operator and Non-Null Types***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/008-null-safety-in-kotlin-understanding-the--operator-and-non-null-types)
{.links-list}




# KotlinのNullの安全: か。理解する演算子と非NULL型

KotlinはJVM上で動作する静的型プログラミング言語です。 Javaと完全に相互運用可能であり、Android開発のためのJavaの代替としてよく使用されます。 Null安全はKotlinの主な機能の1つです。 Javaプログラムでエラーの主な原因となる可能性があるNULLポインタ例外のリスクを排除します。

Kotlinでは、すべての変数はnullを受け入れるか、nullではないと宣言する必要があります。 NULL入力可能変数はNULL値を保持できますが、NULL以外の変数は保持できません。これはコンパイル時に適用されるため、null以外の変数にnull値を割り当てることはできません。

Kotlinのnull安全性を理解する鍵は？オペレーター。この演算子は、変数をnullableとしてマークするために使用されます。たとえば、次の変数はnullまたはnull以外の値を保持できます。

```kotlin
var str：String？ = "Hello、world!"
```

nullable 変数の型は、? を追加して表示されます。型名の後ろ。上記の例では、変数の型はString?です。

最初にnullであることを確認せずにnullable変数にアクセスしようとすると、コンパイル時エラーが発生します。たとえば、次のコードはコンパイルされません。

```kotlin
fun main(args: Array<String>) {
    var str：String？ = "Hello、world!"
    println(str.length)
}
```

コンパイラはstrがnullである可能性があることを知っているので、それに対してlengthプロパティを呼び出すことはできません。この問題を解決するには、アクセスする前にstrがnullであることを確認する必要があります。

```kotlin
fun main(args: Array<String>) {
    var str：String？ = "Hello、world!"
    if(str!=null){
        println(str.length)
    }
}
```

または？ nullable 変数に安全にアクセスする演算子です。変数にアクセスする前に、変数がnullであることを確認してください。 null の場合、式全体が null と評価されます。たとえば、

```kotlin
fun main(args: Array<String>) {
    var str：String？ = "Hello、world!"
    println(str?.length)
}
```

上記のコードでは、str?.length式は、strがnullの場合はnullと評価されます。それ以外の場合は、文字列の長さとして評価されます。

? を使用することも可能です。変数がnullの場合に使用するデフォルト値を指定する演算子。たとえば、

```kotlin
fun main(args: Array<String>) {
    var str：String？ = "Hello、world!"
    println(str?.length ?: 0)
}
```

上記のコードでstrがnullの場合、式は0と評価されます。それ以外の場合は、文字列の長さとして評価されます。

null 型で null 以外の型を作成すると便利なことがよくあります。これは!!を使って行うことができます。オペレーター。この演算子は、null 型を null 以外の型に変換します。ただし、null 型が実際に null の場合、例外が発生します。たとえば、

```kotlin
fun main(args: Array<String>) {
    var str：String？ = "Hello、world!"
    println(str!!.length)
}
```

上記のコードでstrがnullの場合、例外が発生します。それ以外の場合は、文字列の長さが印刷されます。

? を使用することも可能です。演算子!!オペレーター。まず、null 変数が null であることを確認します。 null の場合は null を返します。それ以外の場合は、null 変数を null 以外の型に変換して返します。たとえば、

```kotlin
fun main(args: Array<String>) {
    var str：String？ = "Hello、world!"
    println(str?.length ?: 0)
}
```

上記のコードでstrがnullの場合、式はnullと評価されます。それ以外の場合は、文字列の長さとして評価されます。

Null セーフは、null ポインターの例外を防ぐのに役立つ Kotlin の重要な機能です。 ？を慎重に使用することで、演算子を使用するとコードをより強力にし、このタイプのエラーを回避できます。