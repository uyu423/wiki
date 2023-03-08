---
title: AWS Auto Scaling: 負荷に基づいてクラウド リソースを自動的にスケーリングする
description: 
published: true
date: 2023-01-31T20:23:51.839Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:23:50.279Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [AWS Auto Scaling: Automatically Scaling Cloud Resources Based on Load***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-auto-scaling-automatically-scaling-cloud-resources-based-on-load)
{.links-list}


# AWS Auto Scaling: 負荷に応じて自動的にクラウドリソースを拡張

Auto Scalingは、組織が需要に応じてAmazon Web Services（AWS）リソースを自動的に拡張または縮小し、コストを削減し、必要に応じてリソースを使用できるようにするクラウドコンピューティング機能です。

AWS Auto Scaling は、必要に応じて AWS リソースを使用でき、アイドルリソースの料金を支払わないようにする費用対効果の高い方法です。トラフィックの急増に対処するために必要なリソースを確保することで、アプリケーションのパフォーマンスを向上させる良い方法でもあります。

Auto Scalingは、Amazon Elastic Compute Cloud（EC2）、Amazon Elastic Container Service（ECS）、Amazon Relational Database Service（RDS）、その他のAWSサービスの機能です。

Auto Scalingを設定するときにAWSが維持する最小インスタンスと最大インスタンス数を指定します。その後、AWS はこれらの制限内を維持するために必要に応じてインスタンスを追加または削除します。 AWS がリソースを拡張または縮小する方法を決定する調整ポリシーを指定することもできます。たとえば、CPU使用率が80％を超える場合は、AWSがより多くのインスタンスを追加するように指定できます。

AWS Auto Scalingは、AWS料金を節約し、アプリケーションのパフォーマンスを向上させるための優れた方法です。 Auto Scalingの仕組みを理解して正しく設定することが重要ですが、正しく使用しないと、意図しない結果が生じる可能性があります。

## AWS Auto Scalingの仕組み

AWS Auto Scaling は、「フリット」と呼ばれる EC2 インスタンスグループをメンテナンスして動作します。このフリットは、フリットを拡張または縮小する方法を決定する設定の集まりである「自動拡張グループ」（ASG）によって管理されます。

ASG には、最小インスタンスと最大インスタンス数、必要な容量、調整ポリシーなど、複数の設定可能な設定が含まれています。

ASGを作成するときに維持する最小および最大インスタンス数を指定する必要があります。その後、ASG はこれらの制限内に維持するために必要に応じてフリットを拡張または縮小します。

また、ASG が所与の時間に保持するインスタンス数である所望の容量を指定することもできる。 ASGは、必要に応じてフリットを拡大または縮小して、この目的の容量に達します。

ASGには複数の調整ポリシーも含まれています。これらの方針は、ASGが需要の変化に対応してフリットを拡大または縮小する方法を決定します。

たとえば、CPU使用率が80％を超える場合は、さらにインスタンスを追加する調整ポリシーを指定できます。このポリシーは、CPU使用率が80％を超えるとASGにフリットにさらにインスタンスを追加させることを可能にします。

また、RPS（1秒あたりの要求数）またはBPS（1秒あたりのバイト数）の変更に応じて、ASGがセットを調整する方法を決定する調整ポリシーを指定できます。

Auto Scalingは、AWSのコストを削減し、アプリケーションのパフォーマンスを向上させる優れた方法です。 Auto Scalingの仕組みを理解して正しく設定することが重要ですが、正しく使用しないと、意図しない結果が生じる可能性があります。

## AWS Auto Scalingの設定

AWS Auto Scaling は、Amazon EC2、Amazon ECS、Amazon RDS、その他の AWS サービスの機能です。

Auto Scalingを設定するときにAWSが維持する最小インスタンスと最大インスタンス数を指定します。その後、AWS はこれらの制限内を維持するために必要に応じてインスタンスを追加または削除します。 AWS がリソースを拡張または縮小する方法を決定する調整ポリシーを指定することもできます。たとえば、CPU使用率が80％を超える場合は、AWSがより多くのインスタンスを追加するように指定できます。

Auto Scalingの仕組みを理解して正しく設定することが重要ですが、正しく使用しないと、意図しない結果が生じる可能性があります。

たとえば、CPU使用率が80％以上の場合にインスタンスを追加するように調整ポリシーを指定したが、追加できるインスタンス数を制限する方法がない場合、AWSはインスタンスを追加し続けます。指定したインスタンスの最大数に達しました。これにより、予想外に高いAWS料金が請求される可能性があります。

これを防ぐために「拡張計画」を使用することができます。調整計画は、ASG がセットを拡張または縮小する方法を決定する設定の集合です。

調整計画には、最小インスタンスと最大インスタンス数、必要な容量、調整ポリシーなど、複数の設定可能な設定が含まれます。

調整計画を使用して、指定した期間に追加できるインスタンスの最大数を指定して、追加できるインスタンスの数を制限できます。たとえば、24時間に10を超えるインスタンスを追加できないように指定できます。

調整計画を使用して、保守する必要があるインスタンスの最小数を指定して、削除できるインスタンスの数を制限することもできます。たとえば、少なくとも2つのインスタンスを常に維持するように指定できます。

##結論

AWS Auto Scaling は、必要に応じて AWS リソースを使用でき、アイドルリソースの料金を支払わないようにする費用対効果の高い方法です。トラフィックの急増に対処するために必要なリソースを確保することで、アプリケーションのパフォーマンスを向上させる良い方法でもあります。

Auto Scalingは、Amazon EC2、Amazon ECS、Amazon RDS、その他のAWSサービスの機能です。

Auto Scalingを設定するときにAWSが維持する最小インスタンスと最大インスタンス数を指定します。その後、AWS はこれらの制限内を維持するために必要に応じてインスタンスを追加または削除します。 AWS がリソースを拡張または縮小する方法を決定する調整ポリシーを指定することもできます。

Auto Scalingの仕組みを理解して正しく設定することが重要ですが、正しく使用しないと、意図しない結果が生じる可能性があります。

AWS Auto Scaling の詳細については、次のリソースを参照してください。

- [AWS Auto Scaling ドキュメント] (https://docs.aws.amazon.com/autoscaling/latest/userguide/WhatIsAutoScaling.html)
- [Auto Scaling グループ] (https://docs.aws.amazon.com/autoscaling/latest/userguide/AutoScalingGroups.html)
- [拡張計画]（https://docs.aws.amazon.com/autoscaling/latest/userguide/ScalingPlans.html）