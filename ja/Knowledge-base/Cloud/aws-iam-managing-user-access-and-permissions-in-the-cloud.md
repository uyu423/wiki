---
title: AWS IAM: クラウドでのユーザー アクセスとアクセス許可の管理
description: 
published: true
date: 2023-01-31T08:43:44.393Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:43:42.833Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [AWS IAM: Managing User Access and Permissions in the Cloud***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-iam-managing-user-access-and-permissions-in-the-cloud)
{.links-list}



#AWS IAM：クラウドでのユーザーアクセスと権限の管理

クラウドでユーザーのアクセスと権限の管理を担当する開発者とオペレータは、利用可能なさまざまなツールとサービスを知っている必要があります。このドキュメントでは、AWS Identity and Access Management（IAM）サービスの概要と、それを使用してクラウドでユーザーのアクセスと権限を管理する方法について説明します。

# # AWS IAMとは何ですか？

AWS Identity and Access Management（IAM）は、AWS リソースへのアクセスを安全に制御するのに役立つウェブサービスです。 IAMは、リソース自体とは別のAWSアカウントの機能です。 IAMを使用すると、ユーザーとグループを作成および管理し、権限を使用してAWSリソースへのアクセスを許可および拒否できます。

IAMは、特定の地域に限定されない汎用サービスです。すべてのAWSリージョンで世界中で利用できます。

# # AWS IAMはどのように機能しますか？

AWS IAM は、次のコンポーネントで構成されます。

- **ユーザー**：IAMユーザーは、AWSリソースにアクセスするために使用されるAWSアカウントです。 IAMユーザーは、AWSマネジメントコンソールにアクセスするために使用されるAWSアカウントとは異なります。 IAM ユーザーにはデフォルトでは権限は付与されません。 IAMユーザーに明示的に権限を付与する必要があります。

- **グループ**：IAMグループはIAMユーザーの集まりです。グループは、複数のIAMユーザーを一度に管理する方法です。 IAM グループを使用して、複数のユーザーの権限を指定できます。これは、ユーザーが多い場合、または多数のユーザーの権限を頻繁に変更する必要がある場合に便利です。

- **ポリシー**：IAMポリシーは、IAMユーザーまたはグループがどのAWSリソースで実行できるかを指定するドキュメントです。 IAM ポリシーは JSON で作成されます。

- **役割**：IAMロールは、AWSリソースへのアクセスを信頼できるエンティティに委任する方法です。ロールは、AWS 認証情報で信頼されていない IAM ユーザーまたはグループに権限を付与するために使用されます.ロールを使用して、Amazon S3やAmazon DynamoDBなどのリソースにアクセスする必要があるAWSサービスに権限を付与することもできます。

IAMは汎用サービスなので、特定の地域に限定されません。すべてのAWSリージョンで世界中で利用できます。

## IAMユーザーの作成

IAMユーザーは、AWSリソースにアクセスするために使用されるAWSアカウントです。 IAMユーザーは、AWSマネジメントコンソールにアクセスするために使用されるAWSアカウントとは異なります。 IAM ユーザーにはデフォルトでは権限は付与されません。 IAMユーザーに明示的に権限を付与する必要があります。

IAMユーザーを作成する前に、IAMグループを作成する必要があります。 IAMグループはIAMユーザーの集まりです。 IAM グループを使用して、複数のユーザーの権限を指定できます。これは、ユーザーが多い場合、または多数のユーザーの権限を頻繁に変更する必要がある場合に便利です。

IAMグループを作成したら、IAMユーザーをグループに追加できます。 IAMユーザーをグループに追加するには、iam：AddUserToGroup権限が必要です。

## IAMユーザーにポリシーを接続する

ポリシーは、IAMユーザーまたはグループがどのAWSリソースで実行できるアクションを指定するドキュメントです。 IAM ポリシーは JSON で作成されます。

次の 2 つの方法でポリシーを IAM ユーザーに関連付けることができます。

- ユーザーデータにポリシーをインライン化できます。
- ポリシーを作成してユーザーに接続できます。

ポリシーは複数のユーザーとグループに関連付けることができます。

## IAMロールの作成

IAMロールは、AWSリソースへのアクセスを信頼できるエンティティに委任する方法です。ロールは、AWS 認証情報で信頼されていない IAM ユーザーまたはグループに権限を付与するために使用されます.ロールを使用して、Amazon S3やAmazon DynamoDBなどのリソースにアクセスする必要があるAWSサービスに権限を付与することもできます。

IAMロールを作成する前に、IAMポリシーを作成する必要があります。 IAMポリシーは、IAMユーザーまたはグループがどのAWSリソースで実行できるアクションを指定するドキュメントです。 IAM ポリシーは JSON で作成されます。

IAMポリシーを作成したら、IAMロールを作成してポリシーをロールに関連付けることができます。

IAMユーザーとグループの役割をリンクまたは分離できます。

## IAM ユーザーの削除

IAM ユーザーはいつでも削除できます。 IAM ユーザーが削除されると、ユーザーのすべての権限も削除されます。 IAMユーザーを削除しても、ユーザーがアクセスできるAWSリソースは削除されません。

IAMユーザーを削除するには、iam：DeleteUser権限が必要です。

## summary

AWS Identity and Access Management（IAM）は、AWS リソースへのアクセスを安全に制御するのに役立つウェブサービスです。 IAMは、リソース自体とは別のAWSアカウントの機能です。 IAMを使用すると、ユーザーとグループを作成および管理し、権限を使用してAWSリソースへのアクセスを許可および拒否できます。

IAMは、特定の地域に限定されない汎用サービスです。すべてのAWSリージョンで世界中で利用できます。

IAMユーザーは、AWSリソースにアクセスするために使用されるAWSアカウントです。 IAMユーザーは、AWSマネジメントコンソールにアクセスするために使用されるAWSアカウントとは異なります。 IAM ユーザーにはデフォルトでは権限は付与されません。 IAMユーザーに明示的に権限を付与する必要があります。

IAMグループはIAMユーザーの集まりです。 IAM グループを使用して、複数のユーザーの権限を指定できます。これは、ユーザーが多い場合、または多数のユーザーの権限を頻繁に変更する必要がある場合に便利です。

ポリシーは、IAMユーザーまたはグループがどのAWSリソースで実行できるアクションを指定するドキュメントです。 IAM ポリシーは JSON で作成されます。

IAMロールは、AWSリソースへのアクセスを信頼できるエンティティに委任する方法です。ロールは、AWS 認証情報で信頼されていない IAM ユーザーまたはグループに権限を付与するために使用されます.ロールを使用して、Amazon S3やAmazon DynamoDBなどのリソースにアクセスする必要があるAWSサービスに権限を付与することもできます。

IAMは汎用サービスなので、特定の地域に限定されません。すべてのAWSリージョンで世界中で利用できます。