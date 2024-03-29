---
title: Kubernetes デプロイメントでのローリング アップデートとロールバック
description: 
published: true
date: 2023-01-31T11:36:19.776Z
tags: 
editor: markdown
dateCreated: 2023-01-31T11:36:18.138Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Rolling Updates and Rollbacks with Kubernetes Deployments***English** version of this document is available*](/en/Knowledge-base/Kubernetes/rolling-updates-and-rollbacks-with-kubernetes-deployments)
{.links-list}



# Kubernetes 展開によるローリング更新とロールバック

本番環境では、ダウンタイムなしでアプリケーションを更新する必要があることがよくあります。クーバーネティスはこれを助けるために「ローリングアップデート」と呼ばれる機能を提供します。このガイドでは、「ローリングアップデート」とは何か、それをどのように使用するかについて説明します。

##ローリングアップデートとは？

ローリングアップデートは、ダウンタイムを最小限に抑えたり、まったくしなくてもソフトウェアをアップデートする方法です。この方法では、新しいバージョンのソフトウェアが徐々にサーバーに展開されます。これにより、一部のサーバーが更新されても常に機能するソフトウェアバージョンを使用できます。

##ローリングアップデートはどのように機能しますか？

ローリング更新は、展開内の個々のポッドを更新することによって実行されます。 Kubernetesは一度に1つずつポッドを更新します。これにより、常に機能するソフトウェアバージョンを使用できます。

## ローリングアップデートはどうすればよいですか？

ローリング更新を実行するには、展開の「仕様」を新しいイメージで更新する必要があります。その後、Kubernetesは一度に1つずつポッドを更新します。

##アップデートに問題がある場合は？

アップデートに問題がある場合は、展開を以前のバージョンにロールバックできます。これを行うには、デプロイの「仕様」を前のイメージに更新する必要があります。その後、Kubernetesは一度に1つずつポッドを更新します。

##結論

ローリングアップデートは、ダウンタイムを最小限に抑えるか、中断せずにソフトウェアをアップデートする良い方法です。クーバーネティスは「ローリングアップデート」機能でローリングアップデートを簡単に行うことができます。