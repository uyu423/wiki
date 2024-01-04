---
title: Docker Engine 대체가능한 colima
description: 
published: true
date: 2024-01-04T02:53:09.276Z
tags: docker
editor: markdown
dateCreated: 2024-01-04T02:51:38.909Z
---

> - 라이센스 이슈로 docker-engine을 더 이상 사용하지 않기로 했고, docker-cli 를 그대로 사용할 수 있으면서 docker-engine만 대체할 수 있는 소프트웨어를 찾게됨
> - colima 라는 이름이 잘 연상이 안되어서 맨날 까먹는 바람에 따로 정리함
> - 참고: https://velog.io/@sblee/install-colima

# Installation

```bash
brew install colima docker docker-compose \
&& mkdir -p ~/.docker/cli-plugins \
&& ln -sfn $(brew --prefix)/opt/docker-compose/bin/docker-compose ~/.docker/cli-plugins/docker-compose
```

# Start

```bash
colima start
```

---

- `docker ps` 해서 정상적으로 빈 컨테이너 출력된다면 colima가 docker-engine 대체로서 정상 동작하고 있는 것

```
$ docker ps                                                                           

CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

- [Colima*Github*](https://github.com/abiosoft/colima)
{.links-list}