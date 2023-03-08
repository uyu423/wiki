---
title: Docker Compose 네트워킹: 컨테이너와 네트워크 연결
description: 
published: true
date: 2023-01-31T10:23:49.274Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:23:47.440Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Docker Compose Networking: Connecting Containers with Networks***English** version of this document is available*](/en/Knowledge-base/Docker/docker-compose-networking-connecting-containers-with-networks)
{.links-list}



# Docker Compose 네트워킹: 컨테이너와 네트워크 연결

Docker Compose 파일에서 `network` 키는 컨테이너가 연결해야 하는 네트워크를 지정하는 데 사용됩니다. 기본적으로 컨테이너는 `default` 네트워크에 연결됩니다.

Compose와 함께 사용할 수 있는 세 가지 유형의 네트워크는 브리지, 호스트 및 없음입니다.

## 다리

기본 네트워크 유형은 브리지입니다. 이 네트워크 유형은 호스트 내부에 사설 네트워크를 생성합니다.

브리지 네트워크의 컨테이너는 포트를 호스트에 노출하지 않고 서로 통신할 수 있습니다.

## 주최자

호스트 네트워크 유형은 컨테이너와 Docker 호스트 간의 격리를 제거하고 호스트의 네트워킹을 직접 사용합니다.

이는 호스트 네트워크의 컨테이너가 포트를 외부에 노출하지 않고도 서로 통신할 수 있음을 의미합니다.

## 없음

none 네트워크 유형은 네트워크에 연결되지 않은 컨테이너를 만드는 데 사용됩니다.

이는 개발 또는 테스트 목적에 유용할 수 있습니다.

## 네트워크와 컨테이너 연결

컨테이너를 서로 연결하려면 동일한 네트워크에 있어야 합니다.

`network` 키는 컨테이너가 연결해야 하는 네트워크를 지정하는 데 사용할 수 있습니다. 기본적으로 컨테이너는 `default` 네트워크에 연결됩니다.

컨테이너를 여러 네트워크에 연결하려면 `networks` 키를 사용할 수 있습니다. 이 키는 네트워크 이름 배열을 사용합니다.

## Compose의 네트워킹

Compose 파일에서 `network` 키는 컨테이너가 연결해야 하는 네트워크를 지정하는 데 사용됩니다. 기본적으로 컨테이너는 `default` 네트워크에 연결됩니다.

Compose와 함께 사용할 수 있는 세 가지 유형의 네트워크는 브리지, 호스트 및 없음입니다.

### 다리

기본 네트워크 유형은 브리지입니다. 이 네트워크 유형은 호스트 내부에 사설 네트워크를 생성합니다.

브리지 네트워크의 컨테이너는 포트를 호스트에 노출하지 않고 서로 통신할 수 있습니다.

브리지 네트워크를 생성하려면 `docker network create` 명령을 사용합니다.

```
$ docker network create --driver bridge my-bridge-network
```

Compose 파일에서 `networks` 키를 사용하여 브리지 네트워크를 생성할 수도 있습니다.

```yaml
version: '3'

networks:
  my-bridge-network:
    driver: bridge
```

### 주최자

호스트 네트워크 유형은 컨테이너와 Docker 호스트 간의 격리를 제거하고 호스트의 네트워킹을 직접 사용합니다.

이는 호스트 네트워크의 컨테이너가 포트를 외부에 노출하지 않고도 서로 통신할 수 있음을 의미합니다.

호스트 네트워크를 생성하려면 `docker network create` 명령을 사용합니다.

```
$ docker network create --driver host my-host-network
```

Compose 파일에서 `networks` 키를 사용하여 호스트 네트워크를 생성할 수도 있습니다.

```yaml
version: '3'

networks:
  my-host-network:
    driver: host
```

### 없음

none 네트워크 유형은 네트워크에 연결되지 않은 컨테이너를 만드는 데 사용됩니다.

이는 개발 또는 테스트 목적에 유용할 수 있습니다.

없음 네트워크를 만들려면 `docker network create` 명령을 사용합니다.

```
$ docker network create --driver none my-none-network
```

Compose 파일에서 `networks` 키를 사용하여 없음 네트워크를 만들 수도 있습니다.

```yaml
version: '3'

networks:
  my-none-network:
    driver: none
```

## 네트워크와 컨테이너 연결

컨테이너를 서로 연결하려면 동일한 네트워크에 있어야 합니다.

`network` 키는 컨테이너가 연결해야 하는 네트워크를 지정하는 데 사용할 수 있습니다. 기본적으로 컨테이너는 `default` 네트워크에 연결됩니다.

컨테이너를 여러 네트워크에 연결하려면 `networks` 키를 사용할 수 있습니다. 이 키는 네트워크 이름 배열을 사용합니다.

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

## Compose의 네트워킹

Compose 파일에서 `network` 키는 컨테이너가 연결해야 하는 네트워크를 지정하는 데 사용됩니다. 기본적으로 컨테이너는 `default` 네트워크에 연결됩니다.

Compose와 함께 사용할 수 있는 세 가지 유형의 네트워크는 브리지, 호스트 및 없음입니다.

### 다리

기본 네트워크 유형은 브리지입니다. 이 네트워크 유형은 호스트 내부에 사설 네트워크를 생성합니다.

브리지 네트워크의 컨테이너는 포트를 호스트에 노출하지 않고 서로 통신할 수 있습니다.

브리지 네트워크를 생성하려면 `docker network create` 명령을 사용합니다.

```
$ docker network create --driver bridge my-bridge-network
```

Compose 파일에서 `networks` 키를 사용하여 브리지 네트워크를 생성할 수도 있습니다.

```yaml
version: '3'

networks:
  my-bridge-network:
    driver: bridge
```

### 주최자

호스트 네트워크 유형은 컨테이너와 Docker 호스트 간의 격리를 제거하고 호스트의 네트워킹을 직접 사용합니다.

이는 호스트 네트워크의 컨테이너가 포트를 외부에 노출하지 않고도 서로 통신할 수 있음을 의미합니다.

호스트 네트워크를 생성하려면 `docker network create` 명령을 사용합니다.

```
$ docker network create --driver host my-host-network
```

Compose 파일에서 `networks` 키를 사용하여 호스트 네트워크를 생성할 수도 있습니다.

```yaml
version: '3'

networks:
  my-host-network:
    driver: host
```

### 없음

none 네트워크 유형은 네트워크에 연결되지 않은 컨테이너를 만드는 데 사용됩니다.

이는 개발 또는 테스트 목적에 유용할 수 있습니다.

없음 네트워크를 만들려면 `docker network create` 명령을 사용합니다.

```
$ docker network create --driver none my-none-network
```

Compose 파일에서 `networks` 키를 사용하여 없음 네트워크를 만들 수도 있습니다.

```yaml
version: '3'

networks:
  my-none-network:
    driver: none
```

## 네트워크와 컨테이너 연결

컨테이너를 서로 연결하려면 동일한 네트워크에 있어야 합니다.

`network` 키는 컨테이너가 연결해야 하는 네트워크를 지정하는 데 사용할 수 있습니다. 기본적으로 컨테이너는 `default` 네트워크에 연결됩니다.

컨테이너를 여러 네트워크에 연결하려면 `networks` 키를 사용할 수 있습니다. 이 키는 네트워크 이름 배열을 사용합니다.

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