---
title: AWS Athena: サーバーレスコンピューティングを使用して S3 データで SQL クエリを実行する
description: 
published: true
date: 2023-01-31T08:57:38.617Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:57:36.969Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [AWS Athena: Running SQL Queries on S3 Data with Serverless Computing***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-athena-running-sql-queries-on-s3-data-with-serverless-computing)
{.links-list}
 

#AWS Athena：サーバーレスコンピューティングでS3データからSQLクエリを実行する

## はじめに

クラウドコンピューティングの最大の利点の1つは、需要に応じてサービスを拡張または縮小できることです。これは、年間の特定の時期に使用量が急増するビジネスにとって特に重要です。サーバーレスコンピューティングは、クラウドプロバイダーがサーバーを実行し、顧客が使用量に応じて料金を支払うクラウドコンピューティング実行モデルです。

AWS Athenaは、標準SQLを使用してAmazon S3のデータを簡単に分析できるサーバーレス対話型クエリサービスです。 Athenaは使いやすいです。インフラストラクチャを設定または管理する必要はありません。データはS3に保存されるため、可用性と耐久性に優れています。 Athenaはクエリを並列に実行して自動的に拡張するため、大規模なデータセットと複雑なクエリがある場合でも結果は高速です。

この記事では、AWS Athenaを使用してS3に保存されているデータを設定してクエリする方法について説明します。また、Athenaを使用する利点と欠点についても見てみましょう。

# # AWS Athenaの設定

Athenaを使用する前に、AWSでいくつか設定する必要があります。

まず、データを保存するS3バケットを作成する必要があります。 AWSマネジメントコンソールを使用してこれを行うか、次のAWS CLIコマンドを使用できます。

```
aws s3 mb s3://{bucket-name}
```

{bucket-name} をバケット名に置き換えます。

次に、Athenaでデータベースとテーブルを作成する必要があります。 AthenaはApache Hiveメタストアを使用して、データベースとテーブルに関する情報を保存します。

AWSマネジメントコンソールを使用してデータベースとテーブルを作成するか、次のAthenaクエリエディタコマンドを使用できます。

```sql
CREATE DATABASE {database-name};

CREATE TABLE {table-name}
（
  {column-name} {data-type}
)
ROW FORMAT SERDE 'org.apache.hive.hcatalog.data.JsonSerDe'
WITH SERDEPROPERTIES(
  'serialization.format' = '1'
)
STORED AS {file-format};
```

以下を交換してください。

- {database-name}: データベース名
- {table-name}: テーブル名
- {column-name}: 列名
- {data-type}: 列のデータ型
- {file-format}：データのファイル形式（例： 'TEXTFILE'、 'PARQUET'など）

データベースとテーブルを作成したら、データをテーブルにロードする必要があります。 AWSマネジメントコンソールを使用するか、次のAWS CLIコマンドを使用できます。

```
aws s3 cp {s3-path} {local-path} --recursive
```

以下を交換してください。

- {s3-path}: S3 のデータパス (例: s3://mybucket/data/)
- {local-path}: データをコピーするローカルディレクトリへのパス

# # Athenaによるデータの照会

これでデータが設定されたので、Athenaでクエリを開始できます。 AWSマネジメントコンソールを使用するか、Athenaクエリエディタを使用してこれを実行できます。

Athenaクエリエディタを使用するには、エディタを開き、クエリするデータベースとテーブルを選択します。次に、クエリエディタにSQLクエリを入力し、[クエリの実行]をクリックします。

Athenaはクエリを実行し、結果を返します。

後で使用するためにクエリを保存することもできます。これを行うには、保存するクエリを選択して[保存]ボタンをクリックします。クエリ名と説明を入力し、[保存]をクリックします。

## Athenaを使用する利点

以下を含むAthenaを使用すると、多くの利点があります。

- アテナは使いやすいです。インフラストラクチャを設定または管理する必要はありません。
- データはS3に保存されるため、可用性と耐久性に優れています。
- Athenaはクエリを並列に実行して自動的に拡張されるため、大規模なデータセットと複雑なクエリがある場合でも結果が速くなります。
- Athenaはサーバーレスなので、実行したクエリに対してのみ支払います。容量計画やサーバー管理について心配する必要はありません。

## Athenaの使用の欠点

Athenaの使用には、次のようないくつかの欠点もあります。

- Athenaはリアルタイムデータ分析を必要とするユースケースには適していません。 S3のデータは通常数分または数時間ごとに更新されるため、Athenaクエリはデータが更新された直後に結果を返しません。
- Athenaは非常に短い待ち時間のデータ分析を必要とするユースケースには適していません。 S3のデータは通常数分または数時間ごとに更新されるため、Athenaクエリはデータが更新された直後に結果を返しません。
- Athenaは、高スループットデータ分析を必要とするユースケースには適していません。 S3のデータは通常数分または数時間ごとに更新されるため、Athenaクエリはデータが更新された直後に結果を返しません。

## 結論

この記事では、AWS Athenaを使用してS3に保存されているデータを設定してクエリする方法について説明しました。また、Athenaの使用のいくつかの利点と欠点も見てきました。