---
title: Kubernetes 拡張 API: クラスターの機能を強化する
description: 
published: true
date: 2023-02-17T18:17:23.811Z
tags: 
editor: markdown
dateCreated: 2023-01-31T02:23:22.399Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Kubernetes Extension APIs: Enhancing the Functionality of Your Cluster***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-extension-apis-enhancing-the-functionality-of-your-cluster)
{.links-list}



#Kubernetes拡張API：クラスタの機能強化

Kubernetesは、コンテナ化されたアプリケーションの展開、拡張、および管理を自動化するためのオープンソースシステムです。アプリケーションを構成するコンテナを論理単位でグループ化することで、簡単に管理および検索できます。 Kubernetesは、ストレージオーケストレーション、ネットワーキング、およびセキュリティのためのメカニズムも提供します。

Kubernetes機能拡張は人気のあるトピックであり、これを行う方法はいくつかあります。この記事では、Kubernetes Extension APIに焦点を当てます。それらが何であるか、どのように機能するのか、そしてなぜ使用すべきかについて議論します。また、開始できるようにいくつかのサンプルコードを提供します。

## Kubernetes拡張APIとは何ですか？

Kubernetes Extension APIは、Kubernetesクラスターの機能を拡張できる一連のAPIです。コアコードを変更せずにKubernetesに新機能を追加する方法を提供します。

拡張APIはCRD（CustomResourceDefinitions）として実装されています。 CRD は Kubernetes に新しいリソースを追加する方法です。リソースは、Podやサービスなど、Kubernetesで管理できるオブジェクトです。 CRDを使用すると、Kubernetesが管理できる新しいリソースを定義できます。

## Kubernetes Extension APIはどのように機能しますか？

Kubernetes Extension APIはCRD（CustomResourceDefinitions）として実装されています。 CRD は Kubernetes に新しいリソースを追加する方法です。リソースは、Podやサービスなど、Kubernetesで管理できるオブジェクトです。 CRDを使用すると、Kubernetesが管理できる新しいリソースを定義できます。

各CRDには、名前、タイプ、および属性を含むリソースの説明があります。 Kubernetesはこの情報を使用して新しいリソースを作成します。その後、Kubernetes APIを使用してこの新しいリソースを管理できます。

## Kubernetes Extension APIを使用するのはなぜですか？

Kubernetes Extension APIは、コアコードを変更せずにKubernetesに新機能を追加する方法を提供します。これは、新しい機能を追加したい場合や、クラスタの信頼性に影響を与えずに新しいコードを試したい場合に便利です。

拡張 API は、Kubernetes コミュニティとコードを共有する方法も提供します。コードが他の人に役立つと思われる場合は、Kubernetesに含めるように送信できます。

## サンプルコード

以下は、CustomResourceDefinitionの簡単な例です。

```
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  name: mycrd.example.com
spec:
  scope: Cluster
  group: example.com
  version: v1
  names:
    plural: mycrds
    singular: mycrd
    kind: MyCrd
    shortNames:
    - crd
  validation:
    openAPIV3Schema:
      description: MyCrds are ..."
      type: object
      properties:
        spec:
          type: object
          properties:
            size:
              type: integer
              minimum: 1
              maximum: 100
          required:
          - size
  subresources:
    status: {}
```

このCRDは「MyCrd」というリソースを定義します。このリソースには、1から100の整数である「サイズ」という属性があります。

Kubernetes API を使用して MyCrds を作成、更新、削除できます。

```
#Create a MyCrd
apiVersion: example.com/v1
kind: MyCrd
metadata:
  name: mycrd-1
spec:
  size: 10

#Update a MyCrd
apiVersion: example.com/v1
kind: MyCrd
metadata:
  name: mycrd-1
spec:
  size: 20

#Delete a MyCrd
apiVersion: example.com/v1
kind: MyCrd
metadata:
  name: mycrd-1
spec:
  size: 0
```

##結論

Kubernetes Extension APIは、コアコードを変更せずにKubernetesに新機能を追加する方法を提供します。 Kubernetesに新しいリソースを追加する方法であるCRD（CustomResourceDefinitions）として実装されています。各CRDには、名前、タイプ、および属性を含むリソースの説明があります。 Kubernetesはこの情報を使用して新しいリソースを作成します。

Kubernetes Extension API を使用すると、Kubernetes に新しい機能を追加したり、クラスターの信頼性に影響を与えずに新しいコードを試すことができます。コードが他の人に役立つと思われる場合は、Kubernetesに含めるように送信できます。