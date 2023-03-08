---
title: AWS での Kubernetes: アマゾン ウェブ サービスでのクラスターのデプロイ
description: 
published: true
date: 2023-02-01T00:06:05.586Z
tags: 
editor: markdown
dateCreated: 2023-02-01T00:06:03.907Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Kubernetes on AWS: Deploying Clusters on Amazon Web Services***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-aws-deploying-clusters-on-amazon-web-services)
{.links-list}



#AWSのクーバーネティス：Amazon Web Servicesにクラスターをデプロイする

Kubernetesは、アプリケーションの展開、拡張、および管理を自動化するためのオープンソースコンテナオーケストレーションシステムです。アプリケーションを構成するコンテナを論理単位でグループ化することで、簡単に管理および検索できます。

AWSは、Amazonが提供する包括的で進化するクラウドコンピューティングプラットフォームです。 IaaS（Infrastructure as a Service）、PaaS（Platform as a Service）、およびパッケージ型SaaS（Software as a Service）製品を混合して提供します。

AWS で Kubernetes を使用して、AWS でコンテナ化されたアプリケーションをデプロイ、管理、および拡張できます。この記事では、AWS で Kubernetes クラスターをデプロイする方法について説明します。

## 前提条件

このガイドに従うには、次のものが必要です。

- AWSアカウント。アカウントがない場合は、ここ（https://aws.amazon.com/）で作成できます。

- コンピュータにインストールおよび設定されたAWSコマンドラインインターフェイス（CLI）。これを行う方法については、[こちら]（https://docs.aws.amazon.com/cli/latest/userguide/installing.html）にあります。

- コンピュータにインストールされたkubectlコマンドラインツール。これを行う方法については、[ここ]（https://kubernetes.io/docs/tasks/tools/install-kubectl/）にあります。

- ドメイン名。 [Freenom]（https://www.freenom.com/）などのサービスで無料で入手できます。

## AWS Kubernetes クラスターの設定

AWS で Kubernetes クラスターを設定する方法はいくつかあります。この記事では、AWSマネジメントコンソールを使用してクラスターを設定します。

まず、AWSマネジメントコンソールにログインし、Amazon EKSサービスに移動します。

![](https://i.imgur.com/LDAd5u8.png)

「クラスタの作成」ボタンをクリックします。

![](https://i.imgur.com/p0bJUO4.png)

次のページでクラスタ名を入力し、展開する地域を選択します。次に、使用するKubernetesのバージョンを選択します。作成時に最新バージョンの1.17を使用します。

![](https://i.imgur.com/Ft7YIxu.png)

次に、ワーカーノードを構成する必要があります。ワーカーノードは、アプリケーションを実行するクラスタのマシンです。ワーカーノードにAmazon EC2インスタンスを使用します。

「CloudFormation スタックの開始」ボタンをクリックします。

![](https://i.imgur.com/O4E0b4I.png)

次のページで、「AWS CloudFormationがIAMリソースを作成できることを確認してください」チェックボックスを選択して[スタックの作成]ボタンをクリックします。

![](https://i.imgur.com/VkzM0Ss.png)

次のページでは、CloudFormationで作成されたスタックを表示できます。これには数分かかります。

![](https://i.imgur.com/W0Qiu8D.png)

スタックが作成されたら、[出力]タブをクリックしてワーカーノード構成の詳細を表示できます。

![](https://i.imgur.com/tY0NVT3.png)

後で必要なので、「NodeInstanceRole」と「WorkerNodeSecurityGroup」の値を書き留めます。

これでワーカーノードが設定されたので、Amazon EKSコンソールに戻ってクラスターを作成できます。

「次のステップ」ボタンをクリックしてください。

![](https://i.imgur.com/Ft7YIxu.png)

次のページでワーカーノードを設定する必要があります。必要なワーカーノードの数を選択し、以前に記録した「NodeInstanceRole」と「WorkerNodeSecurityGroup」の値を入力します。

![](https://i.imgur.com/vALDKQi.png)

次に、ネットワークを構成する必要があります。 「VPC」オプションを選択し、CloudFormationスタックで作成したVPCを選択します。次に、「サブネット」オプションを選択し、CloudFormationスタックで作成した2つのサブネットを選択します。

![](https://i.imgur.com/7DpjTGi.png)

これで、Kubernetesクラスターエンドポイントアクセスタイプを選択する必要があります。 「公開」オプションを選択します。

![](https://i.imgur.com/DY0b4oI.png)

次に、セキュリティグループを設定する必要があります。 [セキュリティグループ]オプションを選択し、CloudFormationスタックで作成したセキュリティグループを選択します。

![](https://i.imgur.com/4JcM0Ss.png)

これで、Kubernetes クラスターのログ記録の種類を選択する必要があります。 「Amazon CloudWatch」オプションを選択します。

![](https://i.imgur.com/BkzM0Ss.png)

次に、Kubernetesクラスターの監視タイプを選択する必要があります。 「Amazon CloudWatch」オプションを選択します。

![](https://i.imgur.com/nALDKQi.png)

これで、Kubernetesクラスター暗号化タイプを選択する必要があります。 「AES-256」オプションを選択します。

![](https://i.imgur.com/p0bJUO4.png)

これで、Kubernetes クラスターの自動拡張グループの種類を選択する必要があります。 「AsgBasedAutoScaling」オプションを選択します。

![](https://i.imgur.com/FkzM0Ss.png)

これで、ワーカーノードAuto-Scalingグループを設定する必要があります。 「WorkerNodesAsg」オプションを選択し、CloudFormationスタックで作成した自動拡張グループを選択します。

![](https://i.imgur.com/VkzM0Ss.png)

これで、Kubernetesクラスタ拡張構成タイプを選択する必要があります。 「デフォルト」オプションを選択します。

![](https://i.imgur.com/p0bJUO4.png)

次のページでクラスタ構成を確認し、[クラスタの作成]ボタンをクリックします。

![](https://i.imgur.com/LDAd5u8.png)

次のページでクラスタが作成されていることがわかります。これには数分かかります。

![](https://i.imgur.com/W0Qiu8D.png)

クラスタが作成されたら、[kubectlの設定]ボタンをクリックしてクラスタと通信するようにkubectlコマンドラインツールを設定できます。

![](https://i.imgur.com/nALDKQi.png)

次のページで、「設定のダウンロード」ボタンをクリックしてください。

![](https://i.imgur.com/7DpjTGi.png)

これにより、kubeconfigファイルがコンピュータにダウンロードされます。このファイルを ~/.kube ディレクトリに移動し、名前を config に変更します。

これで、次のコマンドを実行してクラスタが機能しているかどうかをテストできます。

```
kubectl get svc
```

すべてが正しく機能したら、クラスタにサービスの一覧を表示する必要があります。

## Kubernetesクラスタへのアプリケーションのデプロイ

これでKubernetesクラスタが起動して実行されているので、ここにアプリケーションをデプロイできます。この例では、Goで書かれた単純な「Hello World」アプリケーションをデプロイします。

まず、アプリケーション用のDockerfileを作成する必要があります。次の内容で、プロジェクトのルートに「Dockerfile」というファイルを作成します。

```
FROM golang:1.13-アルピン

RUN mkdir /app

ADD。 /app/

WORKDIR /app

RUN go build -o main 。

CMD ["/app/main"]
```

次に、アプリケーションコードを書く必要があります。次の内容で、プロジェクトのルートに「main.go」というファイルを作成します。

「go」
package main

import(
    "fmt"
    「net/http」
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello World!")
}

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8080", nil)
}
```

これで、DockerイメージをビルドしてDockerレジストリにプッシュできます。 DockerレジストリにAmazon ECRを使用します。

まず、Amazon ECRで新しいリポジトリを作成する必要があります。 Amazon ECR コンソールにログインし、「リポジトリの作成」ボタンをクリックします。

![](https://i.imgur.com/tY0NVT3.png)

次のページでリポジトリ名を入力し、[リポジトリの作成]ボタンをクリックします。

![](https://i.imgur.com/nALDKQi.png)

これで、Dockerイメージをビルドして新しいリポジトリにプッシュできます。

次のコマンドを実行してDockerイメージをビルドしてプッシュします。

```
$ docker build -t {your_aws_account_id}.dkr.ecr.{your_region}.amazonaws.com/{your_repository_name} 。

$ docker push {your_aws_account_id}.dkr.ecr.{your_region}.amazonaws.com/{your_repository_name}
```

{your_aws_account_id}、{your_region}、{your_repository_name} をアカウントとリポジトリに適した値に置き換えます。

Dockerイメージがリポジトリにプッシュされたため、Kubernetesクラスタに展開できます。

まず、配布ファイルを作成する必要があります。次の内容で、プロジェクトのルートに「deployment.yaml」というファイルを作成します。

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
spec:
  レプリカ：3
  セレクター：
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: {your_aws_account_id}.dkr.ecr.{your_region}.amazonaws.com/{your_repository_name}
        ports:
        - containerPort: 8080
```

{your_aws_account_id}、{your_region}、{your_repository_name} をアカウントとリポジトリに適した値に置き換えます。

これで、次のコマンドを実行してKubernetesクラスタにアプリケーションをデプロイできます。

```
kubectl apply -f deployment.yaml
```

これにより、3つのレプリカを持つ「hello-world」という配布が作成されます。

実際の配置を見るには、それを外部の世界にさらす必要があります。サービスを作成してこれを実行できます。

まずサービスファイルを生成する必要があります。次の内容で、プロジェクトのルートに「service.yaml」というファイルを作成します。

```yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-world
spec:
  type: LoadBalancer
  ports:
  - port: 80
    protocol: TCP
    targetPort: 8080
  セレクター：
    app: hello-world
```

これで、次のコマンドを実行してサービスを展開できます。

```
kubectl apply -f service.yaml
```

これにより、「LoadBalancer」タイプの「hello-world」というサービスが作成されます。このタイプのサービスはAWSでロードバランサーを作成し、デプロイを外部の世界に公開します。

ロードバランサの URL を検索するには、次のコマンドを実行します。

```
kubectl get svc hello-world
```

次のような出力が表示されます。

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
hello-world LoadBalancer 10.100.200.16 aaa.bbb.ccc.ddd 80:32000/TCP,443:31943/TCP 5m29s
```

「EXTERNAL-IP」値はロードバランサーのURLです。

## Kubernetesクラスターの削除

Kubernetes クラスターを削除する場合は、Amazon EKS コンソールから削除できます。

まず、Amazon EKSコンソールにログインして[クラスタ]ページに移動します。

![](https://i.imgur.com/LDAd5u8.png)

次のページで、削除するクラスタの横にあるチェックボックスを選択して[削除]ボタンをクリックします。

![](https://i.imgur.com/7DpjTGi.png)

次のページの[クラスタ名]フィールドにクラスタ名を入力し、[クラスタの削除]ボタンをクリックします。

![](https://i.imgur.com/p0bJUO4.png)

##結論

この記事では、AWS に Kubernetes クラスターをデプロイする方法について説明しました。また、クラスタにアプリケーションをデプロイする方法も示しました。

Kubernetesの詳細については、次のリソースをお勧めします。

- クバネティス公式文書：https://kubernetes.io/docs/

- 公式Amazon EKSドキュメント：https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html

- 公式Amazon ECRドキュメント：https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html