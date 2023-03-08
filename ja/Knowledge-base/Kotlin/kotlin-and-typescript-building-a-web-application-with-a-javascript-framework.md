---
title: Kotlin と TypeScript: JavaScript フレームワークを使用した Web アプリケーションの構築
description: 
published: true
date: 2023-02-17T18:16:45.973Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:36:33.209Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Kotlin and TypeScript: Building a Web Application with a JavaScript Framework***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-typescript-building-a-web-application-with-a-javascript-framework)
{.links-list}


KotlinとTypeScriptは、Webアプリケーションの構築に使用できる2つの広く使用されているプログラミング言語です。この記事では、KotlinとTypeScriptを使用してJavaScriptフレームワークでWebアプリケーションを構築する方法について説明します。

まず、KotlinとTypeScriptを一緒に使用することのいくつかの利点を見てみましょう。 Kotlinは、Java Virtual Machine（JVM）で実行される静的に型指定された言語です。安全性、相互運用性、ツールサポートで有名です。 TypeScript は、静的タイピングやその他の機能を追加する JavaScript の親セットです。ツールのサポートと拡張機能で有名です。

KotlinとTypeScriptを一緒に使用すると、両方の言語の利点を得ることができます。 Kotlinの安全とツールのサポートとTypeScriptの拡張機能を使用できます。

次に、KotlinとTypeScriptを使用してプロジェクトを設定する方法を見てみましょう。シンプルな「Hello、World！」 Webアプリケーション。

まず、プロジェクトディレクトリを作成する必要があります。コマンドラインまたはIDEを使用してこれを実行できます。

次に、プロジェクトディレクトリに「Hello.kt」というファイルを作成します。ファイルに次のコードを追加します。

```kotlin
fun main(args: Array<String>) {
    println("Hello, World!")
}
```

その後、コマンドラインを使用してKotlinコードをコンパイルできます。

```
kotlinc Hello.kt -d hello.js
```

これにより、プロジェクトディレクトリに「hello.js」というファイルが作成されます。

これで、プロジェクトディレクトリに「index.html」というファイルを作成できます。ファイルに次のコードを追加します。

```html
<!doctype html>
<html>

<head>
    <meta charset="utf-8">
    <title>Hello、World！</title>
</head>

<body>
    <script src="hello.js"></script>
</body>

</html>
```

最後に、ブラウザで「index.html」を開くことができ、「Hello、World！」と表示されます。メッセージ。

KotlinとTypeScriptを使用してプロジェクトを設定する方法を見てきたので、JavaScriptフレームワークでKotlinとTypeScriptを使用する方法を見てみましょう。私たちはReact JavaScriptフレームワークを使用します。

まず、ReactとReact-DOMをインストールする必要があります。コマンドラインを使用してこれを実行できます。

```
npm install react react-dom
```

次に、プロジェクトディレクトリに「Hello.tsx」というファイルを作成します。ファイルに次のコードを追加します。

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

ReactDOM.render(
    <h1>Hello、World！</h1>、
    document.getElementById("root")
）;
```

次に、コマンドラインを使用してTypeScriptコードをコンパイルします。

```
tsc --jsx react Hello.tsx
```

これにより、プロジェクトディレクトリに「Hello.js」というファイルが作成されます。

最後に、Reactコードを含むように "index.html"ファイルを更新する必要があります。ファイルに次のコードを追加します。

```html
<!doctype html>
<html>

<head>
    <meta charset="utf-8">
    <title>Hello、World！</title>
</head>

<body>
    <div id="root"></div>
    <script src="hello.js"></script>
</body>

</html>
```

その後、ブラウザで「index.html」を開くと、「Hello, World!」と表示されます。メッセージ。

KotlinとTypeScriptは、Webアプリケーションの構築に使用できる2つの広く使用されているプログラミング言語です。この記事では、KotlinとTypeScriptを使用してJavaScriptフレームワークでWebアプリケーションを構築する方法について説明しました。