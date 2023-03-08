---
title: Kotlin と Flask: シンプルな Web アプリケーションの構築
description: 
published: true
date: 2023-02-01T05:36:31.950Z
tags: 
editor: markdown
dateCreated: 2023-02-01T05:36:30.345Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Kotlin and Flask: Building a Simple Web Application***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-flask-building-a-simple-web-application)
{.links-list}



#KotlinとFlask：シンプルなWebアプリケーションの構築

KotlinはJVMで実行される静的に型指定されたプログラミング言語であり、JavaScriptまたはネイティブコードでコンパイルできます。関数型プログラミングとオブジェクト指向プログラミングの機能を組み合わせた実用的なオープンソース言語です。

Flaskは、小さなコアと拡張しやすい哲学で構築されたPython Webフレームワークです。 Flaskは軽い特性のため、マイクロサービスの構築に広く使用されています。

この記事では、KotlinとFlaskを使用して単純なWebアプリケーションを構築する方法を学びます。まず開発環境を設定し、KotlinクラスとFlaskパスを作成して簡単なメッセージを表示します。

##開発環境設定

コーディングを開始する前に開発環境を設定する必要があります。 KotlinコンパイラとFlask Webフレームワークをインストールする必要があります。

### Kotlinコンパイラのインストール

Kotlin コンパイラは [公式 Kotlin Web サイト] (https://kotlinlang.org/) からインストールできます。 Windows、macOS、LinuxにKotlinをインストールする手順があります。

###フラスコの取り付け

Flaskは[pip]（https://pip.pypa.io/en/stable/）パッケージマネージャを使用して[Python Package Index]（https://pypi.org/）からインストールできます。

```
$ pip install flask
```

## こんにちは、コトリン

これで開発環境が設定されているので、Kotlinコードを書いてみましょう。 「Hello.kt」というKotlinファイルを作成することから始めましょう。

```kotlin
fun main(args: Array<String>) {
    println("Hello, Kotlin!")
}
```

`kotlinc`コンパイラを使用して、このKotlinコードをJavaScriptにコンパイルできます。

```
$kotlinc Hello.kt -output hello.js
```

`kotlinc-native`コンパイラを使ってネイティブコードにコンパイルすることもできます。

```
$kotlinc-native Hello.kt -o hello
```

## こんにちは、フラスコ

ここでKotlinファイルがあるので、簡単なメッセージを表示するFlaskパスを作成しましょう。 `app.py`というファイルを作成し、`Flask`クラスを取得します。

```python
from flask import Flask
```

次に、`Flask`クラスのインスタンスを作成します。アプリケーションの名前を渡す必要があります。

```python
app = Flask(__name__)
```

これでパスを作成できます。パスは `@app.route` デコレータで装飾された関数です。 `@app.route`デコレータはパスを引数として使用します。関数に関連付けるパスです。

```python
@app.route('/')
def index():
    return 'Hello, Flask!'
```

最後に、Flaskにアプリケーションを実行するように指示する必要があります。私たちは `run` メソッドを呼び出してこれを行います。

```python
if __name__ == '__main__':
    app.run()
```

Flask コマンドを使用して Flask アプリケーションを実行できます。

```
$flask run
 *サービングフラスコアプリ「アプリ」
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

これでhttp://127.0.0.1:5000/からアプリケーションにアクセスできます。

##結論

この記事では、KotlinとFlaskを使用して単純なWebアプリケーションを構築する方法について説明しました。開発環境の設定から始めて、KotlinファイルとFlaskパスを作成して簡単なメッセージを表示しました。