---
title: Dockerfile 모범 사례: 신뢰할 수 있는 Docker 이미지 생성
description: 
published: true
date: 2023-02-15T23:32:48.933Z
tags: 
editor: markdown
dateCreated: 2023-02-15T23:32:47.213Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Dockerfile Best Practices: Creating Reliable Docker Images***English** document is available*](/en/Knowledge-base/Docker/dockerfile-best-practices-creating-reliable-docker-images)
{.links-list}


# Dockerfile 모범 사례: 신뢰할 수 있는 Docker 이미지 생성

Dockerfile은 Docker 사용의 기본 부분입니다. 새 컨테이너를 만드는 데 사용할 수 있는 고유한 이미지를 만들 수 있습니다. 잘 만들어진 Dockerfile을 사용하면 이미지를 쉽게 생성, 유지 관리 및 업데이트할 수 있으며 장기적으로 많은 시간과 노력을 절약할 수 있습니다.

이 문서에서는 Docker 사용자의 삶을 더 쉽게 만들기 위해 신뢰할 수 있는 Docker 이미지를 만들기 위한 몇 가지 모범 사례를 제공합니다.

## .dockerignore 사용

.dockerignore 파일은 이미지에서 제외해야 하는 파일 및 디렉터리를 지정하는 데 사용됩니다. 이는 임시 파일 또는 빌드 아티팩트와 같이 이미지에 필요하지 않은 파일을 제외하는 데 유용합니다.

.dockerignore 파일을 만들려면 프로젝트의 루트 디렉터리에 ".dockerignore"라는 파일을 만들고 제외하려는 각 파일 또는 디렉터리를 한 줄에 하나씩 추가하면 됩니다. 예를 들어:

```
.dockerignore

# Exclude all temporary files
*.tmp

# Exclude all build artifacts
build/
```

## Dockerfile을 단순하게 유지

간단한 Dockerfile은 복잡한 것보다 이해하고 유지 관리하기 쉽습니다. 또한 Docker의 향후 버전과 호환될 가능성이 더 높습니다.

Dockerfile을 단순하게 유지하는 한 가지 방법은 복잡한 셸 명령을 사용하지 않는 것입니다. 가능하면 기존 도커 이미지를 자체 이미지의 기반으로 사용하고 apt 또는 yum과 같은 패키지 관리자를 사용하여 필요한 소프트웨어를 설치합니다.

Dockerfile을 단순하게 유지하는 또 다른 방법은 불필요한 소프트웨어 설치를 피하는 것입니다. 특정 용도로만 이미지를 사용하는 경우 텍스트 편집기, 웹 브라우저 등 전체 운영 체제를 설치할 필요가 없습니다.

## 기본 이미지에 특정 태그 사용

Docker 레지스트리의 기본 이미지를 사용하는 경우 "최신" 태그를 사용하는 대신 항상 특정 태그를 지정하십시오. "최신" 태그는 종종 개발자가 이미지의 최신 개발 버전을 나타내기 위해 사용하는데, 이는 프로덕션 용도에 적합하지 않을 수 있습니다.

## 단일 RUN 명령어 사용

가능하면 Dockerfile에서 여러 명령이 아닌 단일 RUN 명령을 사용하십시오. 이렇게 하면 이미지를 더 쉽게 만들 수 있고 성능에 중요할 수 있는 이미지의 레이어 수를 줄일 수 있습니다.

단일 RUN 명령을 사용하려면 실행하려는 모든 명령을 &&로 구분하여 한 줄로 결합하기만 하면 됩니다. 예를 들어:

```
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:my-ppa && \
    apt-get update && \
    apt-get install -y my-software
```

## 특정 사용자 사용

기본적으로 컨테이너는 루트 사용자로 실행됩니다. 컨테이너에서 실행 중인 모든 프로세스가 호스트 시스템에 대한 전체 액세스 권한을 가지므로 이는 보안 위험이 될 수 있습니다.

이를 방지하려면 Dockerfile에서 새 사용자를 생성하고 이 사용자를 사용하여 컨테이너의 모든 프로세스를 실행할 수 있습니다. 예를 들어:

```
# Create a new user
RUN useradd -ms /bin/bash myuser

# Use the new user for all subsequent commands
USER myuser
```

## 특정 작업 디렉토리 사용

컨테이너가 생성되면 기본 작업 디렉토리가 제공됩니다. 이 디렉터리는 Dockerfile의 WORKDIR 명령을 사용하여 재정의할 수 있습니다.

특정 작업 디렉터리를 지정하는 것이 좋습니다. 컨테이너에서 파일을 더 쉽게 찾을 수 있고 서로 다른 시스템 간의 이식성에 도움이 될 수 있기 때문입니다. 예를 들어:

```
# Set the working directory to /app
WORKDIR /app
```

## ADD 및 COPY 사용 금지

ADD 및 COPY 명령어는 비슷하지만 몇 가지 중요한 차이점이 있습니다. ADD는 원격 URL에서 파일을 추출하는 데 사용할 수 있지만 COPY는 빌드 컨텍스트에서 파일을 복사하는 데만 사용할 수 있습니다.

ADD는 또한 파일 간의 종속성을 자동으로 해결할 수 있으므로 COPY보다 강력합니다. 예를 들어 .tar.gz 파일을 추가하면 ADD가 자동으로 아카이브에서 파일을 추출합니다.

이러한 차이로 인해 일반적으로 Dockerfile에서 ADD보다 COPY를 사용하는 것이 좋습니다.

## 상태 확인 지정

상태 확인은 컨테이너가 정상이고 계속 실행되어야 하는지 여부를 결정하는 데 사용되는 테스트입니다. 상태 확인에 실패하면 컨테이너가 중지되고 다시 시작됩니다.

상태 확인은 Dockerfile의 HEALTHCHECK 명령을 사용하여 지정할 수 있습니다. 예를 들어:

```
# Check that the container is healthy every 30 seconds
# and that the HTTP service is responding on port 80
HEALTHCHECK --interval=30s --timeout=5s \
    CMD wget -qO- http://localhost:80/ || exit 1
```

## 다단계 빌드 사용

다단계 빌드는 단일 빌드 프로세스의 일부로 여러 이미지를 만들 수 있는 Docker의 기능입니다. 이미지를 빌드한 후 이미지에서 불필요한 파일을 제거할 수 있으므로 더 작고 안전한 이미지를 만드는 데 유용할 수 있습니다.

다단계 빌드를 사용하려면 Dockerfile에서 각각 이미지 이름이 다른 여러 FROM 명령을 생성하기만 하면 됩니다. 예를 들어:

```
# Build stage
FROM golang:1.8 as builder

WORKDIR /src

COPY . .

RUN go build -o app

# Run stage
FROM alpine:latest

WORKDIR /app

COPY --from=builder /src/app .

CMD ["./app"]
```

## 결론

이 문서에 설명된 모범 사례를 따르면 Dockerfile을 보다 안정적이고 이해하기 쉽고 유지 관리하기 쉽게 만들 수 있습니다. 이렇게 하면 장기적으로 시간과 노력을 절약할 수 있고 Docker 사용자로서의 삶이 훨씬 쉬워질 것입니다.