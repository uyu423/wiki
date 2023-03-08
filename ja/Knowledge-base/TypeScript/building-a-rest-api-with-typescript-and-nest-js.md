---
title: TypeScript と Nest.js を使用して REST API を構築する
description: 
published: true
date: 2023-02-17T18:12:54.690Z
tags: 
editor: markdown
dateCreated: 2023-01-30T19:44:00.612Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Building a REST API with TypeScript and Nest.js***English** version of this document is available*](/en/Knowledge-base/TypeScript/building-a-rest-api-with-typescript-and-nest-js)
{.links-list}


#TypeScriptとNest.jsでREST APIを構築する

Nest.jsは、TypeScriptとJavaScript（ES6、7、8）の上に効率的でスケーラブルなエンタープライズクラスのサーバーサイドアプリケーションを構築するためのNode.jsフレームワークです。

##なぜNest.jsを使用するのですか？

REST APIを構築するためにNest.jsを使用したい理由はたくさんあります。

Nest.jsはTypeScriptに基づいているため、静的型チェックを含むTypeScriptのすべての利点を活用できます。これは動的に型指定されたJavaScriptとは対照的です。

また、Nest.jsはJavaScript Expressフレームワークを利用しています。 Expressは、Node.jsのための迅速で独特ではないミニマリストのWebフレームワークです。 Expressを使用することで、Nest.jsは利用可能な多数のExpressプラグインとミドルウェアを利用できます。

Nest.jsも非常にモジュラーです。 Nest.jsアーキテクチャは、共通ルート名アーキテクチャ（CRN）に基づいています。このアーキテクチャでは、Nest.js の各モジュールを互いに独立して使用できます。

## TypeScriptを使用する利点

Nest.jsはTypeScriptに基づいているため、TypeScriptのすべての機能を利用できます。 TypeScript は、オプションの静的型をコードに追加する JavaScript の親セットです。

JavaScriptよりもTypeScriptを使用すると、次の利点があります。

- TypeScriptはJavaScriptの親セットです。つまり、有効なすべてのJavaScriptコードは有効なTypeScriptコードでもあります。これにより、JavaScript開発者はTypeScriptを簡単に起動できます。

- TypeScriptコードはJavaScriptでコンパイルされるため、すべてのJavaScript環境で実行されます。これにより、サーバーまたはWebブラウザにTypeScriptコードを簡単にデプロイできます。

- TypeScriptは静的に入力されます。これは、TypeScriptコンパイラが実行される前にコードのエラーを確認できることを意味します。これは、エラーがコードに導入されるのを防ぐのに役立ちます。

- TypeScriptコンパイラは、以前のバージョンのJavaScriptと互換性のあるJavaScriptコードを生成できます。これを特定のJavaScriptバージョンを「ターゲティング」することが知られています。これは、古いブラウザまたはサーバーをサポートする必要がある場合に便利です。

- TypeScriptには独自の型定義ファイルが付属しています。このファイルを使用して、コードで予想される値の種類に関するTypeScript情報を提供できます。これは、JavaScriptで書かれたサードパーティのライブラリを使用する場合に特に便利です。

## TypeScriptとNest.jsのインストール

TypeScriptとNest.jsを使用するにはインストールが必要です。 TypeScriptコンパイラは、npmパッケージマネージャを使用してインストールできます。

```
npm install -g typescript
```

Nest.jsフレームワークはnpmパッケージマネージャを使用してインストールできます。

```
npm install -g @nestjs/cli
```

## Nest.jsでTypeScriptを使用する

Nest.js は TypeScript をプログラミング言語として使用します。つまり、Nest.jsアプリケーションを開発するときにTypeScriptを使用する必要があります。

TypeScriptはJavaScriptの親セットです。つまり、すべての有効なJavaScriptコードは有効なTypeScriptコードでもあります。 TypeScriptはオプションの静的型をコードに追加します。

JavaScriptよりもTypeScriptを使用すると、次の利点があります。

- TypeScriptは静的に入力されます。これは、TypeScriptコンパイラが実行される前にコードのエラーを確認できることを意味します。これは、エラーがコードに導入されるのを防ぐのに役立ちます。

- TypeScriptコンパイラは、以前のバージョンのJavaScriptと互換性のあるJavaScriptコードを生成できます。これを特定のJavaScriptバージョンを「ターゲティング」することが知られています。これは、古いブラウザまたはサーバーをサポートする必要がある場合に便利です。

- TypeScriptには独自の型定義ファイルが付属しています。このファイルを使用して、コードで予想される値の種類に関するTypeScript情報を提供できます。これは、JavaScriptで書かれたサードパーティのライブラリを使用する場合に特に便利です。

Nest.jsはコードベース全体でTypeScript言語を使用します。つまり、Nest.jsを効果的に使用するには、TypeScriptに精通している必要があります。

TypeScriptに慣れていない場合は、TypeScript WebサイトでTypeScriptチュートリアルを確認できます。

## Nest.jsアプリケーションの作成

TypeScriptとNest.jsがインストールされているので、Nest.jsアプリケーションを作成できるようになりました。

Nest.js CLIを使用して新しいNest.jsアプリケーションを作成できます。

```
nest new my-api
```

これにより、「my-api」というディレクトリに新しいNest.jsアプリケーションが作成されます。

## パス定義

ルートは Nest.js ルータで定義されます。ルータは、アプリケーションのパスを定義するために使用されるモジュールです。

パスはパスとハンドラ関数で定義されます。パスは、着信要求のURLを一致させるために使用される文字列です。ハンドラ機能は、着信要求を処理し、応答を生成するために使用されます。

Nest.jsでは、パスは「app.routing.ts」です。

「タイプスクリプト」
import {ModuleWithProviders、RouterModule、Routes} from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

constパス：パス= [
  {パス： '/'、コントローラ：AppController、メソッド： 'get'}、
];

エクスポート const AppRoutingModule: ModuleWithProviders = RouterModule.forRoot(ルート);
```

Code above、a route is defined for the path ```/ ''。このルートはURL ```/ ```'と一致し、``AppController ''にハンドルを要求します。

「AppController」はNest.js controllerです。 Controllers are responsible for handling requests and generating responses.

「タイプスクリプト」
import {Controller、Get} from '@nestjs/common';
import { AppService } from './app.service';

@制御装置()
エクスポートクラス AppController {
  コンストラクタ (プライベート読み取り専用 appService: AppService) {}

  @取得()
  getHello(): 文字列 {
    this.appService.getHello() を返します。
  }
}
```

コードを追加すると、「AppController」がアノテートされています。「@Controller」 This decorator tells Nest.js that this class is a controller.

「AppController」はシングルルートハンドラーです。 This handler is annotated with the ```@Get '' decorator。 This decorator tells Nest.js that this handler will process GET requests.

``````getHello（） '' ` handler is a simple handler that returns the string "Hello World!"。

## Defining Services

Services are used to encapsulate business logic in Nest.js applications. Services are injected into controllers and are used to process requests and generate responses.

Services are defined in the file「app.service.ts」

「タイプスクリプト」
「@nestjs / common」から{注入可能}をインポートする。

@注射用（）
エクスポートクラス AppService {
  getHello(): 文字列 {
    「Hello World!」を返します。
  }
}
```

コードを追加すると、「AppService」がアノテートされています。 This decorator tells Nest.js that this class is a service.

「AppService」は単一のメソッド、「getHello（）」です。 This method returns the string "Hello World!".

## Injecting Services

Services are injected into controllers using the ```@Inject() '' decorator.

「タイプスクリプト」
import {Controller、Get、Inject} from '@nestjs/common';
import { AppService } from './app.service';

@制御装置()
エクスポートクラス AppController {
  建設者（
    @Inject（「アプリ_サービス」）
    プライベート読み取り専用 appService: AppService,
  ){}

  @取得()
  getHello(): 文字列 {
    this.appService.getHello() を返します。
  }
}
```

コードを追加すると、「AppService」が入力されています。「AppController」は「@Inject（）」デコレータです。 ```@Inject（） ''デコレータはサービストークンをパラメータにします。 The service token is used to identify the service that is being injected.

The ```@Inject（） ''は、デコレータを使用してインジェクトサービスを使用することができます。

## Running the Application

The Nest.js CLI can be used to run the application.

```
巣の始まり
```

これにより、ポート3000でNest.jsアプリケーションが起動します。