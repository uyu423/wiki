---
title: リアルタイム処理のために Kafka と Spring Boot を統合する
description: 
published: true
date: 2023-02-17T18:04:55.493Z
tags: 
editor: markdown
dateCreated: 2023-01-30T13:32:55.921Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Integrating Kafka with Spring Boot for Real-time Processing***English** version of this document is available*](/en/Knowledge-base/Backend/integrating-kafka-with-spring-boot-for-real-time-processing)
{.links-list}




#リアルタイム処理のためのKafkaとSpring Bootの統合

この記事を読んでいる場合は、データストリーミングの概念とプロセスに関連するさまざまなツールとテクノロジについてよく知っているはずです。この記事では、特定のストリーミングデータツールであるApache Kafkaに焦点を当てます。リアルタイム処理のためにKafkaをSpring Bootと統合する方法を示します。始める前に、いくつかの基本を見てみましょう。

データストリーミングは、ソースからターゲットにデータレコードを継続的に転送するプロセスです。データレコードはリアルタイムで生成され、任意のサイズまたは形式にすることができます。ソースは、単純なログファイルから複雑なイベント処理システムに至るまで、何でも構いません。ターゲットは、データウェアハウス、NoSQLデータベース、または単純なファイルシステムです。データストリーミングの主な利点は、処理を開始する前にすべてのデータが収集されるのを待たずに、データが到着したときに処理できることです。

Kafkaはデータストリーミングのための人気のオープンソースツールです。もともとLinkedInによって開発され、後でApache Software Foundationに寄付されました。 KafkaはJavaとScalaで書かれています。 3つの主な機能を提供するパブリケーション - 購読メッセージングシステム。

- **持続性:** Kafkaメッセージはディスクに保持され、クラスタ内で複製されます。
- **低レイテンシ：** Kafkaは非常に短いレイテンシで到着するメッセージを処理できます。
- **拡張性:** Kafkaは水平拡張が可能です。つまり、クラスターにさらにブローカーを追加して、スループットを増やすことができます。

KafkaはJavaエコシステムとの完全な統合を提供するので、Spring Bootとうまく機能します。 Spring Bootは、スタンドアロンのプロダクションクラスSpringベースのアプリケーションを簡単に作成できる人気のあるJavaフレームワークです。 Spring Bootは、自動構成や組み込みサーバーなどのデータストリーミングアプリケーションに役立ついくつかの機能を提供します。

この記事では、KafkaとSpring Bootを使用して簡単なメッセージプロデューサとコンシューマアプリケーションを構築する方法を説明します。また、メッセージベースのマイクロサービスを構築するためのライブラリであるSpring Cloud Streamの使用方法も紹介します。


##カフカ設定

アプリケーション開発を開始する前に、Kafkaブローカーを設定する必要があります。 KafkaブローカーはKafkaシステムの中核です。トピックのリストを維持し、生産者からのメッセージを受け入れて複製することを担当します。 [ここからダウンロード]（https://kafka.apache.org/downloads?view=release-2.4.0）できるApache Kafkaバージョン2.4.0を使用してください。

Kafkaバイナリをダウンロードしたら、目的の場所に解凍します。この資料では、Kafka バイナリが次の場所に解凍されていると仮定します。

```
/kafka_2.12-2.4.0
```

これで、次のコマンドを実行してKafkaブローカーを起動できます。

```
bin/zookeeper-server-start.sh config/zookeeper.properties
bin/kafka-server-start.sh config/server.properties
```

これでZooKeeperサーバーとKafkaブローカーが起動します。デフォルトでは、Kafkaブローカーはポート9092でリッスンします。

## Kafkaトピックの作成

これでKafkaブローカーが実行されているので、Kafkaトピックを作成できます。 Kafkaトピックは、メッセージの保存の論理単位です。名前で識別され、複数のパーティションに分けられます。パーティションはKafkaクラスタ全体に分散されています。

次のコマンドを使用して、2つのパーティションを持つ「test」というKafkaトピックを作成できます。

```
bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 2 --topic test
```

## メッセージの生成

これでKafkaトピックがあるので、メッセージの生成を開始できます。メッセージを生成するために使用できるコマンドラインツールであるKafkaコンソールプロデューサを使用します。コンソールプロデューサは、標準入力からメッセージを読み取り、Kafkaブローカーに送信します。

次のコマンドでコンソールプロデューサーを起動できます。

```
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
```

コンソールプロデューサーは今メッセージを待っています。メッセージを入力し、Enter キーを押して送信できます。メッセージはKafkaブローカーに送信され、割り当てられたパーティションに複製されます。

## メッセージ消費

Kafkaのトピックがあり、メッセージを生成しているので、メッセージの使用を開始できます。メッセージを消費するために使用できるコマンドラインツールであるKafkaコンソールコンシューマを使用します。コンソールコンシューマはKafkaブローカからメッセージを読み、標準出力に書き込みます。

次のコマンドでコンソールコンシューマを起動できます。

```
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning
```

コンソールコンシューマは現在、Kafka ブローカからメッセージを読み込み、標準出力への書き込みを開始します。コンソールプロデューサを使用して送信されたメッセージが表示されます。

##スプリングブートとカフカ

Kafkaを設定する方法とメッセージを生成して消費する方法を見てみました。 Spring Bootは、自動構成や組み込みサーバーなどのデータストリーミングアプリケーションに役立ついくつかの機能を提供します。

Spring Bootは、アプリケーションに含めることができる事前設定された依存関係である複数のStarter POMも提供します。たとえば、「spring-kafka-starter」スターターPOMには、KafkaとSpring Kafkaへの依存関係が含まれています。

このセクションでは、 `spring-kafka-starter`スターターPOMを使って簡単なメッセージプロデューサーとコンシューマーアプリケーションを開発する方法を説明します。

##メッセージプロデューサー

最初にすべきことは、Spring Bootアプリケーションを作成することです。アプリケーションの上位に `spring-boot-starter-parent` スターター POM を使用します。 `spring-boot-starter-parent`スターターPOMは、私たちが継承できるいくつかの依存関係とプラグイン管理機能を提供します。

Spring Initializrを使用してSpring Bootアプリケーションを作成できます。 Spring Initializrは、Spring Bootアプリケーションの作成に使用できるWebベースのツールです。 Spring Initializrを使用して、 `spring-kafka-starter` Starter POMを使用してMavenベースのSpring Bootアプリケーションを作成できます。

アプリケーションが作成されたら、 `pom.xml`ファイルに次の依存関係を追加できます。

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.kafka</groupId>
        <artifactId>spring-kafka</artifactId>
    </dependency>
    <dependency>
        <groupId>org.apache.kafka</groupId>
        <artifactId>kafka-clients</artifactId>
        <version>2.4.0</version>
    </dependency>
</dependencies>
```

`spring-kafka-starter`スターターPOMは`kafka-clients`の依存関係をもたらします。 `spring-kafka-starter` Starter POMに含まれるバージョンがApache Kafka 2.4.0と互換性がないため、`kafka-clients`依存関係バージョンを指定する必要があります。

これで依存関係があるので、構成クラスを作成できます。構成クラスは、Kafka プロデューサーを構成するために使用されます。 Spring BootアプリケーションでKafkaを有効にするために `@EnableKafka`アノテーションを使うことができます。

また、`KafkaTemplate` Beanも生成します。 「KafkaTemplate」は、Kafkaにメッセージを送信するために使用できるヘルパークラスです。

```java
@Configuration
ツイートをサイトに埋め込む
public class KafkaConfig {

    @Bean
    public KafkaTemplate<String, String> kafkaTemplate(
            ProducerFactory<String, String> producerFactory) {
        return new KafkaTemplate<>(producerFactory);
    }
}
```

これで、メッセージプロデューサー Bean を作成できます。メッセージコンストラクタ Bean は、Kafka にメッセージを送信するために使用されます。メッセージコンストラクタBeanに `KafkaTemplate`を挿入します。

```java
@Component
public class MessageProducer {

    private KafkaTemplate <String、String> kafkaTemplate;

    @Autowired
    public MessageProducer(KafkaTemplate<String, String> kafkaTemplate) {
        this.kafkaTemplate = kafkaTemplate;
    }

    public void sendMessage(String topic, String message) {
        kafkaTemplate.send（topic、message）;
    }
}
```

'sendMessage'メソッドは、Kafkaトピックにメッセージを送信するために使用できます。メッセージ消費者はこの方法を使用します。

## メッセージコンシューマ

これでメッセージコンシューマBeanを作成できます。メッセージコンシューマBeanはKafkaからのメッセージを消費するために使用されます。メッセージコンシューマBeanに `KafkaTemplate`と `MessageProducer`を挿入します。

```java
@Component
public class MessageConsumer {

    private KafkaTemplate <String、String> kafkaTemplate;
    private MessageProducer messageProducer;

    @Autowired
    public MessageConsumer(
            KafkaTemplate<String, String> kafkaTemplate,
            MessageProducer messageProducer) {
        this.kafkaTemplate = kafkaTemplate;
        this.messageProducer = messageProducer;
    }

    @KafkaListener(topics = "test")
    public void processMessage(String message) {
        messageProducer.sendMessage("test2", message);
    }
}
```

`processMessage`メソッドは `@KafkaListener`としてコメントアウトされます。このコメントは、Kafka メッセージ受信機を設定するために使用されます。 `@KafkaListener`コメントは、Kafkaトピックからメッセージを受信したときに呼び出されるメソッドにコメントを追加するために使用できます。この例では、「@KafkaListener」アノテーションを使用して「テスト」トピックのメッセージリスナーを構成します。

`@KafkaListener`コメントには、メッセージリスナーを設定するために使用できるいくつかの属性があります。

- `topics`：聞くKafkaトピックのリストです。
- `groupId`：KafkaコンシューマグループID。
- `containerFactory`: 使用する `KafkaListenerContainerFactory` です。

`processMessage`メソッドは、「test」エントリからメッセージを受信すると呼び出されます。メッセージは処理され、次に「test2」エントリに送信されます。

これでアプリケーションを実行し、「テスト」トピックに関するメッセージを生成できるようになりました。メッセージが処理され、「test2」トピックに送信されます。 Kafkaコンソールの消費者を使用して、「test2」トピックのメッセージを使用できます。

##結論

この記事では、KafkaとSpring Bootを使用して簡単なメッセージプロデューサーとコンシューマーアプリケーションを構築する方法を紹介しました。また、メッセージベースのマイクロサービスを構築するためのライブラリであるSpring Cloud Streamの使用方法も示しました。