---
title: AWS SQS: クラウドでの分散タスク キュー システムの構築
description: 
published: true
date: 2023-02-17T18:16:31.131Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:05:23.344Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [AWS SQS: Building a Distributed Task Queue System in the Cloud***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-sqs-building-a-distributed-task-queue-system-in-the-cloud)
{.links-list}


#AWS SQS：クラウドに分散ジョブキューシステムを構築する

この記事では、Amazon Simple Queue Service（SQS）を使用して分散ジョブキューシステムを構築する方法について説明します。次のトピックを扱います。

- ジョブキューとは何ですか？
- ジョブキューを使用する理由は何ですか？
- Amazon SQSとは何ですか？
- Amazon SQSを始めよう
- Amazon SQSで分散ジョブキューを構築する

## タスクキューとは？

タスクキューは、タスクを管理および処理するためのシステムです。タスクは、電子メールの送信、画像処理、またはデータのクリーンアップなど、実行する必要があるすべてのタスクにすることができます。

ジョブキューは、ジョブを非同期的に処理するために使用されます。これは、ジョブがキューに追加され、後でワーカーによって処理されることを意味します。これは、ジョブが直ちに処理される同期処理とは異なります。

ジョブキューには次の利点があります。

- デフォルトのアプリケーションをブロックせずにバックグラウンドでタスクを処理するために使用できます。
- 複数のワーカーを使用してジョブを並列に処理するために使用できます。
- 複数のコンピュータにタスクを展開するために使用できます。

## ジョブキューを使用するのはなぜですか？

ジョブキューを使用する理由はたくさんあります。ここに例があります：

- メインアプリケーションをブロックせずにバックグラウンドでタスクを処理したい。
- 複数のワーカーを使用してジョブを並列に処理する場合。
- 複数のコンピュータにタスクを展開しようとしています。

ジョブキューはさまざまなジョブに使用できます。たとえば、ジョブキューを使用して次のことを実行できます。

- メールを送信
- プロセスイメージ
- データの整理
- レポート生成

## Amazon SQSとは何ですか？

Amazon Simple Queue Service（SQS）はマネージドメッセージキューサービスです。分散ジョブキューシステムの構築に使用できます。

SQS は、信頼性が高くスケーラブルで低コストのメッセージキューサービスです。標準および先入れ先出し（FIFO）キューの両方をサポートします。

## Amazon SQSを始めよう

SQSを使用する前に、Amazon SQSキューを作成する必要があります。これは、AWSマネジメントコンソール、AWSコマンドラインインターフェイス（CLI）、またはAWS SDKを使用して実行できます。

キューを作成したら、キューへのメッセージの追加を開始できます。 AWSマネジメントコンソール、AWS CLI、またはAWS SDKを使用してメッセージを追加できます。

キューにメッセージを追加すると、ワーカーはメッセージを処理できます。ワーカーは、AWSマネジメントコンソール、AWS CLI、またはAWS SDKを使用して作成できます。

## Amazon SQSによる分散ジョブキューの構築

このセクションでは、Amazon SQS を使用して分散ジョブキューシステムを構築する方法について説明します。次のコンポーネントを使用します。

- Amazon SQS
- Amazon Elastic Compute Cloud（EC2）
- Amazonシンプル通知サービス（SNS）

また、次のオープンソースソフトウェアを使用します。

- Apache ActiveMQ
- Apacheラクダ

### Amazon SQSキューの作成

最初のステップは、Amazon SQSキューを作成することです。これは、AWSマネジメントコンソール、AWS CLI、またはAWS SDKを使用して実行できます。

キューが作成されたら、構成する必要があります。次の構成設定が必要です。

- メッセージ保持期間：メッセージが削除されるまでキューに残っている時間。最小値は4秒、最大値は14日です。

- 配信遅延：メッセージがワーカーに配信される前にキューに残っている時間。最小値は0秒、最大値は15分です。

- 受信ハンドル：キューからメッセージを削除するために使用されるトークン。

- Visibility timeout：メッセージが他のワーカーに表示される前にキューに残っている時間。最小値は0秒、最大値は12時間です。

### Amazon EC2 インスタンスの作成

次のステップは、Amazon EC2インスタンスを作成することです。これは、AWSマネジメントコンソール、AWS CLI、またはAWS SDKを使用して実行できます。

インスタンスが作成されたら、構成する必要があります。次の構成設定が必要です。

- セキュリティグループ：ポート22（SSH）とポート8080（HTTP）でインバウンドトラフィックを許可するセキュリティグループを作成する必要があります。

- 鍵ペア：鍵ペアを作成し、秘密鍵を安全な場所に保存する必要があります。

- IAMロール：EC2インスタンスがSQSにアクセスできるようにするIAMロールを作成する必要があります。

### Apache ActiveMQのインストールと構成

次のステップは、Apache ActiveMQをインストールして構成することです。 Apache ActiveMQはオープンソースのメッセージブローカーです。

まず、Apache ActiveMQをダウンロードする必要があります。これは、次のコマンドを使用して実行できます。

```
wget http://www.apache.org/dyn/closer.cgi?filename=/activemq/5.15.8/apache-activemq-5.15.8-bin.tar.gz&action=download
```

Next, you need to extract the downloaded file. This can be done using the following command:

```
tar -xzf apache-activemq-5.15.8-bin.tar.gz
```

次に、ActiveMQディレクトリに変更する必要があります。これは、次のコマンドを使用して実行できます。

```
cd apache-activemq-5.15.8/
```

次に、ActiveMQ構成ファイルを編集する必要があります。お気に入りのテキストエディタを使用してこれを行うことができます。たとえば、次のコマンドを使用できます。

```
nano conf/activemq.xml
```

ActiveMQ 構成ファイルはよく文書化されています。マニュアルを読み、次のように変更します。

- ```<broker> '' element、set the ```persistent = "true" '' attribute。

- In the ``<transportConnectors> '' element、add the following ``<transportConnector> '' element：

```xml
<transportConnector name="sqs" uri="sqs://ACCESS_KEY_ID:SECRET_ACCESS_KEY@sqs.us-east-1.amazonaws.com:9324?queuePrefix=act" />
```

- In the ``<destinations> '' element、add the following ``<queue>```element：

```xml
<キューの物理名="TASK_QUEUE_NAME" />
```

Replace ```TASK_QUEUE_NAME '' with the name of the Amazon SQS queue that you created earlier.

- In the ``<systemUsage> '' element、set the ```storeUsage> ''、および ```tempUsage> ''

```xml
<storeUsage limit="20GB"/>
<tempUsage制限="10GB"/>
```

This will ensure that the ActiveMQ broker does not run out of storage space.

- In the ``<plugins> '' element、add the following ```<statisticsBrokerPlugin> '' element：

```xml
<statisticsBrokerPlugin/>
```

This will enable ActiveMQ broker statistics.

- Save your changes and exit the text editor.

### Starting Apache ActiveMQ

The next step is to start the Apache ActiveMQ broker. This can be done using the following command:

```
空/activemqを起動
```

You can check that the broker is running by executing the following command:

```
空/activemqステータス
```

You should see the following output:

```
ACTIVEMQ_HOME: /home/ec2-user/apache-activemq-5.15.8
ACTIVEMQ_DATA: /home/ec2-user/apache-activemq-5.15.8/data
ブローカーのURLに接続しています。sqs://ACCESS_KEY_ID:SECRET_ACCESS_KEY@sqs.us-east-1.amazonaws.com:9324?queuePrefix=act
含める: queue://TASK_QUEUE_NAME
ログ：Apache ActiveMQ 5.15.8（localhost、ID：ip-10-0-1-32.ec2.internal-39767-1588389434974-0:1）が起動中です。
戻る
情報：ヘルプまたは詳細については、http://activemq.apache.orgを参照してください。
情報: http://0.0.0.0:8161/ で使用できる ActiveMQ WebConsole
情報：Springアプリケーションのコンテキストを閉じています。
情報: Apache ActiveMQ 5.15.8(localhost, ID:ip-10-0-1-32.ec2.internal-39767-1588389434974-0:1) 稼働時間
37.528秒
情報: Apache ActiveMQ 5.15.8(localhost, ID:ip-10-0-1-32.ec2.internal-39767-1588389434974-0:1)は
終了
```

If the broker is not running, you can start it using the following command:

```
空/activemqを起動
```

### Installing and configuring Apache Camel

The next step is to install and configure Apache Camel. Apache Camel is an open-source integration framework.

First, you need to download Apache Camel. This can be done using the following command:

```
wget http://www.apache.org/dyn/closer.cgi?filename=/camel/2.23.1/apache-camel-2.23.1.tar.gz&action=download
```

次に、ダウンロードしたファイルを抽出する必要があります。これは、次のコマンドを使用して実行できます。

```
tar -xzf Apache ラクダ-2.23.1.tar.gz
```

Next, you need to change into the Camel directory. This can be done using the following command:

```
cd Apache-ラクダ-2.23.1/
```

Next, you need to create a configuration file. This can be done using your favorite text editor. For example, you could use the following command:

```
ナノconf/camel.xml
```

Add the following content to the file:

```xml
<豆xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:スキーマの場所="
  http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
  http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">
 
  <camelContext id="ラクダ" xmlns="http://camel.apache.org/schema/spring">
    <路線>
      <from uri="sqs://ACCESS_KEY_ID:SECRET_ACCESS_KEY@sqs.us-east-1.amazonaws.com:9324?queuePrefix=act&amp;delay=5000&concurrentConsumers=5&maxMessagesPerPoll=10"/>
      <to uri="activemq:TASK_QUEUE_NAME"/>
    </パス>
  </camelContext>
</豆>
```

Replace「ACCESS_KEY_ID」と「SECRET_ACCESS_KEY」とのAmazon SQSアクセスキーIDとシークレットアクセスキー。 Replace ```TASK_QUEUE_NAME '' with the name of the Amazon SQS queue that you created earlier.

- Save your changes and exit the text editor.

### Running Apache Camel

The next step is to start Apache Camel. This can be done using the following command:

```
空/ラクダ
```

You can check that Apache Camel is running by executing the following command:

```
空/ラクダの状態
```

You should see the following output:

```
 ラクダは走りません。
```

If Apache Camel is not running, you can start it using the following command:

```
空/ラクダ開始
```

### Sending messages to the queue

The next step is to send messages to the Amazon SQS queue. This can be done using the AWS Management Console, AWS CLI, or AWS SDK.

Messages can be any JSON-formatted data. The following is an example message:

```json
{
  "作業": "send_email",
  "に": "john@example.com",
  "from": "noreply@example.com",
  「タイトル」：「こんにちはジョン」、
  "body": "こんにちはジョン、\n\nジョブキューから送信されたメッセージです。"
}
```

### Processing messages

Messages in the Amazon SQS queue can be processed by workers. Workers can be created using the AWS Management Console, AWS CLI, or AWS SDK.

Workers can be any type of program, such as a web application, a command-line program, or a script. The following is an example worker written in PHP:

```php
<?php

//メッセージが受信されたことを確認します。
if (!empty($_GET['message'])) {
  // メッセージをデコードします。
  $message = json_decode($_GET['メッセージ']);
 
  // メッセージを処理します。
  スイッチ ($message->task) {
    ケース 'send_email':
      // メールを送信します。
      mail($message->to, $message->タイトル, $message->body, '送信者: ' . $message->from);
      壊れる。
 
    ケース 'process_image':
      //画像を処理します。
      // ...
      壊れる。
 
    ケース 'cleanup_data':
      //データを整理します。
      // ...
      壊れる。
 
    ケース 'generate_report':
      // レポートを生成します。
      // ...
      壊れる。
  }
}
```

##結論

この記事では、Amazon Simple Queue Service（SQS）を使用して分散ジョブキューシステムを構築する方法について説明しました。私たちは次のトピックを扱いました。

- ジョブキューとは何ですか？
- ジョブキューを使用する理由は何ですか？
- Amazon SQSとは何ですか？
- Amazon SQSを始めよう
- Amazon SQSで分散ジョブキューを構築する

ご質問があれば、いつでもコメントに投稿してください。