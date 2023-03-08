---
title: 066: Kotlin のプロトタイプ パターン: 既存のオブジェクトから新しいオブジェクトを作成する
description: 
published: true
date: 2023-01-31T10:17:35.759Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:17:32.304Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [066: The Prototype Pattern in Kotlin: Creating New Objects from Existing Ones***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/066-the-prototype-pattern-in-kotlin-creating-new-objects-from-existing-ones)
{.links-list}


  066：Kotlinのプロトタイプパターン：既存のオブジェクトから新しいオブジェクトを作成する

プロトタイプパターンは、作成するオブジェクトの種類が新しいオブジェクトを作成するために複製されるプロトタイプインスタンスによって決定されるときにソフトウェア開発で使用される生成デザインパターンです。このパターンは次に使用されます。

- 最初から新しいオブジェクトを作成するオーバーヘッドを避け、
- オブジェクトの生成を管理するために「ファクトリ」オブジェクトは必要ありません。
- オブジェクトを組み立てるために「ビルダー」オブジェクトは必要ありません。

プロトタイプパターンはファクトリメソッドと抽象ファクトリパターンの代替であり、しばしば一緒に使用されます。

プロトタイプパターンの主な利点は、生成するオブジェクトの正確なタイプを指定することなく、新しいオブジェクトを作成できることです。これは、作成するオブジェクトの種類が事前にわからない場合や、最初から新しいオブジェクトを作成するコストが膨大な場合に役立ちます。

プロトタイプパターンの主な欠点は、プロトタイプに対するすべての変更がすべてのクローンに伝播されるため、プロトタイプを維持および更新するのが難しいことです。

プロトタイプパターンを使用する場合

プロトタイプパターンは、次の場合に使用する必要があります。

- 作成するオブジェクトの種類を事前に不明、
- 最初から新しいオブジェクトを作成する費用は膨大です。
- 生成するオブジェクトの数が多い。

プロトタイプパターンの実装方法

プロトタイプパターンは、次の手順を使用してKotlinで実装できます。

1. プロトタイプを表すクラスを作成します。このクラスには、プロトタイプのコピーを返す clone() メソッドが必要です。

2. プロトタイプクラスを拡張する具体的なクラスを作成します。

3. プロトタイプをインスタンス化し、複製する main() メソッドを作成します。

4.プロトタイプで新しいオブジェクトを作成し、レプリカであることを確認してプロトタイプパターンをテストします。

以下はKotlinのプロトタイプパターンの例です。

```kotlin
// The Prototype クラス

abstract class Prototype {

abstract fun clone(): Prototype

}

// The Concrete Prototype classes

class ConcretePrototypeA: Prototype {

override fun clone(): Prototype {

return ConcretePrototypeA()

}

}

class ConcretePrototypeB: Prototype {

override fun clone(): Prototype {

return ConcretePrototypeB()

}

}

// The main() メソッド

fun main(args: Array<String>) {

val prototypeA = ConcretePrototypeA()

val prototypeB = ConcretePrototypeB()

// Clone the prototypes

val cloneA = prototypeA.clone()

val cloneB = prototypeB.clone()

// Verify that the prototypes have been cloned

println("cloneA is a clone of prototypeA: ${cloneA === prototypeA}")

println("cloneB is a clone of prototypeB: ${cloneB === prototypeB}")

}
```

この例では、Prototypeクラスは抽象クラスであり、特定のクラスによって実装されるclone（）メソッドを定義します。 Concrete Prototypeクラスは、オブジェクトのコピーを返すためにclone（）メソッドをオーバーライドするPrototypeクラスの特定のサブクラスです。

main() メソッドは、ConcretePrototypeA と ConcretePrototypeB の 2 つのプロトタイプをインスタンス化して複製します。次に、レプリカがソースのコピーであることを確認します。

プログラムの出力は次のとおりです。

```
cloneA is a clone of prototypeA: false

cloneB is a clone of prototypeB: false
```

出力が示すように、レプリカはプロトタイプと同じオブジェクトではなく、プロトタイプのコピーです。

プロトタイプパターンを使用する場合

プロトタイプパターンは、次の場合に使用する必要があります。

- 作成するオブジェクトの種類を事前に不明、
- 最初から新しいオブジェクトを作成する費用は膨大です。
- 生成するオブジェクトの数が多い。

プロトタイプパターンの主な利点は、生成するオブジェクトの正確なタイプを指定することなく、新しいオブジェクトを作成できることです。これは、作成するオブジェクトの種類が事前にわからない場合や、最初から新しいオブジェクトを作成するコストが膨大な場合に役立ちます。

プロトタイプパターンの主な欠点は、プロトタイプに対するすべての変更がすべてのクローンに伝播されるため、プロトタイプを維持および更新するのが難しいことです。

外部リンク

- Wikipediaのプロトタイプパターン（https://en.wikipedia.org/wiki/Prototype_pattern）

- Javaのプロトタイプデザインパターン（https://www.geeksforgeeks.org/prototype-design-pattern/）

- Pythonのプロトタイプデザインパターン（https://fkhadra.github.io/2017/02/01/python-prototype/）