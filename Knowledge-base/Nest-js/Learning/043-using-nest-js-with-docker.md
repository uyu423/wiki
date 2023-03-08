---
title: 043: Nest.js를 도커와 함께 사용하기
description: 
published: true
date: 2023-02-15T14:32:51.833Z
tags: 
editor: markdown
dateCreated: 2023-02-15T14:32:50.203Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [043: Using Nest.js with Docker***English** document is available*](/en/Knowledge-base/Nest-js/Learning/043-using-nest-js-with-docker)
{.links-list}


# Nest.js를 Docker와 함께 사용

Docker는 웹 애플리케이션을 개발하고 배포하기 위한 훌륭한 도구입니다. 애플리케이션을 배포 및 관리하기 쉬운 독립형 환경으로 패키징할 수 있습니다.

Nest.js는 효율적이고 확장 가능한 Node.js 서버 측 애플리케이션을 구축하기 위한 프레임워크입니다. 최신 JavaScript를 사용하고 TypeScript(JavaScript에 정적 유형 검사를 제공)로 구축되었으며 객체 지향 프로그래밍과 함수형 프로그래밍의 요소를 결합합니다.

이 게시물에서는 Nest.js를 Docker와 함께 사용하는 방법을 알아봅니다. 간단한 Nest.js 애플리케이션을 만든 다음 Docker를 사용하여 컨테이너화합니다. 또한 Docker Compose를 사용하여 애플리케이션의 종속성을 관리하는 방법도 배웁니다.

## Nest.js 애플리케이션 만들기

간단한 Nest.js 애플리케이션을 만들어 시작해 보겠습니다. 애플리케이션을 "todo-list"라고 합니다.

먼저 Nest.js CLI를 설치해야 합니다. npm을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install -g @nestjs/cli
```

Nest.js CLI가 설치되면 다음 명령을 사용하여 애플리케이션을 만들 수 있습니다.

```
nest new todo-list
```

이렇게 하면 "todo-list"라는 새 디렉토리가 생성되고 Nest.js 애플리케이션의 기본 스캐폴딩이 생성됩니다.

다음으로 애플리케이션에 대한 종속성을 설치해야 합니다. npm을 사용하여 이 작업을 수행할 수 있습니다.

```
cd todo-list
npm install
```

이제 애플리케이션의 종속성이 설치되었으므로 다음 명령을 사용하여 애플리케이션을 시작할 수 있습니다.

```
npm start
```

이렇게 하면 포트 3000에서 애플리케이션이 시작됩니다. http://localhost:3000으로 이동하여 브라우저에서 애플리케이션을 볼 수 있습니다.

## 애플리케이션 컨테이너화

이제 기본 Nest.js 애플리케이션이 실행 중이므로 Docker를 사용하여 컨테이너화해 보겠습니다.

먼저 애플리케이션의 루트 디렉터리에 "Dockerfile"이라는 파일을 만들어야 합니다. 이 파일에는 Docker 이미지를 빌드하기 위한 지침이 포함됩니다.

Dockerfile은 다음 줄로 시작합니다.

```
FROM node:10-alpine
```

이 줄은 Docker 이미지의 기본 이미지로 Node.js 10 Alpine 이미지를 사용하도록 지정합니다. Alpine은 애플리케이션의 기본 이미지로 사용하기에 완벽한 경량 Linux 배포판입니다.

다음으로 애플리케이션의 파일을 이미지에 복사해야 합니다. COPY 명령을 사용하여 이를 수행할 수 있습니다.

```
COPY . .
```

그러면 현재 디렉토리의 모든 파일이 이미지로 복사됩니다.

이제 파일이 복사되었으므로 애플리케이션의 종속성을 설치해야 합니다. npm 명령을 사용하여 이 작업을 수행할 수 있습니다.

```
RUN npm install
```

마지막으로 애플리케이션을 시작하는 데 사용할 명령을 지정해야 합니다. CMD 명령을 사용하여 이 작업을 수행할 수 있습니다.

```
CMD ["npm", "start"]
```

컨테이너가 시작될 때 애플리케이션이 시작됩니다.

이제 Dockerfile이 완성되었습니다. 다음 명령을 사용하여 Docker 이미지를 빌드할 수 있습니다.

```
docker build -t todo-list .
```

그러면 Dockerfile의 지침을 사용하여 "todo-list"라는 이미지가 빌드됩니다.

이미지가 빌드되면 다음 명령을 사용하여 이미지를 실행할 수 있습니다.

```
docker run -d -p 3000:3000 todo-list
```

그러면 "todo-list" 이미지를 기반으로 컨테이너가 시작되고 컨테이너의 포트 3000이 호스트 시스템의 포트 3000에 매핑됩니다.

이제 http://localhost:3000으로 이동하여 브라우저에서 애플리케이션을 볼 수 있습니다.

## Docker Compose 사용

Docker Compose는 다중 컨테이너 Docker 애플리케이션을 정의하고 실행하기 위한 도구입니다. 단일 파일에서 애플리케이션의 종속성을 지정한 다음 단일 명령으로 모든 컨테이너를 시작할 수 있습니다.

애플리케이션의 루트 디렉터리에 "docker-compose.yml" 파일을 생성해 보겠습니다. 이 파일에는 Docker Compose를 사용하여 애플리케이션을 실행하기 위한 지침이 포함됩니다.

docker-compose.yml 파일은 다음 줄로 시작합니다.

```
version: '3'
```

이 줄은 Docker Compose 파일 형식의 버전 3을 사용하고 있음을 지정합니다.

다음으로 애플리케이션이 의존하는 서비스를 지정해야 합니다. "services" 키를 사용하여 이를 수행할 수 있습니다.

```
services:
  todo-list:
    image: todo-list
    ports:
      - "3000:3000"
```

이것은 "todo-list" 이미지를 사용하고 컨테이너의 포트 3000을 호스트 시스템의 포트 3000에 매핑하는 "todo-list"라는 서비스를 정의합니다.

이제 docker-compose.yml 파일이 완성되었으므로 다음 명령을 사용하여 애플리케이션을 시작할 수 있습니다.

```
docker-compose up
```

이렇게 하면 docker-compose.yml 파일에 정의된 모든 컨테이너가 시작됩니다.

이제 http://localhost:3000으로 이동하여 브라우저에서 애플리케이션을 볼 수 있습니다.

## 결론

이번 포스트에서는 Nest.js를 Docker와 함께 사용하는 방법을 배웠습니다. 간단한 Nest.js 애플리케이션을 만든 다음 Docker를 사용하여 컨테이너화했습니다. 또한 Docker Compose를 사용하여 애플리케이션의 종속성을 관리하는 방법도 배웠습니다.