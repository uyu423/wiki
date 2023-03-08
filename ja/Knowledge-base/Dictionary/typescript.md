---
title: TypeScript
description: 
published: true
date: 2023-02-01T00:57:37.569Z
tags: 
editor: markdown
dateCreated: 2023-02-01T00:57:35.962Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [TypeScript***English** version of this document is available*](/en/Knowledge-base/Dictionary/typescript)
{.links-list}


#Overview
TypeScriptは、Microsoftが開発および保守するオープンソースのプログラミング言語です。 JavaScript の親セットです。つまり、すべての有効なJavaScriptコードは有効なTypeScriptコードでもあります。 TypeScriptは、オプションの静的型付けとクラスベースのオブジェクト指向プログラミングを言語に追加します。大規模なアプリケーション開発用に設計されており、JavaScriptにトランスコンパイルされています。

#History
TypeScriptは2012年10月に初めてリリースされました。 TypeScript は、大規模なアプリケーションに適した型付き JavaScript 親セットを提供するために Microsoft によって開発されました。 TypeScriptは以来、最も人気のあるプログラミング言語の1つになり、Microsoft、Google、Facebookを含む多くの大企業で使用されています。

#description
TypeScript は、通常の JavaScript でコンパイルされる型付き JavaScript 親セットです。オプションの静的型付けとクラスベースのオブジェクト指向プログラミングを言語に追加します。大規模なアプリケーション開発用に設計されており、JavaScriptにトランスコンパイルされています。 TypeScript コンパイラ自体は TypeScript で記述され、JavaScript でコンパイルされます。

#特徴
TypeScriptには、大規模なアプリケーション開発に魅力的な言語になる多くの機能があります。開発者がランタイムではなくコンパイル時にエラーをキャッチできるようにするオプションの静的型指定があります。さらに、クラス、インタフェース、モジュールがあるため、開発者はより体系的にコードを整理できます。 TypeScriptは、開発者がさまざまな種類のデータで作業できるコードを書くことを可能にするジェネリックもサポートしています。

#yes
以下は、「Hello World!」を印刷する単純なTypeScriptプログラムの例です。コンソールへ：

```typescript
クラス Greeter {
  greeting: string;
  コンストラクタ(message: string) {
    this.greeting = message;
  }
  greet() {
    return "Hello," + this.greeting;
  }
}

let greeter = new Greeter("world");

console.log(greeter.greet());
```

#長所と短所
TypeScriptには通常のJavaScriptよりも多くの利点があります。開発者がランタイムではなくコンパイル時にエラーをキャッチできるようにするオプションの静的型指定があります。さらに、クラス、インタフェース、モジュールがあるため、開発者はより体系的にコードを整理できます。 TypeScriptは、開発者がさまざまな種類のデータで作業できるコードを書くことを可能にするジェネリックもサポートしています。

しかし、TypeScriptにはいくつかの欠点もあります。通常のJavaScriptよりも複雑なので、学ぶのは難しいかもしれません。また、時間がかかる可能性があるビルドプロセスが必要です。最後に、通常のJavaScriptほど広く使用されていないため、学習とデバッグに使用できるリソースが少なくなる可能性があります。

#関連技術
TypeScriptは型付き言語の親セットであるため、JavaScriptに関連しています。また、クラスやインタフェースなどの同様の機能があるため、C#やJavaなどの他のフォーマット言語にも関連しています。

#余談
TypeScriptは、Microsoftが開発および保守するオープンソースのプログラミング言語です。 JavaScript の書式設定された親セットです。つまり、すべての有効なJavaScriptコードは有効なTypeScriptコードでもあります。 TypeScriptは、オプションの静的型付けとクラスベースのオブジェクト指向プログラミングを言語に追加します。大規模なアプリケーション開発用に設計されており、JavaScriptにトランスコンパイルされています。