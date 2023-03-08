---
title: 永続ボリュームを使用して Kubernetes にステートフル アプリケーションをデプロイする
description: 
published: true
date: 2023-01-31T14:43:53.490Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:43:51.917Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Deploying Stateful Applications on Kubernetes with Persistent Volumes***English** version of this document is available*](/en/Knowledge-base/Kubernetes/deploying-stateful-applications-on-kubernetes-with-persistent-volumes)
{.links-list}



# 永続ボリュームを使用した Kubernetes へのステートフルアプリケーションのデプロイ

Kubernetesは、開発者がコンテナ化されたアプリケーションを大規模に展開および管理できるようにする強力なコンテナオーケストレーションツールです。 Kubernetesの主な機能の1つは、ステートフルアプリケーション用の永続ストレージを提供することです。これは、データベースなどの障害が発生した場合や再起動してもデータが持続する必要があるアプリケーションに不可欠です。

この記事では、永続ボリュームを持つKubernetesにステートフルアプリケーションをデプロイする方法について説明します。次のトピックを扱います。

- 永久ボリュームとは何ですか？重要な理由は何ですか？
- 永続ボリュームを作成してKubernetes Podに接続する方法
- ステートフルアプリケーションで永続ボリュームを使用する方法

##永久ボリュームとは何ですか？なぜ重要ですか？

永久ボリューム（PV）は、Kubernetesポッドのデータを保存するために使用されるブロックデバイスです。ポッドが削除されてもPVのデータは削除されず、他のポッドで再利用できます。したがって、PVはデータベースなどのステートフルアプリケーション用のデータを保存するのに理想的です。

PV は障害や再起動後もデータを保持できるため重要です。これは、データベースなどのデータを永続化する必要があるアプリケーションに不可欠です。 PVはまた、複数のPod間でデータを共有できるようにするため、複数のインスタンス間でデータを同期する必要があるアプリケーションに役立ちます。

## 永続ボリュームを作成して Kubernetes ポッドに接続する方法

PV生成は2段階プロセスです。まず、kubectlコマンドラインツールを使用してPVオブジェクトを作成する必要があります。このオブジェクトは、ストレージのサイズや種類などのPVのパラメータを定義します。次に、PodでPVを使用する方法を定義するPVCオブジェクトを作成する必要があります。

次の例では、ストレージが1 GBのPVを作成します。

```
kubectl create -f pv.yaml
```

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  名前: pv-1
  labels:
    type: local
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/tmp/data"
```

次の例では、前の例で作成したPVを使用するPVCを作成します。

```
kubectl create -f pvc.yaml
```

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  名前: pvc-1
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  セレクター：
    matchLabels:
      type: local
```

その後、PVCを使用してPVを使用するポッドを作成できます。

```
kubectl create -f pod.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-1
spec:
  containers:
  - name: container-1
    image: busybox
    command: ["sleep", "3600"]
    volumeMounts:
    - name: pv-1
      mountPath: "/data"
  volumes:
  - name: pv-1
    persistentVolumeClaim:
      claimName: pvc-1
```

##ステートフルアプリケーションで永続ボリュームを使用する方法

データベースなどのステートフルアプリケーションは、永続ボリュームを使用してKubernetesにデプロイできます。次の例は、PV を使用して Kubernetes に MySQL データベースをデプロイする方法を示しています。

```
kubectl create -f mysql-pv.yaml
```

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mysql-pv-1
  labels:
    type: local
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath：
    path: "/tmp/data"
```

```
kubectl create -f mysql-pvc.yaml
```

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pvc-1
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  セレクター：
    matchLabels:
      type: local
```

```
kubectl create -f mysql-pod.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mysql-pod-1
spec:
  containers:
  - name: mysql-container-1
    image: mysql:5.6
    env：
    - name: MYSQL_ROOT_PASSWORD
      value: "secret"
    - name: MYSQL_USER
      value: "user"
    - name: MYSQL_PASSWORD
      value: "secret"
    - name: MYSQL_DATABASE
      value: "db"
    ports:
    - containerPort: 3306
      name: mysql
    volumeMounts:
    - name: mysql-data
      mountPath: /var/lib/mysql
  volumes:
  - name: mysql-data
    persistentVolumeClaim:
      claimName: mysql-pvc-1
```

上記の例では、1 GBのストレージを持つPVとPVを使用するPVCを作成しました。次に、MySQLコンテナを含み、PVを/var/lib/mysqlにマウントするポッドを作成しました。

MySQLコンテナはPVを使用してデータを保存します。ポッドが削除されても、PVのデータは削除されず、他のポッドで再利用できます。したがって、PVはデータベースなどのステートフルアプリケーション用のデータを保存するのに理想的です。

##結論

この記事では、永続ボリュームを持つKubernetesにステートフルアプリケーションをデプロイする方法について説明しました。 PVを使用してステートフルアプリケーションのデータを保存する方法と、ステートフルアプリケーションでPVを使用する方法について説明しました。