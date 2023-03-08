---
title: Docker Compose Networking: コンテナーをネットワークに接続する
description: 
published: true
date: 2023-01-31T10:23:49.451Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:23:47.444Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Docker Compose Networking: Connecting Containers with Networks***English** version of this document is available*](/en/Knowledge-base/Docker/docker-compose-networking-connecting-containers-with-networks)
{.links-list}



#Docker Composeネットワーキング：コンテナとのネットワーク接続

Docker Composeファイルの `network`キーは、コンテナが接続する必要があるネットワークを指定するために使用されます。デフォルトでは、コンテナは `default` ネットワークに接続されます。

Composeで使用できる3種類のネットワークは、ブリッジ、ホスト、およびなしです。

##脚

デフォルトのネットワークタイプはブリッジです。このタイプのネットワークは、ホストの内部にプライベートネットワークを作成します。

ブリッジネットワークのコンテナは、ポートをホストに公開することなく互いに通信できます。

##オーガナイザー

ホストネットワークタイプは、コンテナとDockerホスト間の分離を排除し、ホストのネットワーキングを直接使用します。

これは、ホストネットワークのコンテナがポートを外部に公開することなく互いに通信できることを意味します。

## なし

なしネットワークタイプは、ネットワークに接続されていないコンテナを作成するために使用されます。

これは開発やテスト目的に役立ちます。

## ネットワークとコンテナの接続

コンテナを互いに接続するには、同じネットワーク上にある必要があります。

`network`キーは、コンテナが接続する必要があるネットワークを指定するために使用できます。デフォルトでは、コンテナは `default` ネットワークに接続されます。

コンテナを複数のネットワークに接続するには、 `networks`キーを使用できます。このキーはネットワーク名の配列を使用します。

## Composeのネットワーキング

Composeファイルの `network`キーは、コンテナが接続する必要があるネットワークを指定するために使用されます。デフォルトでは、コンテナは `default` ネットワークに接続されます。

Composeで使用できる3種類のネットワークは、ブリッジ、ホスト、およびなしです。

### 橋

デフォルトのネットワークタイプはブリッジです。このタイプのネットワークは、ホストの内部にプライベートネットワークを作成します。

ブリッジネットワークのコンテナは、ポートをホストに公開することなく互いに通信できます。

ブリッジネットワークを作成するには、`docker network create`コマンドを使用します。

```
$ docker network create --driver bridge my-bridge-network
```

Composeファイルの `networks`キーを使ってブリッジネットワークを作成することもできます。

```yaml
バージョン： '3'

networks:
  my-bridge-network:
    driver: bridge
```

###オーガナイザー

ホストネットワークタイプは、コンテナとDockerホスト間の分離を排除し、ホストのネットワーキングを直接使用します。

これは、ホストネットワークのコンテナがポートを外部に公開することなく互いに通信できることを意味します。

ホストネットワークを作成するには、 `docker network create`コマンドを使用してください。

```
$ docker network create --driver host my-host-network
```

Composeファイルの `networks`キーを使ってホストネットワークを作成することもできます。

```yaml
バージョン： '3'

networks:
  my-host-network:
    driver: host
```

### なし

なしネットワークタイプは、ネットワークに接続されていないコンテナを作成するために使用されます。

これは開発やテスト目的に役立ちます。

なしネットワークを作成するには、`docker network create`コマンドを使用します。

```
$ docker network create --driver none my-none-network
```

Composeファイルで `networks`キーを使用してネットワークを作成することもできます。

```yaml
バージョン： '3'

networks:
  my-none-network:
    driver: none
```

## ネットワークとコンテナの接続

コンテナを互いに接続するには、同じネットワーク上にある必要があります。

`network`キーは、コンテナが接続する必要があるネットワークを指定するために使用できます。デフォルトでは、コンテナは `default` ネットワークに接続されます。

コンテナを複数のネットワークに接続するには、 `networks`キーを使用できます。このキーはネットワーク名の配列を使用します。

```yaml
バージョン： '3'

services:
  web:
    image: nginx
    ports:
      - 「80:80」
    networks:
      - my-bridge-network
      - my-host-network
      - my-none-network
```

## Composeのネットワーキング

Composeファイルの `network`キーは、コンテナが接続する必要があるネットワークを指定するために使用されます。デフォルトでは、コンテナは `default` ネットワークに接続されます。

Composeで使用できる3種類のネットワークは、ブリッジ、ホスト、およびなしです。

### 橋

デフォルトのネットワークタイプはブリッジです。このタイプのネットワークは、ホストの内部にプライベートネットワークを作成します。

ブリッジネットワークのコンテナは、ポートをホストに公開することなく互いに通信できます。

ブリッジネットワークを作成するには、`docker network create`コマンドを使用します。

```
$ docker network create --driver bridge my-bridge-network
```

Composeファイルの `networks`キーを使ってブリッジネットワークを作成することもできます。

```yaml
バージョン： '3'

networks:
  my-bridge-network:
    driver: bridge
```

###オーガナイザー

ホストネットワークタイプは、コンテナとDockerホスト間の分離を排除し、ホストのネットワーキングを直接使用します。

これは、ホストネットワークのコンテナがポートを外部に公開することなく互いに通信できることを意味します。

ホストネットワークを作成するには、 `docker network create`コマンドを使用してください。

```
$ docker network create --driver host my-host-network
```

Composeファイルの `networks`キーを使ってホストネットワークを作成することもできます。

```yaml
バージョン： '3'

networks:
  my-host-network:
    driver: host
```

### なし

なしネットワークタイプは、ネットワークに接続されていないコンテナを作成するために使用されます。

これは開発やテスト目的に役立ちます。

なしネットワークを作成するには、`docker network create`コマンドを使用します。

```
$ docker network create --driver none my-none-network
```

Composeファイルで `networks`キーを使用してネットワークを作成することもできます。

```yaml
バージョン： '3'

networks:
  my-none-network:
    driver: none
```

## ネットワークとコンテナの接続

コンテナを互いに接続するには、同じネットワーク上にある必要があります。

`network`キーは、コンテナが接続する必要があるネットワークを指定するために使用できます。デフォルトでは、コンテナは `default` ネットワークに接続されます。

コンテナを複数のネットワークに接続するには、 `networks`キーを使用できます。このキーはネットワーク名の配列を使用します。

```yaml
バージョン： '3'

services:
  web:
    image: nginx
    ports:
      - 「80:80」
    networks:
      - my-bridge-network
      - my-host-network
      - my-none-network
```