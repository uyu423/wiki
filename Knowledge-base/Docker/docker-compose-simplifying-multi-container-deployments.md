---
title: Docker Compose: 다중 컨테이너 배포 간소화
description: 
published: true
date: 2023-02-01T12:57:41.494Z
tags: 
editor: markdown
dateCreated: 2023-02-01T12:57:38.046Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Docker Compose: Simplifying Multi-Container Deployments***English** version of this document is available*](/en/Knowledge-base/Docker/docker-compose-simplifying-multi-container-deployments)
{.links-list}



# Docker Compose: 다중 컨테이너 배포 간소화

Docker Compose는 다중 컨테이너 Docker 애플리케이션을 정의하고 실행하기 위한 도구입니다. Compose에서는 YAML 파일을 사용하여 애플리케이션의 서비스를 구성합니다. 그런 다음 단일 명령으로 구성에서 모든 서비스를 만들고 시작합니다.

Compose 사용은 기본적으로 3단계 프로세스입니다.

1. Dockerfile로 앱의 환경을 정의하여 어디에서나 재현할 수 있습니다.

2. 격리된 환경에서 함께 실행할 수 있도록 docker-compose.yml에서 앱을 구성하는 서비스를 정의합니다.

3. docker-compose up을 실행하면 Compose가 전체 앱을 시작하고 실행합니다.

## Dockerfile로 앱 환경 정의

Dockerfile은 Docker 이미지를 빌드하기 위해 일반적으로 수동으로 실행하는 모든 명령이 포함된 텍스트 문서입니다.

```
FROM node:8

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 8080

CMD [ "npm", "start" ]
```

가장 먼저 해야 할 일은 컨테이너에 사용할 기본 이미지를 지정하는 것입니다. 이 경우 Node.js 애플리케이션 실행에 널리 사용되는 이미지인 node:8을 사용하고 있습니다.

다음으로 WORKDIR 명령어는 Dockerfile에서 뒤에 오는 RUN, CMD, ENTRYPOINT, COPY 및 ADD 명령어에 대한 작업 디렉터리를 설정합니다.

COPY 명령은 <src>에서 새 파일 또는 디렉터리를 복사하고 <dest> 경로에 있는 이미지의 파일 시스템에 추가합니다.

RUN 명령은 현재 이미지 위에 있는 새 레이어에서 모든 명령을 실행하고 결과를 커밋합니다. 커밋된 결과 이미지는 Dockerfile의 다음 단계에 사용됩니다.

이 경우 npm install을 실행하여 package.json 파일에 정의된 모든 종속성을 설치합니다.

사본 . . 명령은 현재 디렉토리의 모든 파일을 컨테이너에 복사합니다.

EXPOSE 명령어는 컨테이너가 런타임에 지정된 네트워크 포트에서 수신 대기할 것임을 Docker에 알립니다.

CMD 명령에는 두 가지 형식이 있습니다. 선호되는 형식인 exec 형식과 셸 형식입니다.

exec 형식을 사용하면 셸 문자열 변경을 방지하고 다른 셸을 사용하거나 셸을 전혀 사용하지 않을 수 있습니다. 이렇게 하면 쉘 형식을 사용하는 CMD 또는 RUN 명령이 실행되지 않습니다.

이 경우 우리는 exec 형식을 사용하고 있으며 컨테이너가 시작될 때 npm start 명령을 실행하도록 지정하고 있습니다.

## docker-compose.yml에서 앱을 구성하는 서비스 정의

이제 Dockerfile이 있으므로 docker-compose.yml 파일에서 서비스를 정의할 수 있습니다.

```
version: '3'

services:
  web:
    build: .
    ports:
     - "8080:8080"
```

이 파일에서 web이라는 단일 서비스를 정의합니다. 이 서비스는 현재 디렉터리의 Dockerfile을 사용하여 빌드됩니다. 그리고 호스트의 포트 8080을 컨테이너의 포트 8080에 매핑하고 있습니다.

## docker-compose up을 실행하면 Compose가 전체 앱을 시작하고 실행합니다.

이제 Dockerfile 및 docker-compose.yml 파일이 있으므로 docker-compose up을 실행하여 앱을 시작할 수 있습니다.

```
$ docker-compose up
```

이 명령은 웹 서비스를 시작하고 콘솔에 로그를 인쇄합니다.

## 결론

Docker Compose는 다중 컨테이너 Docker 애플리케이션을 배포하는 프로세스를 단순화하기 위한 훌륭한 도구입니다. Dockerfile 및 docker-compose.yml 파일을 사용하면 단일 명령으로 전체 앱을 정의하고 실행할 수 있습니다.