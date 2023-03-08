---
title: Spring Boot アプリケーションをクラウドにデプロイする
description: 
published: true
date: 2023-02-17T18:03:21.166Z
tags: 
editor: markdown
dateCreated: 2023-01-30T11:02:21.959Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Deploying Spring Boot Applications to the Cloud***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/deploying-spring-boot-applications-to-the-cloud)
{.links-list}


# Spring Bootアプリケーションをクラウドにデプロイ

今日、開発者はアプリケーションをデプロイするプラットフォームに関して選択の幅が広いです。クラウドは、強力なサービスを提供するAmazon Web Services（AWS）、Microsoft Azure、およびGoogle Cloud Platform（GCP）の3つの主要プロバイダーとともに、新しいアプリケーションをデプロイするための事実上の標準になりました。

この記事では、Spring Bootアプリケーションをクラウドにデプロイすることに焦点を当てます。 Spring Bootは、「単に実行」できるスタンドアロンのプロダクションクラスSpringベースのアプリケーションを簡単に作成できる人気のあるJavaベースのフレームワークです。

Spring Bootアプリケーションをクラウドにデプロイする方法はいくつかあります。最も広く使用されている2つのアプローチを取り上げます。

* PaaS（Platform as a Service）にデプロイ
* IaaS（Infrastructure as a Service）にデプロイ

## PaaS(Platform as a Service)にデプロイ

PaaS（Platform as a Service）は、サードパーティのプロバイダが通常、サービスやプラットフォームの形式でインターネットを介してユーザーにプラットフォームとインフラストラクチャを提供するクラウドコンピューティングモデルです。

PaaSはクラウドで完全な開発と展開を提供するため、開発者は基本的なインフラストラクチャを心配することなくコードを書くことに集中できます。

###ヘロク

人気のPaaSプロバイダの1つは[Heroku]（https://www.heroku.com/）で、Spring Bootアプリケーションホスティングに最適化されたプラットフォームを提供します。

Herokuの魅力はシンプルさにあります。 Spring BootアプリケーションをHerokuにデプロイするには、プロジェクトのルートに次の行を含む `Procfile`を作成するだけです。

    Web: java -jar target/<アプリケーション名>.jar

また、 `pom.xml`ファイルに次の依存関係を追加する必要があります。

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
    <scope>provided</scope>
</dependency>
```

完了したら、 `heroku`コマンドラインツールを使用してアプリケーションをHerokuにデプロイできます。まず、新しいHerokuアプリケーションを作成する必要があります。

    ヘロク生成

その後、アプリケーションをHerokuにデプロイできます。

    git push ヘロクマスター

これで、アプリケーションは `https://<your-app-name>.herokuapp.com`で実行されます。

###クラウドファウンドリ

[Cloud Foundry]（https://www.cloudfoundry.org/）は、Spring Bootアプリケーションの展開を検討する価値があるもう1つの人気のあるPaaSプロバイダです。

Herokuと同様に、Cloud Foundryを使用すると、Spring Bootアプリケーションを簡単にデプロイできます。 Spring BootアプリケーションをCloud Foundryにデプロイする前に、プロジェクトのルートに `manifest.yml`ファイルを作成する必要があります。このファイルには、名前、メモリー制限、ホスト名などのアプリケーションに関する情報が含まれています。

以下は `manifest.yml`ファイルの例です。

```yaml
---
applications:
- name: my-app
  memory: 512M
  disk_quota: 1024M
  instances: 1
  path: build/libs/my-app.jar
  env：
    JAVA_OPTS: -Djava.security.egd=file:///dev/urandom
  buildpack: https://github.com/cloudfoundry/java-buildpack
```

その後、 `cf`コマンドラインツールを使用してアプリケーションをCloud Foundryにデプロイできます。

    cfプッシュ

これで、アプリケーションは `https://<your-app-name>.cfapps.io`で実行されます。

##IaaS（Infrastructure as a Service）にデプロイ

IaaS（Infrastructure as a Service）は、サードパーティのプロバイダがインターネットを介してユーザーにインフラストラクチャ（通常はサーバー、ストレージ、およびネットワーク）を提供するクラウドコンピューティングモデルです。

IaaS は、開発者に PaaS よりも基本インフラストラクチャのコントロールをはるかに多く提供しますが、セットアップとメンテナンスにはより多くの作業が必要です。

### AWS

AWS（Amazon Web Services）は最も人気のあるIaaSプロバイダであり、Spring Bootアプリケーションをホストするために使用できる幅広いサービスを提供します。このセクションでは、[Elastic Beanstalk]（https://aws.amazon.com/elasticbeanstalk/）を使用してSpring BootアプリケーションをAWSにデプロイする方法に焦点を当てます。

Elastic Beanstalkは、Java、.NET、PHP、Node.js、Python、およびRubyで開発されたWebアプリケーションおよびサービスを、Apache、Nginx、Passenger、IISなどの使いやすいサーバーに簡単に展開、管理、および拡張できるサービスです。 。

Elastic BeanstalkにSpring Bootアプリケーションをデプロイする前に、プロジェクトの `src/main/resources`ディレクトリに `application.properties`ファイルを作成する必要があります。このファイルには、名前、バージョン、環境などのアプリケーションに関する情報が含まれています。

以下は `application.properties` ファイルの例です。

``properties
name=my-app
version=1.0.0
environment=production
```

また、プロジェクトのルートに `AWS Elastic Beanstalk`ファイルを作成する必要があります。このファイルには、リージョン、インスタンスタイプ、セキュリティグループなどのアプリケーション環境に関する情報が含まれています。

以下は `AWS Elastic Beanstalk` ファイルの例です。

```yaml
---
AWSEBDebuggingMode: true
AWSEBEnvironmentVariables:
  JAVA_OPTS: -Djava.security.egd=file:///dev/urandom
AWSEBServiceRole: null
AWSEBUseAmi64：true
AWSEluaticLoadBalancerScheme: internet-facing
AWSEBSecurityGroups:
- my-security-group
AWSEBSubnets:
- subnet-12345678
AWSEBIAMInstanceProfile: null
AWSEBRDSDatabaseInstance: null
AWSEBRDSDatabasePassword: null
AWSEBRDSDatabaseUsername: null
AWSEBRDSDatabaseEngine: null
AWSEBRDSDatabaseName: null
AWSEBRDSSnapshotIdentifier: null
AWSEBRDSAllocatedStorage: null
AWSEBRDSStorageType: null
AWSEBRDSMultiAZ: null
AWSEBRDSIops: null
AWSEBRDSEncrypted: null
AWSEBRDSKmsKeyId: null
AWSEBRDSDeletionPolicy: null
AWSEBS3Key: my-s3-key
AWSEBS3Bucket: my-s3-bucket
AWSEBS3ObjectKey: my-s3-object-key
AWSEBS3ETag: my-s3-etag
AWSEBS3VersionId: my-s3-version-id
AWSEBS3Region: us-east-1
AWSEBS3StorageClass: STANDARD
AWSEBNotificationEndpoint: null
AWSEBNotificationProtocol: null
AWSEBNotificationTopicARN: null
AWSEBManagedActionHistoryRetentionPeriod: 14
```

これらのファイルを作成したら、 `eb`コマンドラインツールを使用してアプリケーションをElastic Beanstalkにデプロイできます。まず、新しいElastic Beanstalkアプリケーションを作成する必要があります。

    EB作成

その後、アプリケーションをElastic Beanstalkにデプロイできます。

    EB配信

これで、アプリケーションは `http://<your-app-name>.elasticbeanstalk.com`で実行されます。

### アジュール

Microsoft Azureは、Spring Bootアプリケーションをホストするために使用できるさまざまなサービスを提供するもう1つの人気のあるIaaSプロバイダです。このセクションでは、[App Service]（https://docs.microsoft.com/en-us/azure/app-service/overview）を使用してAzureにSpring Bootアプリケーションをデプロイする方法に焦点を当てます。

App Serviceは、WebアプリケーションとWebサービスのホスティングに最適化されたMicrosoft Azure PaaSサービスです。 App ServiceにSpring Bootアプリケーションをデプロイする前に、プロジェクトの `src/main/resources`ディレクトリに `application.properties`ファイルを作成する必要があります。このファイルには、名前、バージョン、環境などのアプリケーションに関する情報が含まれています。

以下は `application.properties` ファイルの例です。

``properties
name=my-app
version=1.0.0
environment=production
```

また、プロジェクトの `src/main/webapp/WEB-INF` ディレクトリに `web.xml` ファイルを生成する必要があります。このファイルには、サーブレットクラスやマッピングなどのアプリケーションのサーブレットに関する情報が含まれています。

以下は `web.xml` ファイルの例です。

```xml
<web-app>
  <servlet>
    <servlet-name>my-app</servlet-name>
    <servlet-class>org.springframework.boot.web.servlet.support.SpringBootServletInitializer</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>my-app</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
</web-app>
```

これらのファイルを作成したら、 `az`コマンドラインツールを使用してアプリケーションをApp Serviceにデプロイできます。まず、新しいApp Serviceアプリケーションを作成する必要があります。

    az appservice plan create --name my-app-service-plan --resource-group my-resource-group --sku S1

その後、アプリケーションをApp Serviceにデプロイできます。

    az webapp create --resource-group my-resource-group --plan my-app-service-plan --name my-app --deployment-container-image="mcr.microsoft.com/java/jdk:8u192-ズールー - アルパイン」

これで、アプリケーションは `http://my-app.azurewebsites.net`で実行されます。

##結論

この記事では、Spring Bootアプリケーションをクラウドにデプロイする2つの方法について説明しました。

* PaaS（Platform as a Service）にデプロイ
* IaaS（Infrastructure as a Service）にデプロイ

各アプローチには独自の長所と短所があるため、アプリケーションに適したものを選択することが重要です。

アプリケーションをクラウドで起動して実行するための迅速で簡単な方法を探している場合は、PaaSが適しています。 HerokuとCloud Foundryは、考慮する価値がある2つの人気のあるPaaSプロバイダです。

基盤インフラストラクチャのより多くの制御を探している場合は、IaaSが行く方法です。 AWSとAzureは、Spring Bootアプリケーションをホストするために使用できる幅広いサービスを提供する2つの人気のあるIaaSプロバイダです。