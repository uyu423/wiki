---
title: Docker Compose 网络：连接容器与网络
description: 
published: true
date: 2023-01-31T10:23:49.451Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:23:47.444Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Docker Compose Networking: Connecting Containers with Networks***English** version of this document is available*](/en/Knowledge-base/Docker/docker-compose-networking-connecting-containers-with-networks)
{.links-list}



# Docker Compose 网络：连接容器和网络

在 Docker Compose 文件中，`network` 键用于指定容器应连接到的网络。默认情况下，容器连接到“默认”网络。

Compose 可以使用三种类型的网络：网桥、主机和无。

## 桥

默认网络类型是网桥。此网络类型创建主机内部的专用网络。

桥接网络上的容器可以相互通信，而无需将其端口暴露给主机。

## 主持人

主机网络类型去除了容器与Docker主机之间的隔离，直接使用主机的网络。

这意味着主机网络上的容器可以相互通信，而无需将其端口暴露给外界。

## 没有任何

none 网络类型用于创建不连接任何网络的容器。

这对于开发或测试目的很有用。

## 将容器与网络连接

为了将容器相互连接，它们必须在同一个网络上。

`network` 键可用于指定容器应连接到的网络。默认情况下，容器连接到“默认”网络。

如果要将容器连接到多个网络，可以使用 networks 键。该键采用网络名称数组。

## Compose 中的网络

在 Compose 文件中，`network` 键用于指定容器应连接到的网络。默认情况下，容器连接到“默认”网络。

Compose 可以使用三种类型的网络：网桥、主机和无。

### 桥

默认网络类型是网桥。此网络类型创建主机内部的专用网络。

桥接网络上的容器可以相互通信，而无需将其端口暴露给主机。

要创建桥接网络，请使用 `docker network create` 命令。

```
$ docker network create --driver bridge my-bridge-network
```

您还可以使用 Compose 文件中的 networks 键创建桥接网络。

```yaml
version: '3'

networks:
  my-bridge-network:
    driver: bridge
```

### 主持人

主机网络类型去除了容器与Docker主机之间的隔离，直接使用主机的网络。

这意味着主机网络上的容器可以相互通信，而无需将其端口暴露给外界。

要创建主机网络，请使用 `docker network create` 命令。

```
$ docker network create --driver host my-host-network
```

您还可以使用 Compose 文件中的 networks 键创建主机网络。

```yaml
version: '3'

networks:
  my-host-network:
    driver: host
```

### 没有任何

none 网络类型用于创建不连接任何网络的容器。

这对于开发或测试目的很有用。

要创建一个无网络，请使用 `docker network create` 命令。

```
$ docker network create --driver none my-none-network
```

您还可以使用 Compose 文件中的 networks 键创建一个无网络。

```yaml
version: '3'

networks:
  my-none-network:
    driver: none
```

## 将容器与网络连接

为了将容器相互连接，它们必须在同一个网络上。

`network` 键可用于指定容器应连接到的网络。默认情况下，容器连接到“默认”网络。

如果要将容器连接到多个网络，可以使用 networks 键。该键采用网络名称数组。

```yaml
version: '3'

services:
  web:
    image: nginx
    ports:
      - "80:80"
    networks:
      - my-bridge-network
      - my-host-network
      - my-none-network
```

## Compose 中的网络

在 Compose 文件中，`network` 键用于指定容器应连接到的网络。默认情况下，容器连接到“默认”网络。

Compose 可以使用三种类型的网络：网桥、主机和无。

### 桥

默认网络类型是网桥。此网络类型创建主机内部的专用网络。

桥接网络上的容器可以相互通信，而无需将其端口暴露给主机。

要创建桥接网络，请使用 `docker network create` 命令。

```
$ docker network create --driver bridge my-bridge-network
```

您还可以使用 Compose 文件中的 networks 键创建桥接网络。

```yaml
version: '3'

networks:
  my-bridge-network:
    driver: bridge
```

### 主持人

主机网络类型去除了容器与Docker主机之间的隔离，直接使用主机的网络。

这意味着主机网络上的容器可以相互通信，而无需将其端口暴露给外界。

要创建主机网络，请使用 `docker network create` 命令。

```
$ docker network create --driver host my-host-network
```

您还可以使用 Compose 文件中的 networks 键创建主机网络。

```yaml
version: '3'

networks:
  my-host-network:
    driver: host
```

### 没有任何

none 网络类型用于创建不连接任何网络的容器。

这对于开发或测试目的很有用。

要创建一个无网络，请使用 `docker network create` 命令。

```
$ docker network create --driver none my-none-network
```

您还可以使用 Compose 文件中的 networks 键创建一个无网络。

```yaml
version: '3'

networks:
  my-none-network:
    driver: none
```

## 将容器与网络连接

为了将容器相互连接，它们必须在同一个网络上。

`network` 键可用于指定容器应连接到的网络。默认情况下，容器连接到“默认”网络。

如果要将容器连接到多个网络，可以使用 networks 键。该键采用网络名称数组。

```yaml
version: '3'

services:
  web:
    image: nginx
    ports:
      - "80:80"
    networks:
      - my-bridge-network
      - my-host-network
      - my-none-network
```