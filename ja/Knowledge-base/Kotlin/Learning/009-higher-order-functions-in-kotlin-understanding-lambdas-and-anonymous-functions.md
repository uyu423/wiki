---
title: 009: Kotlin の高階関数: ラムダと匿名関数を理解する
description: 
published: true
date: 2023-01-31T05:36:06.422Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:36:02.790Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [009: Higher-Order Functions in Kotlin: Understanding Lambdas and Anonymous Functions***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/009-higher-order-functions-in-kotlin-understanding-lambdas-and-anonymous-functions)
{.links-list}


#009：Kotlinの高次関数：ラムダと匿名関数の理解

コンピュータプログラミングでは、高次関数は、1つ以上の関数を引数（つまり手続き型パラメータ）として取り、その結果として新しい関数を返す関数です。

Kotlinでは、言語の豊富な組み込み関数のセットと関数が一流の市民であるという事実のために、高次関数は非常に一般的です。つまり、変数に格納され、他の関数に引数として渡される可能性があります。

Kotlinで最も一般的に使用される高次関数の1つは、オブジェクトで指定されたコードブロックを実行してからオブジェクト自体を返すために使用される「適用」関数です。たとえば、次のコードを考えてみましょう。

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

上記のコードでは、 `apply`関数は `list`オブジェクトで与えられたコードブロック（つまり中括弧の間のコード）を実行してから `list`オブジェクト自体を返すために使用されます。次に、 `also`関数を使用して `list`オブジェクトに対していくつかの追加操作を実行します（この場合はコンソールに印刷）。

高次関数について理解すべき重要な点の1つは、繰り返しのコードパターンを抽象化するために使用できることです。たとえば、次のコードを考えてみましょう。

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

上記のコードでは、 `apply`関数は `list`に新しい要素を追加してから `list`を返すために使用されます。この特定のコードパターンは非常に一般的であり、Kotlinは代わりに使用できる組み込みの `+=`演算子を提供します。

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list += 5
    list += listOf(6, 7, 8)

    println(list)
}
```

`+=`演算子は `apply`関数の略です。これは次のコードと同じです。

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }

    println(list)
}
```

ご覧のとおり、 `+=`演算子は、要素をリスト（または他の変更可能なコレクション）に追加する一般的なコードパターンを抽象化するために使用できます。

もう1つの一般的な高次関数は、オブジェクトで指定されたコードブロックを実行してからコード結果を返すために使用される `let`関数です。たとえば、次のコードを考えてみましょう。

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list.let {
        it.add(5)
        it.addAll(listOf(6, 7, 8))
        it
    }

    println(newList)
}
```

上記のコードでは、`let`関数は`list`オブジェクトから与えられたコードブロックを実行してから`list`オブジェクト自体を返すために使用されます。 `it`変数は、コードブロック内の `list`オブジェクトを参照するために使用されます。

'apply'関数と同様に、 'let'関数は繰り返しのコードパターンを抽象化するために使用できます。たとえば、次のコードを考えてみましょう。

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list.let {
        it.add(5)
        it.addAll(listOf(6, 7, 8))
        it
    }

    println(newList)
}
```

上記のコードでは、 `let`関数は `list`に新しい要素を追加してから `list`を返すために使用されます。この特定のコードパターンは非常に一般的であり、Kotlinは代わりに使用できる組み込みの `+=`演算子を提供します。

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list += 5
    val newList = list += listOf(6, 7, 8)

    println(newList)
}
```

`+=` 演算子は `let` 関数の速記に過ぎず、これは次のコードと同じであることを意味します。

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list.let {
        it.add(5)
        it.addAll(listOf(6, 7, 8))
        it
    }

    println(newList)
}
```

ご覧のとおり、 `+=`演算子は、要素をリスト（または他の変更可能なコレクション）に追加する一般的なコードパターンを抽象化するために使用できます。

最後に、高次関数は、しばしば名前のない匿名関数であるラムダで使用されることに言及する価値があります。ラムダは、コードブロックを高次関数に引数として渡すためによく使用されます。たとえば、次のコードを考えてみましょう。

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        this.add(5)
        this.addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

上記のコードでは、 `apply`関数は `list`オブジェクトから与えられたラムダを実行し、 `list`オブジェクト自体を返すために使用されます。次に、 `also`関数を使用して `list`オブジェクトに対していくつかの追加操作を実行します（この場合はコンソールに印刷）。

ご覧のとおり、ラムダは繰り返しのコードパターンを抽象化するために使用できます。たとえば、次のコードを考えてみましょう。

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

上記のコードでは、 `apply`関数は `list`に新しい要素を追加してから `list`を返すために使用されます。この特定のコードパターンは非常に一般的であり、Kotlinは代わりに使用できる組み込みの `+=`演算子を提供します。

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list += 5
    list += listOf(6, 7, 8)

    println(list)
}
```

`+=`演算子は `apply`関数の略です。これは次のコードと同じです。

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }

    println(list)
}
```

ご覧のとおり、 `+=`演算子は、要素をリスト（または他の変更可能なコレクション）に追加する一般的なコードパターンを抽象化するために使用できます。

キーポイント：
- 高次関数は、1つ以上の関数を引数として取り、その結果として新しい関数を返す関数です。
- Kotlinでは、言語の豊富な組み込み関数セットと関数が一流の市民であるという事実のため、高次元関数は非常に一般的です。
- Kotlinで最も一般的に使用される高次関数の1つは、オブジェクトで指定されたコードブロックを実行してからオブジェクト自体を返すために使用される `apply`関数です。
- もう一つの一般的な高次関数は、オブジェクトで与えられたコードブロックを実行してからコードの結果を返すために使用される `let`関数です。
- 高次関数は、多くの場合、名前のない匿名関数であるラムダと共に使用されます。