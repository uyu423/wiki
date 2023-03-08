---
title: 도커 핸드북
description: 내가 볼려고 필요한 것들만 정리함
published: true
date: 2023-02-17T18:00:48.388Z
tags: docker
editor: markdown
dateCreated: 2023-01-27T07:59:02.025Z
---

## Docker 설치

- docker.com 에서 제공하는 스크립트로 설치

```bash
curl -sSL get.docker.com | sh
```

## Docker 상태 확인

```bash
docker ps
```

- 다음과 같은 에러가 발생한다면 Docker Daemon을 띄워줘야함
  - `Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?`
  - `sudo service` 혹은 `sudo systemctl` 명령어로 도커 데몬을 띄울 수 있음 
    - `sudo service docker start`

> 윈도우의 WSL version 1 환경에서는 많은 어려움이 있다. WSL version 2인 경우에는 큰 문제 없이 설치가 되니 참고
{.is-warning}

> WSL v2 + Ubuntu 22.04 이상에서 iptables 관련 이슈가 있다.
> `sudo update-alternatives --config iptables` 명령어를 사용해서 `iptables-ntf` 대신 `iptables-legacy` 를 사용하면 이슈 해결
{.is-warning}

- `docker ps` 실행 시 아래와 같이 ps 상태가 나타나면 도커 데몬 정상 실행 중

```bash
$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

## Docker Build

### with AWS ECR

- awscli 설치

```bash
sudo apt install awscli
```

- awscli 설정
  - IAM 등에서 발급된 Access Key, Secret Key를 설정한다.

```bash
aws configure
AWS Access Key ID:
AWS Secret Access Key:
Default region name [ap-northeast-2]:
Default output format [None]:
```

- aws 설정을 사용하여 docker 저장소 로그인
- 로그인 엔드포인트 주소는 AWS ECR에서 확인

```bash
aws ecr get-login-password --region ap-northeast-2 | docker login --username AWS --password-stdin 1234567890.dkr.ecr.ap-northeast-2.amazonaws.com
```

- 현재 위치의 `Dockerfile`을 사용해서 AWS ECR에 app을 배포

```
docker build . -t 1234567890.dkr.ecr.ap-northeast-2.amazonaws.com/app:0.0.2
```

