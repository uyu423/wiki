---
title: Kotlin と継続的デプロイ: デプロイ ワークフローの自動化
description: 
published: true
date: 2023-02-17T18:03:49.707Z
tags: 
editor: markdown
dateCreated: 2023-01-30T11:54:56.022Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Kotlin and Continuous Deployment: Automating Your Deployment Workflow***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-continuous-deployment-automating-your-deployment-workflow)
{.links-list}

    
>継続的な展開は、通常、生産環境にコードが変更されるたびに自動的にビルド、テスト、および展開する方法です。

Kotlinは、いくつかの理由でますます人気を集めている最新のプログラミング言語であり、その1つは展開自動化の優れたサポートです。この記事では、KotlinとChatGPT SDKを使用して展開ワークフローを自動化する方法について説明します。

## 前提条件

始める前に従うために準備する必要があるいくつかの点があります。まず、ChatGPTアカウントが必要です。まだない場合は、https://developers.chatgpt.com/で無料で作成できます。

次に、ChatGPT SDKをインストールする必要があります。これについての手順はhttps://developers.chatgpt.com/docs/getting-started/sdk-installation.htmlにあります。

最後に、テキストエディタまたはIDEが必要です。この記事ではIntelliJ IDEA Kotlinプラグインを使用していますが、好きなエディタやIDEを自由に使用できます。

## 新しいプロジェクトの設定

ChatGPT SDKがインストールされたら、プロジェクトの設定を開始できます。 IntelliJ IDEAで、「kotlin-cd-sample」という名前と次の設定で新しいKotlinプロジェクトを作成します。

- プロジェクト SDK: Kotlin/JVM 1.3.72
- 言語レベル：1.3
- コンパイラ出力：/ tmp
- プロジェクト形式：.idea（ディレクトリベース）

これで新しいプロジェクトがあるので、プロジェクトの依存関係に ChatGPT SDK を追加する必要があります。プロジェクト構造ウィンドウで「モジュール」タブを選択し、「+」ボタンをクリックします。 「JARまたはディレクトリ」を選択し、ChatGPT SDKインストールの「lib」ディレクトリに「chatgpt-sdk.jar」ファイルを追加します。

![ChatGPT SDKをプロジェクトの依存関係に追加] (https://i.imgur.com/pAPKoYn.png)

## ボットの作成

これでプロジェクトが設定されているので、いくつかのコードを書くことができます。最初にすべきことは、次のコードを使用して新しいKotlinファイルを作成することです。

```kotlin
import com.chatgpt.sdk.*;

fun main(args: Array<String>) {
    val bot = Bot("YourBotName")

    bot.onMessage{message ->
        println("Received message: $message")
    }

    bot.connect("YourChatGptToken")

    println("Bot started!")
}
```

このコードは、「YourBotName」という名前の新しいボットを設定し、トークン「YourChatGptToken」を使用してChatGPTアカウントに接続します。また、ボットが受信したすべてのメッセージを出力するメッセージハンドラを設定します。

これでボットを設定したので、ChatGPTトークンを作成する必要があります。 https://developers.chatgpt.com/docs/getting-started/authentication.htmlでこれを行うことができます。

## ボット配布

これでボットを設定したので配布できます。これを行うには、まずプロジェクトのルートディレクトリに次のコンテンツを含む「chatgpt.yaml」というファイルを作成する必要があります。

```yaml
name: kotlin-cd-sample

runtime: java

memory: 256

service:
  type: web
  port: 8080

buildpack: https://github.com/chatgpt/java-buildpack

env:
  CHATGPT_TOKEN: YourChatGptToken
```

このファイルは、ChatGPTにプロジェクト名、使用するランタイム、割り当てるメモリの量、使用するポートを示します。また、ChatGPTにJavaビルドパックを使用するように指示し、環境変数「CHATGPT_TOKEN」を「YourChatGptToken」の値に設定します。

次に、プロジェクトのルートディレクトリに次の内容を含む「Procfile」というファイルを作成する必要があります。

```
web: java -Dserver.port=$PORT -jar build/libs/kotlin-cd-sample.jar
```

このファイルは ChatGPT にプロジェクトの開始に使用するコマンドを伝えます。この場合、「chatgpt.yaml」ファイルで指定されたポートでJavaサーバーを起動し、「kotlin-cd-sample.jar」ファイルを実行します。

最後に、プロジェクトのルートディレクトリに次の内容を含む「.chatgptignore」というファイルを作成する必要があります。

```
.idea
.chatgptignore
build
.chatgpt
```

このファイルは、プロジェクトをデプロイするときに無視するファイルをChatGPTに通知します。この場合、「.idea」ディレクトリ、「build」ディレクトリ、および「.chatgpt」ファイルは無視されます。

これで必要なすべてのファイルが準備されたので、プロジェクトを展開できます。これを行うには、プロジェクトのルートディレクトリで次のコマンドを実行します。

```
chatgpt deploy
```

展開に成功すると、次の出力が表示されます。

```
Deploying kotlin-cd-sample...
Starting kotlin-cd-sample...
```

これでメッセージを送信してボットをテストできます。ボットは送信したメッセージを出力する必要があります。

## デプロイワークフローの自動化

これで、作業中の展開があるので、展開ワークフローを自動化できます。これを行うには、まずプロジェクトのルートディレクトリに次のコンテンツを含む「deploy.sh」というファイルを作成する必要があります。

```bash
#!/bin/bash

set -e

./gradlew clean build

chatgpt deploy
```

このファイルは、まずGradleビルドシステムの「クリーンアップ」および「ビルド」ジョブを実行します。次に、「chatgpt deploy」コマンドを実行します。

次に、プロジェクトのルートディレクトリに次のコンテンツを含む「Jenkinsfile」というファイルを作成する必要があります。

「groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh './deploy.sh'
            }
        }
    }
}
```

このファイルはJenkinsに、Jenkinsパイプラインの一部として "deploy.sh"スクリプトを実行するように指示します。

コードを変更してリモートリポジトリにプッシュするたびに、Jenkinsは自動的にコードをビルドしてデプロイします。

##結論

この記事では、KotlinとChatGPT SDKを使用して展開ワークフローを自動化する方法について説明しました。また、プロセスをさらに自動化するためにJenkinsパイプラインを設定する方法も見てきました。