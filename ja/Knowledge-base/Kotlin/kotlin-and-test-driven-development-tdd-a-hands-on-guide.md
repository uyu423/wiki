---
title: Kotlin とテスト駆動開発 (TDD): ハンズオン ガイド
description: 
published: true
date: 2023-02-17T18:08:47.831Z
tags: 
editor: markdown
dateCreated: 2023-01-30T16:57:19.002Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Kotlin and Test Driven Development (TDD): A Hands-on Guide***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-test-driven-development-tdd-a-hands-on-guide)
{.links-list}


# Kotlinとテスト主導開発（TDD）：実践ガイド

Kotlinは、JVM、Android、JavaScript、およびNativeを対象とした静的型プログラミング言語です。 Apache 2.0ライセンスに基づくオープンソースプロジェクトです。 Kotlinはまた、高次関数を持つ関数型プログラミング言語です。開発者は、既存のすべてのJavaライブラリとフレームワークでKotlinを使用できます。

##テスト主導開発（TDD）とは何ですか？

テスト主導の開発は、コードを書く前にテストを最初に書く必要があるという開発方法論です。この目的は、コードがテストで指定した要件を満たしていることを確認することです。この方法論はまた、コードをより強力でリファクタリングしやすくするためのものです。

## TDDでKotlinを使用するのはなぜですか？

Kotlinは非常に簡潔な言語なので、全体的に少ないコードを生成できます。コードが多ければ多いほど、すべての機能のテストを書くのに時間がかかるので、これはテストの作成に重要です。また、Kotlinにはnull安全機能が組み込まれており、nullポインタの例外を防ぐのに役立ちます。これはテストにとって特に重要です。ヌルポインタがあるとテストが失敗するからです。

## TDD用Kotlinプロジェクトの設定

IDE用のKotlinプラグインをすでにインストールしているとし、新しいKotlinプロジェクトを作成します。プロンプトが表示されたら、プロジェクトテンプレートとして「Java」を選択します。このガイドでは、Gradleビルドシステムを使用します。

##最初のKotlinテスト

これでプロジェクトが設定されたので、最初のテストを書いてみましょう。まず、 `MyFirstTest.kt`という名前の `src/test/kotlin`ディレクトリにファイルを作成します。このファイルでは、Kotlinの `sum`関数が期待どおりに機能していることを確認するテストを作成します。

```kotlin
import org.junit.Assert.*
import org.junit.Test

class MyFirstTest {
    @Test
    fun testSum() {
        assertEquals(4, sum(2, 2))
    }
}
```

ここでは、テストの作成に使用する `junit`ライブラリをインポートしました。単一の `testSum` メソッドを含む `MyFirstTest` クラスも作成しました。このメソッドは `assertEquals` 関数を使って `2` 引数と `2` 引数で `sum` を呼び出した結果が `4` と同じであることを確認します。

このテストを実行するには、 `MyFirstTest.kt`ファイルを右クリックして「実行」を選択します。テストの実行を確認して合格する必要があります。

## コードを書く

失敗したテストがあるため、テストに合格するようにコードを書くことができます。 `MyFirst.kt` という `src/main/kotlin` ディレクトリにファイルを作成します。このファイルから `sum` 関数を作成します。

```kotlin
fun sum(a: Int, b: Int): Int {
    return a+b
}
```

今度はテストをやり直す必要があります。

##結論

この記事では、TDD用のKotlinプロジェクトを設定する方法と、それに合格するための最初のテストとコードを書く方法について説明しました。 TDDは、コードが正確でリファクタリングしやすいことを確認するための良い方法です。 Kotlinの簡潔な構文と組み込まれたnull安全機能は、KotlinをTDDにとって理想的な言語にします。