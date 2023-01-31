---
title: Java でロンボクを使用する
description: 
published: true
date: 2023-01-31T09:02:30.179Z
tags: 
editor: markdown
dateCreated: 2023-01-31T09:02:30.179Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Using Lombok in Java***English** version of this document is available*](/en/Knowledge-base/Java/using-lombok-in-java)
{.links-list}


Lombokは、Javaで定型句コードを減らすために使用されるオープンソースライブラリです。 Java開発者の間で非常に人気があります。 Lombok は、Java コードの生成および保守プロセスを自動化するために使用されます。作成する必要があるコードの量を減らし、コードを読みやすくします。 Lombokは、eclipseやnetbeansなど、さまざまなIDEのプラグインとして使用できます。

Lombok は、getter、setter、toString、equals、hashCode メソッドなど、さまざまな Java 構成の定型句コードを生成するために使用されます。 Lombok はビルダークラスの生成にも使用されます。 Lombok はコメントベースで、すべてのコメントはパッケージ lombok で使用できます。

Lombokで使用される有名なコメントのいくつかは次のとおりです。

@Getterと@Setter：このコメントは、Javaクラスのフィールドのgetterおよびsetterメソッドを生成するために使用されます。

@ToString：このコメントは、JavaクラスのtoString（）メソッドを生成するために使用されます。

@EqualsAndHashCode：この注釈は、javaクラスのequals（）およびhashCode（）メソッドを生成するために使用されます。

@NoArgsConstructor、@RequiredArgsConstructor、および@AllArgsConstructor：これらのコメントは、Javaクラスのコンストラクタを生成するために使用されます。

@Data：この注釈は、Javaクラスに対して上記のすべてのメソッドを生成するために使用されます。

@Builder：このコメントはビルダークラスを作成するために使用されます。

ロンボクは非常に使いやすいです。必要なコメントをjavaクラスに追加するだけで、Lombokライブラリは必要なコードを生成します。

Lombokは、作成する必要がある定型句コードの量を減らすため、Java開発者の間で非常に人気があります。また、コードを読みやすくします。 Lombokは非常に使いやすく、さまざまなIDE用のプラグインとして使用できます。