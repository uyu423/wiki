---
title: Web Assembly
description: 
published: true
date: 2023-02-12T04:56:23.632Z
tags: 
editor: markdown
dateCreated: 2023-02-12T04:56:15.919Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}



- [Web Assembly***English** document is available*](/en/Knowledge-base/Dictionary/web-assembly)
{.links-list}


# 概要

Web Assembly (WASM) は、スタックベースの仮想マシン用の新しいバイナリ命令形式です。これは、移植可能で、サイズ効率とロード時間効率に優れたプログラミング言語のコンパイル ターゲットになるように設計されており、クライアント アプリケーションとサーバー アプリケーションの Web 上での展開を可能にします。

# 説明

Web Assembly (WASM) は、C、C++、Rust などのプログラミング言語のコンパイル ターゲットとして設計された低レベルのアセンブリに似た言語です。これは、サイズ、ロード時間、および実行時間の点で効率的になるように設計されたバイナリ命令形式です。 WASM は、高水準言語をコンパイルするためのポータブル ターゲットになるように設計されており、クライアント側とサーバー側の両方のアプリケーションで Web 上に展開できます。

WASM は安全なサンドボックス実行環境として設計されており、ユーザーのセキュリティを損なうことなくコードを Web 上で実行できます。また、JavaScript よりも効率的なコードを Web 上で実行する方法も提供するため、パフォーマンスが向上し、読み込み時間が短縮されます。

WASM コードは事前 (AOT) でバイナリ形式にコンパイルされ、仮想マシンによって読み込まれて実行されます。この仮想マシンは、Web ブラウザーに組み込むことも、スタンドアロン アプリケーションとして実装することもできます。

# 歴史

Web Assembly は、新しい Web プラットフォームを作成する取り組みの一環として、World Wide Web Consortium (W3C) によって 2015 年に最初に発表されました。この言語の最初のバージョンは 2017 年にリリースされ、それ以来、いくつかの更新が行われています。

# 特徴

WASM は、Web アプリケーションの魅力的なコンパイル ターゲットとなる多くの機能を提供します。

- サイズ、ロード時間、および実行時間の点で効率的になるように設計された、アセンブリに似た低レベルの言語です。
- 安全でサンドボックス化された実行環境であり、ユーザーのセキュリティを損なうことなくコードを Web 上で実行できます。
- JavaScript よりも効率的な Web 上でコードを実行する方法を提供し、パフォーマンスの向上と読み込み時間の短縮を可能にします。
- 高水準言語をコンパイルするためのポータブル ターゲットとして設計されているため、クライアント側とサーバー側の両方のアプリケーションで Web 上に展開できます。

# 例

以下は、C で記述され、WASM にコンパイルされた単純なプログラムの例です。

```C
#include <stdio.h>

int main() {
  printf("Hello, World!\n");
  return 0;
}
```

このプログラムは、Emscripten などのツールを使用して WASM にコンパイルできます。

```
emcc hello.c -o hello.wasm
```

これにより WASM バイナリが生成され、WASM 仮想マシンでロードして実行できます。

# 長所と短所

WASM には、他の Web テクノロジよりも多くの利点があります。

- 安全でサンドボックス化された実行環境であり、ユーザーのセキュリティを損なうことなくコードを Web 上で実行できます。
- JavaScript よりも効率的な Web 上でコードを実行する方法を提供し、パフォーマンスの向上と読み込み時間の短縮を可能にします。
- 高水準言語をコンパイルするためのポータブル ターゲットとして設計されているため、クライアント側とサーバー側の両方のアプリケーションで Web 上に展開できます。

ただし、WASM の使用にはいくつかの欠点もあります。

- 比較的新しい技術であり、まだ開発中であるため、バグや互換性の問題がある可能性があります。
- 他の Web テクノロジほど広くサポートされていないため、すべてのブラウザがサポートしているわけではありません。
- 他の Web テクノロジほどデバッグが容易ではないため、問題のトラブルシューティングが難しい場合があります。

# 関連技術

WASM は、JavaScript や WebGL などの他の Web テクノロジに関連しています。 JavaScript は動的 Web ページの作成に使用されるスクリプト言語であり、WebGL は Web ブラウザーでハードウェア アクセラレーションによる 3D グラフィックを可能にするグラフィック API です。

# 余談

WASM は、Web アプリケーションの開発方法に革命を起こす可能性を秘めたエキサイティングな新技術です。 JavaScript よりも効率的な Web 上でコードを実行する方法を提供し、パフォーマンスの向上と読み込み時間の短縮を可能にします。また、安全なサンドボックス実行環境になるように設計されているため、ユーザーのセキュリティを損なうことなくコードを Web 上で実行できます。