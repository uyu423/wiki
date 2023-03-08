---
title: Node.js 애플리케이션 도커화
description: 
published: true
date: 2023-02-01T19:41:48.617Z
tags: 
editor: markdown
dateCreated: 2023-02-01T19:38:41.116Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Dockerizing Your Node.js Applications***English** document is available*](/en/Knowledge-base/Backend/dockerizing-your-node-js-applications)
{.links-list}

# Node.js 애플리케이션 도커화

Docker는 개발자와 시스템 관리자가 분산 애플리케이션을 구축, 배송 및 실행할 수 있는 개방형 플랫폼입니다. 런타임 독립적인 이식 가능한 애플리케이션 환경인 Docker Engine과 애플리케이션 공유 및 워크플로 자동화를 위한 클라우드 서비스인 Docker Hub로 구성된 Docker를 사용하면 앱을 구성 요소에서 신속하게 조립할 수 있으며 개발, QA 및 프로덕션 환경 간의 마찰이 제거됩니다. 결과적으로 IT 부서는 랩탑, 데이터 센터 VM 및 모든 클라우드에서 더 빠르게 배송하고 동일한 앱을 변경 없이 실행할 수 있습니다.

Node.js 애플리케이션을 도커화하면 여러 가지 이점이 있습니다.

- **격리**: 컨테이너는 동일한 호스트에서 실행되는 다른 애플리케이션으로부터 애플리케이션을 격리합니다. 이렇게 하면 동일한 호스트에서 여러 애플리케이션을 더 쉽게 실행하고 애플리케이션에 필요한 라이브러리와 구성이 있는지 확인할 수 있습니다.

- **재현성**: Docker 이미지에는 애플리케이션을 실행하는 데 필요한 모든 정보가 포함되어 있습니다. 이를 통해 다른 개발자와 응용 프로그램을 쉽게 공유하고 다른 환경에 배포할 수 있습니다.

- **효율성**: 애플리케이션을 실행하는 데 필요한 모든 종속성을 컨테이너에 패키징하면 애플리케이션이 배포되는 모든 호스트에 이러한 종속성을 설치하지 않아도 됩니다.

- **유연성**: Docker 이미지는 Docker 런타임이 있는 모든 호스트에서 실행할 수 있습니다. 이를 통해 온프레미스 데이터 센터 및 클라우드 기반 플랫폼과 같은 하이브리드 환경에서 애플리케이션을 쉽게 배포할 수 있습니다.

이 기사에서는 Node.js 애플리케이션을 고정 표시하는 방법을 보여줍니다. Express 웹 프레임워크를 사용하여 간단한 웹 애플리케이션을 구축하고 이를 Docker 이미지로 패키징합니다.

## 전제 조건

시작하기 전에 다음이 필요합니다.

- 텍스트 편집기. [Visual Studio Code](https://code.visualstudio.com/) 사용을 권장합니다.

- [Node.js](https://nodejs.org/en/)가 개발 머신에 설치되었습니다.

- 개발 머신에 [Docker](https://www.docker.com/)가 설치되어 있습니다.

## Node.js 애플리케이션 만들기

Express 웹 프레임워크를 사용하여 간단한 Node.js 애플리케이션을 만드는 것부터 시작하겠습니다. 프로젝트의 새 디렉터리를 만들고 그 안에 Node.js 프로젝트를 초기화합니다.

```
mkdir nodejs-docker
cd nodejs-docker
npm init
```

이름, 버전, 설명 등과 같은 프로젝트에 대한 정보를 입력하라는 메시지가 표시됩니다. Enter 키를 눌러 기본값을 수락할 수 있습니다.

다음으로 Express 웹 프레임워크 및 기타 종속 항목을 설치합니다.

```
npm install express --save
```

프로젝트 디렉터리에 `app.js`라는 파일을 만들고 다음 코드를 추가합니다.

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello, world!');
});

app.listen(3000, () => {
  console.log('Example app listening on port 3000!');
});
```

이 코드는 포트 3000에서 수신하고 "Hello, world!"라는 문자열을 반환하는 간단한 웹 서버를 만듭니다. 서버의 루트 URL에 요청을 할 때.

다음 명령을 실행하여 웹 서버를 시작할 수 있습니다.

```
node app.js
```

그런 다음 http://localhost:3000에서 웹 서버에 액세스할 수 있습니다.

## Dockerfile 만들기

Dockerfile은 Docker 이미지를 빌드하기 위한 지침이 포함된 텍스트 파일입니다. 프로젝트 디렉터리에 `Dockerfile`이라는 파일을 만들고 다음 콘텐츠를 추가합니다.

```
FROM node:alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "app.js"]
```

이 Dockerfile은 [Node.js](https://hub.docker.com/_/node/) [Alpine](https://hub.docker.com/_/alpine/) 이미지를 기본 이미지로 사용합니다. 우리의 도커 이미지. Alpine 이미지는 Node.js 애플리케이션을 실행하는 데 필요한 최소한의 것을 포함하는 작은 Linux 배포판입니다.

`WORKDIR` 명령은 후속 명령을 위한 작업 디렉토리를 설정합니다. `COPY` 명령어는 `package.json` 및 `package-lock.json` 파일을 프로젝트 디렉토리에서 작업 디렉토리로 복사합니다. `RUN` 명령은 `npm install` 명령을 실행하여 애플리케이션에 대한 종속성을 설치합니다. 그런 다음 'COPY' 명령어는 나머지 파일을 프로젝트 디렉토리에서 작업 디렉토리로 복사합니다. 'EXPOSE' 명령어는 포트 3000을 노출합니다. 'CMD' 명령어는 컨테이너가 시작될 때 실행할 명령을 지정합니다.

## Docker 이미지 빌드

이제 Dockerfile을 만들었으므로 Docker 이미지를 빌드할 수 있습니다. 프로젝트 디렉터리에서 다음 명령을 실행합니다.

```
docker build -t nodejs-docker .
```

이 명령은 `nodejs-docker`라는 이름의 Docker 이미지를 생성합니다.

## Docker 컨테이너 실행

이제 Docker 이미지를 컨테이너로 실행할 수 있습니다. 다음 명령을 실행하여 컨테이너를 시작합니다.

```
docker build -d -p 3000:3000 nodejs-docker
```

이 명령은 컨테이너를 시작하고 호스트의 포트 3000을 컨테이너의 포트 3000에 바인딩합니다. `-d` 옵션은 컨테이너를 분리 모드로 실행하도록 Docker에 지시합니다. 이것은 컨테이너가 백그라운드에서 실행되고 t에서 실행됨을 의미합니다.