---
title: Kubernetes と Docker を使用したバックエンド アプリケーションのデプロイ
description: 
published: true
date: 2023-02-01T04:36:56.712Z
tags: 
editor: markdown
dateCreated: 2023-02-01T04:36:55.108Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Deploying Backend Applications with Kubernetes and Docker***English** version of this document is available*](/en/Knowledge-base/Backend/deploying-backend-applications-with-kubernetes-and-docker)
{.links-list}



#CubernetesとDockerでバックエンドアプリケーションをデプロイする

この記事では、KubernetesとDockerを使用してバックエンドアプリケーションをデプロイする方法について説明します。まず、これらの技術が何であり、どのように連携するのかを見てみましょう。次に、Kubernetes クラスターをセットアップし、ここにアプリケーションをデプロイする方法について、段階的なガイドを提供します。

## クバネティスとは？

Kubernetesは、開発者がコンテナ化されたアプリケーションを大規模に展開および管理できるようにするコンテナオーケストレーションプラットフォームです。 Kubernetesは、コンテナ化されたアプリケーションのプロビジョニング、拡張、および監視を自動化します。また、複雑なアプリケーションを簡単にデプロイおよび管理できる宣言的構成モデルも提供します。

##ドッカーとは？

Dockerは、開発者が孤立した環境でアプリケーションをパッケージ化してデプロイできるようにするコンテナ化プラットフォームです。 Dockerコンテナは、アプリケーション用の軽量でポータブルなスタンドアロン環境を提供します。デプロイしやすく、Dockerをサポートする任意のプラットフォームで実行できます。

## KubernetesとDockerはどのように連携しますか？

KubernetesとDockerは連携して、コンテナ化されたアプリケーションをデプロイおよび管理するためのプラットフォームを提供します。 KubernetesはDockerコンテナのプロビジョニング、拡張、監視を自動化します。また、複雑なアプリケーションを簡単にデプロイおよび管理できる宣言的構成モデルも提供します。

## Kubernetesクラスタの設定

このセクションでは、Kubernetes クラスターを設定する方法について説明します。 Kubernetesコマンドラインツールkubectlを使用してクラスタを設定します。

まず、kubectlをインストールする必要があります。私たちはこれをカールにすることができます：

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64 /kubectl
```

次に、kubectlバイナリを実行可能にする必要があります。

```
chmod +x ./kubectl
```

最後に、kubectlバイナリをPATHに移動できます。

```
sudo mv ./kubectl /usr/local/bin/kubectl
```

これでkubectlをインストールしたので、それを使用してKubernetesクラスターを設定できます。単一ノードで実行される Kubernetes 実装である Minikube を使用します。

まず、Minikubeをインストールする必要があります。私たちはこれをカールにすることができます：

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

次に、Minikubeバイナリを実行可能にする必要があります。

```
chmod +x minikube
```

最後に、MinikubeバイナリをPATHに移動できます。

```
sudo mv minikube /usr/local/bin/
```

Minikubeをインストールしたので、それを使用してKubernetesクラスタを設定できます。 Minikubeクラスタを起動するには、次のコマンドを実行します。

```
minikube start
```

これにより、1 つのノードで Minikube クラスタが起動します。

## Kubernetesへのアプリケーションのデプロイ

このセクションでは、アプリケーションをKubernetesにデプロイする方法について説明します。簡単なNode.jsアプリケーションを例として使用します。

まず、アプリケーション用のDockerfileを作成する必要があります。 Dockerfileは、Dockerイメージを構築するための指示を含むテキストファイルです。

Dockerfileは次のようになります。

```
FROM node:8

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY 。 。

EXPOSE 3000

CMD ["npm", "start"]
```

この Dockerfile は node:8 Docker イメージをデフォルトイメージとして使用します。その後、プロジェクトはpackage.jsonファイルとpackage-lock.jsonファイルを/ appディレクトリにコピーします。次に、npm installを実行して依存関係をインストールします。最後に、残りのプロジェクトファイルを/ appディレクトリにコピーし、ポート3000を公開します。

これでDockerfileがあるので、Dockerイメージを構築できます。イメージ名を my-app として指定します。

```
docker build -t my-app 。
```

これにより、my-appという名前のDockerイメージが構築されます。

これでDockerイメージがあるので、Dockerレジストリにプッシュできます。 Docker Hubをレジストリとして使用します。

まず、Docker Hubアカウントを作成する必要があります。その後、Docker Hubアカウントにログインする必要があります。

```
docker login
```

次に、Docker Hubユーザー名でDockerイメージにタグを付ける必要があります。

```
docker tag my-app <your-docker-hub-username>/my-app
```

最後に、Docker イメージを Docker Hub にプッシュできます。

```
docker push <your-docker-hub-username>/my-app
```

Docker イメージが Docker Hub にあるので、これを Kubernetes クラスターにデプロイできます。

まず、展開を作成する必要があります。展開は、レプリカグループを管理するKubernetesオブジェクトです。レプリカは、Kubernetesが私たちのノードで実行するアプリケーションのコピーです。

展開を作成するには、次のコマンドを実行します。

```
kubectl create deployment my-app --image=<your-docker-hub-username>/my-app
```

これにより、my-appという配布が作成されます。 --imageフラグは、展開で使用するDockerイメージを指定します。

次に、サービスを作成する必要があります。サービスは、アプリケーションを外部の世界に公開するKubernetesオブジェクトです。

サービスを生成するには、次のコマンドを実行します。

```
kubectl expose deployment my-app --type=LoadBalancer --port=80 --target-port=3000
```

これにより、my-appというサービスが作成されます。 --typeフラグはサービスタイプを指定します。 --port フラグは、サービスが使用するポートを指定します。 --target-port フラグは、アプリケーションが実行されるポートを指定します。

最後に、サービスのURLを取得できます。

```
kubectl get service my-app
```

これは私たちのサービスのURLを出力します。これで、このURLからアプリケーションにアクセスできます。

##結論

この記事では、KubernetesとDockerを使用してバックエンドアプリケーションをデプロイする方法について説明しました。まず、これらの技術が何であり、どのように連携するかを見てみました。次に、Kubernetes クラスターをセットアップし、ここにアプリケーションをデプロイする方法について、段階的なガイドを提供しました。