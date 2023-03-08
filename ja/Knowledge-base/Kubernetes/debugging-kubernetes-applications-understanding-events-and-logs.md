---
title: Kubernetes アプリケーションのデバッグ: イベントとログについて
description: 
published: true
date: 2023-02-17T18:16:17.276Z
tags: 
editor: markdown
dateCreated: 2023-01-31T00:43:18.511Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Debugging Kubernetes Applications: Understanding Events and Logs***English** version of this document is available*](/en/Knowledge-base/Kubernetes/debugging-kubernetes-applications-understanding-events-and-logs)
{.links-list}


#Kubernetesアプリケーションのデバッグ：イベントとログについて

Kubernetesは強力なオーケストレーションツールですが、ここで実行されているアプリケーションをデバッグするのは難しいかもしれません。この記事では、Kubernetesアプリケーションをデバッグするための2つの重要なツールであるイベントとログについて説明します。

## イベント

イベントは、Kubernetesクラスタ内で何が起こっているのかを見やすくするのに最適な方法です。イベントを表示するには、 `kubectl`コマンドを使用してください。

```
kubectl get events
```

これにより、タイムスタンプ、タイプなどとともにクラスタ内のすべてのイベントのリストが返されます。

イベントはラベルでフィルタリングできるため、特定のポッドに関連するイベントのみを表示するには、 `--selector`フラグを使用できます。

```
kubectl get events --selector=app=nginx
```

特定の名前空間のイベントを表示することもできます。

```
kubectl get events --namespace=default
```

最後に、 `--since`フラグを使用して、特定の時間以降に発生したイベントのみを取得できます。

```
kubectl get events --since=2019-01-01T00:00:00Z
```

## ログ

イベントに加えて、ログはKubernetesアプリケーションをデバッグするためのもう1つの重要なツールです。ポッドのログを取得するには、 `kubectl`コマンドを使用してください。

```
kubectl logs POD_NAME
```

`POD_NAME`をログをインポートしたいPodの名前に置き換えます。

展開内のすべてのポッドのログを取得することもできます。

```
kubectl logs DEPLOYMENT_NAME
```

`DEPLOYMENT_NAME`をログをインポートしたい配布の名前に置き換えます。

最後に、 `--since`フラグを使用して、特定の時間以降に生成されたログのみを取得できます。

```
kubectl logs --since=2019-01-01T00:00:00Z
```

##結論

この記事では、Kubernetesアプリケーションをデバッグするための2つの重要なツールであるイベントとログについて説明しました。イベントは、Kubernetesクラスタ内で何が起こっているのかを見やすくするための優れた方法であり、ログはアプリケーションの問題を解決するために使用できます。