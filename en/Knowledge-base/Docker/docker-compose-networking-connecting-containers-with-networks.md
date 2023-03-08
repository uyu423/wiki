---
title: Docker Compose Networking: Connecting Containers with Networks
description: 
published: true
date: 2023-01-31T10:23:51.165Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:23:47.441Z
---

- [Docker Compose 네트워킹: 컨테이너와 네트워크 연결***Korean** version of this document is available*](/ko/Knowledge-base/Docker/docker-compose-networking-connecting-containers-with-networks)
{.links-list}
- [Docker Compose Networking: コンテナーをネットワークに接続する***Japanese** version of this document is available*](/ja/Knowledge-base/Docker/docker-compose-networking-connecting-containers-with-networks)
{.links-list}
- [Docker Compose 网络：连接容器与网络***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Docker/docker-compose-networking-connecting-containers-with-networks)
{.links-list}



# Docker Compose Networking: Connecting Containers with Networks

In a Docker Compose file, the `network` key is used to specify the networks that containers should connect to. By default, containers are connected to the `default` network.

There are three types of networks that can be used with Compose: bridge, host, and none.

## Bridge

The default network type is bridge. This network type creates a private network internal to the host.

Containers on a bridge network can communicate with each other without exposing their ports to the host.

## Host

The host network type removes the isolation between the container and the Docker host, and uses the host’s networking directly.

This means that the containers on the host network can communicate with each other without exposing their ports to the outside world.

## None

The none network type is used to create a container that is not connected to any network.

This can be useful for development or testing purposes.

## Connecting Containers with Networks

In order to connect containers with each other, they must be on the same network.

The `network` key can be used to specify the network that containers should connect to. By default, containers are connected to the `default` network.

If you want to connect containers to multiple networks, you can use the `networks` key. This key takes an array of network names.

## Networking in Compose

In a Compose file, the `network` key is used to specify the networks that containers should connect to. By default, containers are connected to the `default` network.

There are three types of networks that can be used with Compose: bridge, host, and none.

### Bridge

The default network type is bridge. This network type creates a private network internal to the host.

Containers on a bridge network can communicate with each other without exposing their ports to the host.

To create a bridge network, use the `docker network create` command.

```
$ docker network create --driver bridge my-bridge-network
```

You can also create a bridge network using the `networks` key in a Compose file.

```yaml
version: '3'

networks:
  my-bridge-network:
    driver: bridge
```

### Host

The host network type removes the isolation between the container and the Docker host, and uses the host’s networking directly.

This means that the containers on the host network can communicate with each other without exposing their ports to the outside world.

To create a host network, use the `docker network create` command.

```
$ docker network create --driver host my-host-network
```

You can also create a host network using the `networks` key in a Compose file.

```yaml
version: '3'

networks:
  my-host-network:
    driver: host
```

### None

The none network type is used to create a container that is not connected to any network.

This can be useful for development or testing purposes.

To create a none network, use the `docker network create` command.

```
$ docker network create --driver none my-none-network
```

You can also create a none network using the `networks` key in a Compose file.

```yaml
version: '3'

networks:
  my-none-network:
    driver: none
```

## Connecting Containers with Networks

In order to connect containers with each other, they must be on the same network.

The `network` key can be used to specify the network that containers should connect to. By default, containers are connected to the `default` network.

If you want to connect containers to multiple networks, you can use the `networks` key. This key takes an array of network names.

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

## Networking in Compose

In a Compose file, the `network` key is used to specify the networks that containers should connect to. By default, containers are connected to the `default` network.

There are three types of networks that can be used with Compose: bridge, host, and none.

### Bridge

The default network type is bridge. This network type creates a private network internal to the host.

Containers on a bridge network can communicate with each other without exposing their ports to the host.

To create a bridge network, use the `docker network create` command.

```
$ docker network create --driver bridge my-bridge-network
```

You can also create a bridge network using the `networks` key in a Compose file.

```yaml
version: '3'

networks:
  my-bridge-network:
    driver: bridge
```

### Host

The host network type removes the isolation between the container and the Docker host, and uses the host’s networking directly.

This means that the containers on the host network can communicate with each other without exposing their ports to the outside world.

To create a host network, use the `docker network create` command.

```
$ docker network create --driver host my-host-network
```

You can also create a host network using the `networks` key in a Compose file.

```yaml
version: '3'

networks:
  my-host-network:
    driver: host
```

### None

The none network type is used to create a container that is not connected to any network.

This can be useful for development or testing purposes.

To create a none network, use the `docker network create` command.

```
$ docker network create --driver none my-none-network
```

You can also create a none network using the `networks` key in a Compose file.

```yaml
version: '3'

networks:
  my-none-network:
    driver: none
```

## Connecting Containers with Networks

In order to connect containers with each other, they must be on the same network.

The `network` key can be used to specify the network that containers should connect to. By default, containers are connected to the `default` network.

If you want to connect containers to multiple networks, you can use the `networks` key. This key takes an array of network names.

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