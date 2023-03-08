---
title: Kubernetes Pod: クラスターの構成要素
description: 
published: true
date: 2023-02-17T18:05:39.130Z
tags: 
editor: markdown
dateCreated: 2023-01-30T14:32:40.140Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Kubernetes Pods: The Building Blocks of Your Cluster***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-pods-the-building-blocks-of-your-cluster)
{.links-list}



# Kubernetes Pod: クラスターのビルディングブロック

Kubernetes ポッドは、Kubernetes クラスターでデプロイ可能な最小単位であり、クラスターのビルディングブロックです。ポッドは一時的なものであるため、指定された時間に実行される保証はなく、必要に応じて削除して再作成できます。

PodはKubernetesコントロールプレーンによって管理され、ユーザーも知らない間にクラッシュして再起動することができます。これがKubernetesを使用する利点の1つです。クラスタ内の個々のシステムを抽象化すると、クラスタ全体を単一のエンティティとして扱うことができます。

ポッドには1つ以上のコンテナが含まれており、アプリケーション、データベース、またはKubernetesクラスタで実行する必要があるその他のエントリをホストするために使用できます。ポッドは常に同じノードに配置され共同予約されているため、ボリュームやネットワークインターフェイスなどのリソースを共有できます。

ポッドを作成するときは、コンテナイメージや必要な設定など、ポッドに必要な状態を指定する必要があります。その後、Kubernetesはポッドを希望の状態に保ちます。

PodはKubernetesのデフォルトの配布単位であり、通常はステートレスアプリケーションをホストするために使用されます。 Kubernetesでステートフルアプリケーションを実行する必要がある場合は、StatefulSetを使用する必要があります。

## パードの作成

`kubectl`コマンドラインツールを使用してポッドを作成したり、マニフェストファイルを使用したりできます。

### `kubectl`を使う

`kubectl`を使ってポッドを生成するには、 `run`コマンドを使うことができます。たとえば、 `nginx`コンテナイメージを実行するポッドを作成するには、次のコマンドを使用します。

```
kubectl run nginx --image=nginx
```

これにより、単一の `nginx`コンテナを持つポッドが作成されます。複数のコンテナでポッドを作成するには、 `run-container`コマンドを使用できます。

```
kubectl run-container nginx-container --image=nginx --image=mysql
```

### マニフェストファイルの使用

あるいは、 `Pod`マニフェストファイルを作成し、 `kubectl` `create`コマンドを使ってポッドを生成することもできます。たとえば、次のマニフェストファイルは単一の `nginx`コンテナを持つポッドを作成します。

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx
```

その後、次のコマンドを実行してポッドを作成できます。

```
kubectl create -f nginx.yaml
```

## Podを削除

ポッドは `kubectl` `delete` コマンドを使って削除できます。たとえば、前のセクションで作成した `nginx` ポッドを削除するには、次のコマンドを使用できます。

```
kubectl delete pod nginx
```

## ポッドの状態

ポッドは次のいずれかの状態になります。

- **Pending**：ポッドが作成されましたが、1つ以上のコンテナが起動されませんでした。
- **実行中**：ポッドとすべてのコンテナが実行中です。
- **Succeeded**: Pod が操作を正常に完了し、すべてのコンテナが `Exited` 状態です。
- **Failed**: Podが失敗し、すべてのコンテナが`Exited`状態です。
- **不明**：ポッドの状態を確認できません。

##結論

Kubernetesポッドはクラスタのビルディングブロックであり、アプリケーション、データベース、またはKubernetesクラスタで実行する必要がある他のエントリをホストするために使用されます。ポッドは常に同じノードに配置され共同予約されているため、ボリュームやネットワークインターフェイスなどのリソースを共有できます。

ポッドを作成するときは、コンテナイメージや必要な設定など、ポッドに必要な状態を指定する必要があります。その後、Kubernetesはポッドを希望の状態に保ちます。

PodはKubernetesのデフォルトの配布単位であり、通常はステートレスアプリケーションをホストするために使用されます。 Kubernetesでステートフルアプリケーションを実行する必要がある場合は、StatefulSetを使用する必要があります。