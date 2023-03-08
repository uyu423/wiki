---
title: Kubernetes CLI: コマンドラインからクラスターを操作する
description: 
published: true
date: 2023-02-17T18:16:51.436Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:43:36.149Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Kubernetes CLI: Working with Your Cluster from the Command Line***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-cli-working-with-your-cluster-from-the-command-line)
{.links-list}

    

# Kubernetes CLI: コマンドラインでのクラスター操作

Kubernetesコマンドラインインターフェイス（CLI）であるcfsslは、ユーザーがコマンドラインからKubernetesクラスタを操作できるようにするツールです。この資料では、cfsslツールをインストールおよび設定する方法、およびそれを使用してKubernetesクラスターを管理する方法の概要について説明します。

## Cfsslツールのインストール

Cfsslツールは、任意のLinuxまたはmacOSシステムにインストールできます。 Linux に cfssl をインストールするには、次のコマンドを使用します。

```
$curl -LO https://storage.googleapis.com/kubernetes-release/cfssl/cfssl_linux-amd64.tar.gz
$tar -xzf cfssl_linux-amd64.tar.gz
$mv cfssl_linux-amd64/bin/cfssl /usr/local/bin/
$rm -rf cfssl_linux-amd64
```

macOS に cfssl をインストールするには、次のコマンドを使用します。

```
$ brew install cfssl
```

## Cfsslツールの設定

cfsslツールをインストールしたら、環境変数を設定する必要があります。 CFSSL_CA 環境変数は、cfssl が使用する CA 証明書のパスを指定します。 CFSSL_CERT 環境変数は、cfssl が使用するクライアント証明書のパスを指定します。 CFSSL_KEY環境変数は、cfsslで使用されるクライアントキーのパスを指定します。

cfssl ツールを設定するには、次のコマンドを使用します。

```
$export CFSSL_CA=/path/to/ca.pem
$export CFSSL_CERT=/path/to/client.pem
$export CFSSL_KEY=/path/to/client-key.pem
```

## Kubernetesクラスターの作成

cfsslツールをインストールして設定したら、それを使用してKubernetesクラスターを作成できます。 Kubernetes クラスターを作成するには、次のコマンドを使用します。

```
$cfssl create-cluster -size=3 -server=https://kubernetes.default.svc.cluster.local:443 -ca=ca.pem -ca-key=ca-key.pem
```

このコマンドは、3つのノードを持つKubernetesクラスタを作成します。サーバーフラグは、Kubernetes APIサーバーのURLを指定します。 ca フラグは、cfssl が使用する CA 証明書のパスを指定します。 ca-key フラグは、cfssl が使用する CA キーのパスを指定します。

## Kubernetesクラスターの削除

Kubernetes クラスターを削除するには、次のコマンドを使用します。

```
$cfssl delete-cluster -name=my-cluster
```

このコマンドは、my-clusterという名前のKubernetesクラスターを削除します。

## Kubernetesクラスターのリスト

cfssl で作成された Kubernetes クラスターを一覧表示するには、次のコマンドを使用します。

```
$cfssl list-clusters
```

このコマンドは、cfsslで作成されたすべてのKubernetesクラスターを一覧表示します。

## クラスタ情報の取得

Kubernetes クラスタに関する情報を取得するには、次のコマンドを使用します。

```
$cfssl get-cluster -name=my-cluster
```

このコマンドは、my-clusterという名前のKubernetesクラスターに関する情報を取得します。

## Kubernetesクラスタの更新

Kubernetes クラスターを更新するには、次のコマンドを使用します。

```
$cfssl update-cluster -name=my-cluster -size=5
```

このコマンドは、my-clusterという名前のKubernetesクラスターのサイズを5つのノードに更新します。

## Kubernetesクラスタへのノードの追加

Kubernetes クラスターにノードを追加するには、次のコマンドを使用します。

```
$cfssl add-node -name=my-cluster -size=3
```

このコマンドは、my-clusterという名前のKubernetesクラスタに3つのノードを追加します。

## Kubernetesクラスタからノードを削除する

Kubernetes クラスターからノードを削除するには、次のコマンドを使用します。

```
$cfssl delete-node -name=my-cluster -size=3
```

このコマンドは、my-clusterという名前のKubernetesクラスターから3つのノードを削除します。

## Kubernetesクラスタ拡張

Kubernetes クラスターを拡張するには、次のコマンドを使用します。

```
$cfssl scale-cluster -name=my-cluster -size=5
```

このコマンドは、my-clusterという名前のKubernetesクラスターを5つのノードに拡張します。

## Kubernetesクラスタのサイズ変更

Kubernetes クラスターのサイズを変更するには、次のコマンドを使用します。

```
$cfssl resize-cluster -name=my-cluster -size=3
```

このコマンドは、my-clusterという名前のKubernetesクラスターのサイズを3つのノードに調整します。

## Kubernetesクラスタの状態を取得する

Kubernetes クラスターの状態を確認するには、次のコマンドを使用します。

```
$cfssl get-status -name=my-cluster
```

このコマンドは、my-clusterという名前のKubernetesクラスターの状態を取得します。

##助けを得る

特定のコマンドのヘルプを表示するには、次のコマンドを使用します。

```
$cfssl help <command>
```

このコマンドは、cfssl コマンドのヘルプを取得します。

## 外部リンク

- [Cfssl ドキュメント] (https://pkg.go.dev/mod/github.com/cloudflare/cfssl?tab=doc)
- [キューバネティス文書](https://kubernetes.io/docs/home/)