---
title: 074: Kotlin のプロキシ パターン: 別のオブジェクトのサロゲートまたはプレースホルダーを提供する
description: 
published: true
date: 2023-01-31T12:17:34.416Z
tags: 
editor: markdown
dateCreated: 2023-01-31T12:17:32.700Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [074: The Proxy Pattern in Kotlin: Providing a Surrogate or Placeholder for Another Object***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/074-the-proxy-pattern-in-kotlin-providing-a-surrogate-or-placeholder-for-another-object)
{.links-list}


  [リソース]セクションに元の文書へのリンクを追加します。

#074：Kotlinのプロキシパターン：他のオブジェクトにデリゲートまたはプレースホルダを与える

プロキシパターンは、サロゲートオブジェクトまたはプレースホルダオブジェクトを他のオブジェクトに提供するソフトウェアデザインパターンです。プロキシパターンでは、クラスは他のクラスの機能を表します。このタイプのデザインパターンは構造パターンに属します。

プロキシパターンには4種類あります。

- 仮想プロキシ：仮想プロキシは、他のオブジェクトを表すオブジェクトです。たとえば、実際のオブジェクトを表すアイコンです。
- リモートプロキシ：リモートプロキシは、異なるアドレス空間にあるオブジェクトのローカル代表を提供します。たとえば、Webサービスにアクセスします。
- 保護プロキシ：保護プロキシは重要なマスターオブジェクトへのアクセスを制御します。 「相互ゲート」オブジェクトは、実際のプリンシパルがアクセスされる前にアクセス可能であることを確認します。
- スマートプロキシ：スマートプロキシはプロキシに追加のロジックを追加します。たとえば、参照カウント。

この記事では、仮想プロキシパターンに焦点を当てます。

## 仮想プロキシパターンとは何ですか？

仮想プロキシは、他のオブジェクトを表すオブジェクトです。実際のオブジェクトは必要なときにのみ作成されます。たとえば、リモートサーバーからロードされているイメージです。画像はプロキシオブジェクトで表されます。プロキシオブジェクトはイメージに対する要求を処理します。イメージがロードされると、プロキシオブジェクトは実際のイメージオブジェクトに置き換えられます。

仮想プロキシを使用すると、次のことができます。

- 高価なオブジェクトの作成を遅らせてパフォーマンスを向上させます。
- オブジェクトの複雑さを隠します。
- まだ利用できないオブジェクトのプレースホルダを提供します。

## Kotlinで仮想プロキシパターンを実装する方法は？

次の例を使用して、仮想プロキシパターンをデモンストレーションします。ユーザーを表す User クラスがあります。 User クラスには名前とアバターがあります。アバターはイメージです。仮想プロキシを使用してアバターイメージを表します。

```kotlin
class User(val name: String, val avatar: Image)
```

Image クラスはイメージを表します。 Image クラスには幅と高さがあります。

```kotlin
class Image(val width: Int, val height: Int)
```

ImageProxy クラスは Image クラスのプロキシです。 ImageProxy クラスには Image クラスへの参照があります。 ImageProxy クラスにはロードフラグもあります。ロードフラグは、Imageクラスがロード中かどうかを追跡するために使用されます。

```kotlin
class ImageProxy(val image: Image) {
    val loading = false
}
```

loadImage() 関数は、Image クラスをロードするために使用されます。 loadImage() 関数はイメージ URL とコールバック関数を使用します。コールバック関数は、イメージがロードされると呼び出されます。

```kotlin
fun loadImage(imageUrl: String, callback: (Image) -> Unit) {
    // TODO: load image from URL
}
```

main() 関数は ImageProxy オブジェクトで User オブジェクトを生成します。 ImageProxy オブジェクトはアバター画像を表します。 loadImage() 関数は、アバターイメージをロードするために使用されます。イメージがロードされると、ImageProxyオブジェクトはImageオブジェクトに置き換えられます。

```kotlin
fun main() {
    val user = User("Alice", ImageProxy(null))

    loadImage("avatar.jpg") { image ->
        user.avatar = image
    }
}
```

## 仮想プロキシパターンはいつ使用しますか？

仮想プロキシパターンは、次の場合に使用する必要があります。

- オブジェクトの作成は高価です。
- オブジェクトは頻繁に使用されません。
- オブジェクトはすぐに使用できません。

## 仮想プロキシパターンの利点

仮想プロキシパターンには次の利点があります。

- 高価なオブジェクトの作成を遅らせ、パフォーマンスを向上させます。
- オブジェクトの複雑さを隠します。

## 仮想プロキシパターンの欠点

仮想プロキシパターンには、次の欠点があります。

- 複雑さを引き起こす可能性があります。

##リソース

- [ウィキペディア]（https://en.wikipedia.org/wiki/Proxy_pattern）
- [ソースメイキング](https://sourcemaking.com/design_patterns/proxy)