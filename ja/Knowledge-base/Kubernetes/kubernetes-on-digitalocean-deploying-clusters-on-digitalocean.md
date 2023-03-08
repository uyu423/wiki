---
title: DigitalOcean での Kubernetes: DigitalOcean でのクラスターのデプロイ
description: 
published: true
date: 2023-02-17T18:02:57.361Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:26:55.601Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Kubernetes on DigitalOcean: Deploying Clusters on DigitalOcean***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-digitalocean-deploying-clusters-on-digitalocean)
{.links-list}


#DigitalOceanのKubernetes：DigitalOceanにクラスタをデプロイする

Kubernetesは、コンテナ化されたアプリケーションの展開、拡張、および管理を自動化するオープンソースコンテナオーケストレーションプラットフォームです。移植可能でスケーラブルでクラスタ管理ソリューションを構築するための基盤を提供します。

DigitalOceanは、仮想プライベートサーバー（VPS）やその他のクラウドサービスを提供するクラウドコンピューティングプラットフォームです。 Webアプリケーションとマイクロサービスをホストするために広く使用されている選択肢です。

この資料では、DigitalOcean に Kubernetes クラスターをデプロイする方法の概要を説明します。リソースのプロビジョニング、ネットワーク構成、およびアプリケーションのデプロイメントをカバーします。

##リソースプロビジョニング

DigitalOceanは、簡単にリソースをプロビジョニングし、Kubernetesクラスタを展開するためのKubernetesサービスを提供します。最初のステップは Kubernetes クラスターを作成することです。これはコントロールパネルまたはAPIを介して行うことができます。

クラスターが作成されたら、クラスターにノードを追加する必要があります。ノードは手動または自動で追加できます。自動ノードプロビジョニングは、3つ以上のノードを持つクラスタで使用できます。

## ネットワーク構成

DigitalOceanのKubernetesクラスタは、デフォルトでプライベートネットワークと一緒に展開されます。このネットワークはパブリックインターネットから隔離され、クラスタ内でのみアクセスできます。

インターネットからサービスにアクセスするには、ゲートウェイを構成する必要があります。これはKubernetesダッシュボードまたはAPIを介して行うことができます。

オンプレミスサービスにアクセスする必要がある場合は、VPNを設定する必要があります。 DigitalOceanは、オンプレミスリソースへの接続に使用できるIPsec VPNサービスを提供します。

## アプリケーションのデプロイ

Kubernetes クラスターにアプリケーションをデプロイするには、デプロイメントを作成する必要があります。これはKubernetesダッシュボードまたはAPIを介して行うことができます。

展開が作成されたら、使用するコンテナイメージと公開するポートを指定する必要があります。環境変数やその他のオプションを指定することもできます。

デプロイが作成されたら、サービスを作成する必要があります。これにより、展開が外部の世界にさらされます。 KubernetesダッシュボードまたはAPIを介してサービスを作成できます。

サービスが作成されたら、サービスタイプ（LoadBalancer、ClusterIP、またはNodePort）と公開するポートを指定する必要があります。サービス名などの他のオプションを指定することもできます。

##結論

この記事では、DigitalOcean で Kubernetes クラスターをデプロイする基本事項について説明します。リソースをプロビジョニングし、ネットワーキングを構成し、アプリケーションをデプロイする方法を示しました。