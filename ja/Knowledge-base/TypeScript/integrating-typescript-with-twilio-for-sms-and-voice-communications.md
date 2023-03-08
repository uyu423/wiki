---
title: TypeScript と Twilio を統合して SMS および音声通信を行う
description: 
published: true
date: 2023-02-17T18:07:51.832Z
tags: 
editor: markdown
dateCreated: 2023-01-30T16:17:27.612Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Integrating TypeScript with Twilio for SMS and Voice Communications***English** version of this document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-twilio-for-sms-and-voice-communications)
{.links-list}


# SMSと音声通信のためにTypeScriptをTwilioと統合

開発者は、アプリケーションにSMSまたは音声機能を追加する必要がある状況に直面する可能性があります。たとえば、ユーザーが会社のカスタマーサービス番号にSMSメッセージを送信できるように、Webサイトに「お問い合わせ」フォームを追加する必要があります。または、ユーザーがWebまたはモバイルアプリから電話をかける機能を追加する必要があるかもしれません。

Twilioは、アプリケーションに音声とSMS機能を追加できるクラウドコミュニケーションプラットフォームです。この記事では、TypeScriptプログラミング言語を使用してTwilioをWebまたはモバイルアプリと統合する方法について説明します。

##タイプスクリプトとは何ですか？

TypeScriptは、Microsoftが開発および保守する無料のオープンソースプログラミング言語です。すべての JavaScript コードが有効な TypeScript コードであることを意味する JavaScript の親セットです。

TypeScriptは、大規模なアプリケーションをより簡単に開発できるようにJavaScriptに機能を追加します。たとえば、TypeScriptは、変数と関数に型情報を追加できる型コメントをサポートしています。これにより、開発プロセスの初期にバグを発見できます。

##タイプスクリプトのインストール

TypeScriptをインストールするには、コンピュータにNode.jsとnpmがインストールされている必要があります。 Node.jsは、ブラウザの外部でJavaScriptコードを実行できるJavaScriptランタイムです。 npmは、TypeScriptやその他のJavaScriptライブラリをインストールできるNode.js用のパッケージマネージャです。

Node.jsとnpmがインストールされたら、次のコマンドを使用してTypeScriptをインストールできます。

```
npm install -g typescript
```

## TypeScriptプロジェクトの設定

TypeScriptがインストールされたら、次のコマンドを実行してTypeScriptプロジェクトを設定できます。

```
tsc --init
```

これにより、プロジェクトディレクトリに `tsconfig.json`というファイルが作成されます。このファイルには、プロジェクトの TypeScript 構成が含まれています。

デフォルトでは、TypeScriptコンパイラは最新のJavaScript標準（ES6）と互換性のあるJavaScriptコードを生成します。以前のバージョンのJavaScriptと互換性のあるコードを生成する必要がある場合は、 `tsconfig.json`で `target`コンパイラオプションを設定できます。たとえば、ES5規格と互換性のあるコードを生成するには、 `target`オプションを ```es5 ''に設定します。

## TypeScriptコードのコンパイル

TypeScriptプロジェクトが設定されたら、次のコマンドを使用してTypeScriptコードをJavaScriptにコンパイルできます。

```
tsc
```

これにより、プロジェクトのすべてのTypeScriptコードがJavaScriptにコンパイルされます。出力JavaScriptファイルは `out`ディレクトリに配置されます。

次のコマンドを実行して特定のTypeScriptファイルをコンパイルすることもできます。

```
tsc file.ts
```

## TwilioとTypeScriptの統合

TypeScriptの基本を見てきたので、TypeScriptを使用してTwilio APIを使用してSMSまたは音声機能をアプリに追加する方法を見てみましょう。

### SMSメッセージを送信

TypeScriptを使用してSMSメッセージを送信するには、Twilioアカウントを設定してTwilio電話番号を購入する必要があります。 Twilioアカウントと電話番号がある場合は、次のTypeScriptコードを使用してSMSメッセージを送信できます。

```typescript
import * as twilio from "twilio";

const accountSid="your-twilio-account-sid";
const authToken = "your-twilio-auth-token";
const client = twilio（accountSid、authToken）;

client.messages
  .create({
     body: "Hello, world!",
     from: "your-twilio-phone-number",
     to: "your-phone-number"
   }）
  .then（message => console.log（message.sid））;
```

上記のコードで `import`キーワードを使用してTwilioライブラリをインポートしました。次に、アカウントの資格情報を使用して新しい「Twilio」クライアントを設定します。最後に、 `client.messages.create`メソッドを使用してSMSメッセージを送信しました。

### 電話をかける

TypeScriptを使用して電話をかけるには、Twilioアカウントを設定してTwilio電話番号を購入する必要があります。 Twilioアカウントと電話番号がある場合は、次のTypeScriptコードを使用して電話をかけることができます。

```typescript
import * as twilio from "twilio";

const accountSid="your-twilio-account-sid";
const authToken = "your-twilio-auth-token";
const client = twilio（accountSid、authToken）;

client.calls
  .create({
     url: "your-twiML-url",
     to: "your-phone-number",
     from: "your-twilio-phone-number"
   }）
  .then（call => console.log（call.sid））;
```

上記のコードで `import`キーワードを使用してTwilioライブラリをインポートしました。次に、アカウントの資格情報を使用して新しい「Twilio」クライアントを設定します。最後に、 `client.calls.create`メソッドを使って電話をかけました。

##結論

この記事では、TypeScriptを使用してTwilio APIを使用してWebまたはモバイルアプリにSMSおよび音声機能を追加する方法について説明しました。また、TypeScriptのインストール方法やTypeScriptプロジェクトの設定方法など、TypeScriptの基本についても説明しました。