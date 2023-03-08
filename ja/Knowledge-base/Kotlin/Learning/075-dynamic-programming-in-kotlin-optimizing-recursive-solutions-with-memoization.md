---
title: 075: Kotlin での動的プログラミング: メモ化による再帰的ソリューションの最適化
description: 
published: true
date: 2023-01-31T18:04:34.408Z
tags: 
editor: markdown
dateCreated: 2023-01-31T18:04:32.808Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [075: Dynamic Programming in Kotlin: Optimizing Recursive Solutions with Memoization***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/075-dynamic-programming-in-kotlin-optimizing-recursive-solutions-with-memoization)
{.links-list}



#075：Kotlinの動的プログラミング：メモ化による再帰ソリューションの最適化

動的プログラミングは、複雑な問題をより小さく、単純なサブ問題に分解して解決する強力な技術です。サブ問題の結果を再計算するのではなく、再利用できるように保存して再帰ソリューションを最適化するために使用できます。

この記事では、動的プログラミングを使用してKotlinで再帰ソリューションを最適化する方法を学びます。技術を説明するために、簡単な例から始めて、より複雑な問題に適用します。

## 簡単な例

n番目のフィボナッチ数を計算したいとします。次のコードを使用して再帰的にこれを実行できます。

```kotlin
fun fib(n: Int): Int {
    if(n<=1) return n
    return fib(n - 1) + fib(n - 2)
}
```

ただし、このコードはサブ問題の結果を再計算するため、非常に非効率的です。たとえば、 `fib(5)` を計算するときに `fib(4)` と `fib(3)` を 2 回計算します。

![フィボナッチ計算](fibonacci.png)

動的プログラミングを使用してサブ問題の結果を再利用できるように保存することで、このコードを最適化できます。すでに計算されているフィボナッチ数を追跡するために、配列を使用してこれを実行できます。

```kotlin
fun fib(n: Int): Int {
    if(n<=1) return n
    val fibs = IntArray(n + 1)
    fibs[0] = 0
    fibs[1] = 1
    for(i in 2..n) {
        fibs[i] = fibs[i - 1] + fibs[i - 2]
    }
    return fibs[n]
}
```

これで `fib(5)` を計算する際に `fib(4)` と `fib(3)` の結果を再利用できるようになりました。

![メモ化を使ったフィボナッチ計算](fibonacci-memoized.png)

このコードは、サブ問題の結果を再計算する必要がないため、はるかに効率的です。

## もう少し複雑な例

それでは、より複雑な問題であるバックパックの問題に動的プログラミングを適用しましょう。バックパックの問題では、我々はそれぞれ重量と価値を持つ一連のアイテムを受け取りました。私たちの目標は、与えられた重量制限を維持しながら、合計値を最大化する項目のサブセットを選択することです。

たとえば、次の項目があるとします。

|アイテム|重量|価値
| --- | --- | --- |
| A | 2 | 6 |
|雨2 | 10 |
|氏| 3 | 12 |

そして、総重みが5以下で、総価値を最大化する項目のサブセットを探してみたいと思います。この場合の最適な解決策は、合計重みが5で合計値が18の項目AとCを選択することです。

動的プログラミングを使用して、バックパックの問題を解決できます。配列を使用して、重量制限までの各重量に対して達成できる最大値を追跡します。

```kotlin
fun knapsack(items: Array<Item>, weightLimit: Int): Int {
    val values = IntArray(weightLimit + 1)
    for(i in items.indices) {
        val item = items[i]
        for(w in weightLimit downTo item.weight) {
            values[w] = max(values[w], values[w - item.weight] + item.value)
        }
    }
    return values[weightLimit]
}
```

このコードで `values[w]` は `w` 以下の重みで得られる最大値を示します。各項目を順番に考慮し、バックパックに追加する価値があることを確認してこの値を計算します。その場合はそれに応じて `values[w]` を更新します。

たとえば、重みが 2 で値が 6 の項目 A を考慮しているとします。 `values[2]` を 6 (項目 A の値) に更新し、 `values[3]` を 8 (項目 A の値 + 重み 1) で得ることができる最高の値です。

![バックパック計算](knapsack.png)

すべての項目を考慮するまでこのプロセスを続けます。最後に `values[weightLimit]` には `weightLimit` 以下の重みで達成できる最大値が含まれます。

##結論

この記事では、動的プログラミングを使用してKotlinで再帰ソリューションを最適化する方法を学びました。私たちは、メモを使用してサブ問題の結果を保存して再利用できるようにする方法を見て、このテクニックをバックパックの問題に適用しました。