---
title: バックエンド開発のための Kotlin 入門
description: 
published: true
date: 2023-01-31T06:23:17.685Z
tags: 
editor: markdown
dateCreated: 2023-01-31T06:23:16.142Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Getting Started with Kotlin for Backend Development***English** version of this document is available*](/en/Knowledge-base/Backend/getting-started-with-kotlin-for-backend-development)
{.links-list}


#バックエンド開発のためのKotlinを始めよう

Kotlinは、JVM、Android、JavaScript、およびNativeを対象とした静的型プログラミング言語です。 JetBrainsによって開発されました。 KotlinはJavaと完全に相互運用できるように設計されており、JVMバージョンは任意のJavaコードを実行できます。 KotlinはApache 2オープンソースライセンスとしてリリースされました。

JetBrainsによると、Kotlinプロジェクトの60％以上がバックエンド開発にこの言語を使用しています。その理由はさまざまです。 Kotlinは簡潔で安全でNull-Pointer-Proof™で、優れたツールサポートを提供します。また、Javaと100％相互運用可能なので、Kotlinコードで既存のすべてのJavaライブラリを使用できます。

この記事では、バックエンド開発のためにKotlinを起動する方法を見ていきます。 Kotlinプロジェクトを設定し、Kotlinでコードを書いて、JVMで実行する方法を見てみましょう。

## Kotlinプロジェクトの設定

Kotlinプロジェクトを設定する方法はいくつかあります。この記事では、Gradleビルドツールを使用します。 Gradleは、ビルドの自動化と複数の言語サポートに焦点を当てたビルドツールです。 Kotlinプロジェクトは、Gradle Kotlin DSLを使用して簡単に作成できます。

最初にすべきことは、プロジェクトのルートに `build.gradle.kts`というファイルを作成することです。このファイルには Kotlin プロジェクトの構成が含まれています。

```kotlin
plugins {
    id("org.jetbrains.kotlin.jvm") version "1.3.72"
}

group="com.example"
version="1.0-SNAPSHOT"

repositories {
    jcenter()
}

dependencies {
    implementation("org.jetbrains.kotlin:kotlin-stdlib-jdk8")
}

tasks.withType<Test> {
    useJUnitPlatform()
}
```

`build.gradle.kts`ファイルでKotlinプラグインを設定し、Kotlin stdlibへの依存関係を追加しました。また、JUnitプラットフォームを使用するように `test`タスクを設定しました。

## Kotlinコードを書く

これでKotlinプロジェクトが設定されたので、Kotlinコードを書くことができます。まず `src/` ディレクトリに `Main.kt` というファイルを生成します。

Main.kt`から「Hello、world！」を出力する簡単なKotlinプログラムを書いてください。コンソールに。

```kotlin
fun main() {
    println("Hello, world!")
}
```

Kotlinプログラムは `main`関数で始まります。 `main`関数はプログラムのエントリポイントです。 `main` 関数に「Hello, world!」という文字列を出力しました。コンソールに。

## Kotlinコードの実行

Kotlinコードは、追加の設定なしでJVMで実行できます。 Kotlinプログラムを実行するには、 `gradle run`コマンドを使用できます。これでKotlinコードがコンパイルされ、 `main`関数が実行されます。

```
$gradle run

> Task：run
Hello, world!

BUILD SUCCESSFUL in 0s
2 actionable tasks: 2 executed
```

##結論

この記事では、バックエンド開発のためにKotlinを起動する方法について説明しました。 Kotlinプロジェクトを設定し、Kotlinコードを書いてJVMで実行しました。 Kotlinはバックエンド開発のための優れた言語であり、私たちはKotlinができることのほんの一部に過ぎません。