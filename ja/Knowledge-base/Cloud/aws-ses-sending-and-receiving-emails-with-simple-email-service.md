---
title: AWS SES: Simple Email Service を使用した E メールの送受信
description: 
published: true
date: 2023-02-17T18:14:51.668Z
tags: 
editor: markdown
dateCreated: 2023-01-30T21:57:30.665Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [AWS SES: Sending and Receiving Emails with Simple Email Service***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-ses-sending-and-receiving-emails-with-simple-email-service)
{.links-list}


#AWS SES：簡単なEメールサービスでEメールを送受信する

IT開発学習ブログへようこそ。この記事では、AWS Simple Email Serviceを使用してEメールを送受信する方法について説明します。

## AWSシンプルメールサービスとは何ですか？

AWS Simple Email Service（SES）は、Eメールを送受信する費用対効果の高い柔軟な方法です。独自のドメイン名を使用して電子メールを送受信できるクラウドベースの電子メールサービスであり、個人と企業のユースケースの両方をサポートします。

AWS SES は、他の AWS サービスと統合される信頼性の高いスケーラブルなメールサービスです。前払い費用のない従量制価格モデルを提供し、設定と使用が簡単です。

## AWS SESにメールを送信

AWS SESを使用してEメールを送信するには、AWSアカウントと確認済みのEメールアドレスまたはドメインが必要です。まだAWSアカウントがない場合は、[ここ]（https://aws.amazon.com/）でアカウントを作成できます。

AWS アカウントをお持ちの場合は、[メールアドレスの確認] (https://docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-email-addresses.html) または [ドメイン] (https://docs.aws.amazon .com/ses/latest/DeveloperGuide/verify-domains.html) を AWS SES で使用します。メールアドレスまたはドメインを確認したら、メールの送信を開始できます。

AWS SESコンソール、AWS SES API、またはAWSコマンドラインインターフェイス（CLI）を使用してEメールを送信できます。この記事では、AWS SESコンソールを使用してEメールを送信します。

まず、AWS SES コンソールに移動し、メニューから **Eメールアドレス**を選択します。次に、**新しいメールアドレスを確認**を選択し、確認したいメールアドレスを入力します。

![メールアドレス確認](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/01-verify-email-address.png)

AWS SESは、入力したアドレスに確認メールを送信します。確認メールの指示に従って確認手順を完了してください。

これでEメールアドレスを確認したので、最初のEメールを送信する準備が整いました。 **AWS SESコンソール**に移動し、**シングルメール送信**を選択します。

![シングルメール送信](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/02-send-email.png)

**シングルメール送信**ページに次の情報を入力します。

* **送信者**：電子メールの送信に使用する確認済みの電子メールアドレスを入力します。
* **受信者**: 受信者のメールアドレスを入力します。
* **タイトル**: メールの件名を入力します。
* **メッセージ**: メール本文を入力します。 **ビジュアルエディタ**または**HTMLエディタ**を使用してメール形式を指定できます。

完了したら**メールを送信**を選択します。

![メールを送信](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/03-send-email.png)

Eメールが正常に送信されたら、AWS SESから確認Eメールを受け取る必要があります。

## AWS SESでEメールを受信する

Eメールを送信することに加えて、AWS SESを使用してEメールを受信することもできます。 AWS SES を使用してメールボックスから電子メールを受信したり、受信メールを Amazon S3 や Amazon Lambda などの他の AWS サービスにルーティングできます。

メールの受信を設定するには、まずAWS SESで[ルールセットの設定]（https://docs.aws.amazon.com/ses/latest/DeveloperGuide/receiving-email-getting-started.html）が必要です。コンソール。ルールセットは、AWS SES が受信メールを処理する方法を決定する 1 つ以上のルールで構成されます。

![ルールセット](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/04-rule-sets.png)

ルールセットを設定するには、メニューから**ルールセット**を選択し、**ルールセットの作成**を選択します。 **ルールセットの作成**ページでルールセットの名前を入力し、**ルールセットの作成**を選択します。

![ルールセットの作成](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/05-create-rule-set.png)

ルールセットが作成されたら、ここにルールを追加できます。ルールは、一連の条件とアクションで構成されます。受信メールがルール条件を満たしている場合は、ジョブが実行されます。

ルールセットにルールを追加するには、[ルールの追加]を選択し、次の情報を入力します。

* **名前**：ルールの名前を入力します。
* **説明**: ルールの説明を入力します。
* **範囲**：ルールをすべてのEメールに適用するか、特定の条件を満たすEメールにのみ適用するかを選択します。
* **受信者**：電子メールを受信する電子メールアドレスを入力します。
* **タスク**：ルールがトリガーされたときにAWS SESで実行するアクションを選択します。メールを Amazon S3 バケットに保存するか、Amazon Lambda 関数に送信するか、別のメールアドレスに転送するかを選択できます。

完了したら、**ルールの作成**を選択します。

![ルールの作成](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/06-create-rule.png)

これでルールセットを作成してルールを追加したので、電子メールを受信する準備が整いました。設定をテストするには、ルールで指定したメールアドレスにメールを送信します。指定したメールボックスまたはAmazon S3バケットからEメールを受け取る必要があります。

##結論

この記事では、AWS Simple Email Serviceを使用してEメールを送受信する方法について説明しました。また、受信メールを処理するためのルールセットを設定する方法も示しました。

AWS SESは、Eメールを送受信する費用対効果の高いスケーラブルな方法です。セットアップと使用が簡単で、他のAWSサービスと統合されます。アプリケーションがEメールを送受信する必要がある場合は、AWS SESを使用することをお勧めします。

##追加リソース

AWS SES の詳細については、次のリソースをお勧めします。

* [AWS SES開発者ガイド]（https://docs.aws.amazon.com/ses/latest/DeveloperGuide/Welcome.html）
* [Amazon SESにEメールを送信]（https://aws.amazon.com/ses/sending-email/）
* [Amazon SESでEメールを受信]（https://aws.amazon.com/ses/receiving-email/）