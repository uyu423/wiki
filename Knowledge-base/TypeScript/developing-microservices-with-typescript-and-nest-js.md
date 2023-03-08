---
title: TypeScript 및 Nest.js로 마이크로서비스 개발
description: 
published: true
date: 2023-03-01T03:32:44.298Z
tags: 
editor: markdown
dateCreated: 2023-03-01T03:32:37.073Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Developing Microservices with TypeScript and Nest.js***English** document is available*](/en/Knowledge-base/TypeScript/developing-microservices-with-typescript-and-nest-js)
{.links-list}


# TypeScript와 Nest.js로 마이크로서비스 개발하기

TypeScript는 JavaScript 개발에 클래스, 인터페이스 및 모듈과 같은 기능과 함께 정적 유형 검사를 제공하는 강력한 언어입니다. Nest.js는 효율적이고 확장 가능한 엔터프라이즈급 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다.

이 기사에서는 TypeScript와 Nest.js를 사용하여 마이크로서비스를 개발하는 방법을 살펴보겠습니다. 마이크로서비스에 TypeScript와 Nest.js를 사용할 때의 이점부터 살펴보겠습니다. 그런 다음 TypeScript와 Nest.js를 사용하여 간단한 마이크로서비스를 만듭니다. 마지막으로 마이크로서비스를 서버에 배포합니다.

## 마이크로서비스용 TypeScript 및 Nest.js 사용의 이점

마이크로서비스 개발에 TypeScript와 Nest.js를 사용하면 많은 이점이 있습니다. TypeScript는 개발 프로세스 초기에 오류를 발견하는 데 도움이 되는 정적 유형 검사를 제공합니다. 다른 TypeScript 파일을 가져올 수 있는 TypeScript의 기능은 코드를 쉽게 모듈화할 수 있음을 의미합니다. Nest.js는 TypeScript를 기반으로 구축되었으며 많은 이점을 공유합니다. 또한 Nest.js는 코드를 구성하는 데 도움이 되는 강력한 모듈 시스템을 제공합니다.

Nest.js는 또한 마이크로서비스 개발에 유용한 여러 기능을 제공합니다. Nest.js는 확장 가능하고 사용하기 쉽도록 설계되었습니다. 또한 메시지 대기열 및 데이터베이스와 같은 마이크로 서비스에 유용한 여러 기능을 지원합니다.

## 간단한 마이크로서비스 만들기

마이크로서비스 개발에 TypeScript와 Nest.js를 사용할 때의 이점을 살펴보았으니 이제 간단한 마이크로서비스를 만들어 보겠습니다. 프로젝트 디렉토리에 `main.ts`라는 파일을 생성하는 것으로 시작하겠습니다. `main.ts`에서 `@nestjs/common` 모듈과 `@nestjs/microservices` 모듈을 가져옵니다. 또한 `Main`이라는 클래스를 만들고 `@nestjs/common` `@Controller` 데코레이터로 장식합니다.

```typescript
import { Controller, Get } from '@nestjs/common';
import { MessagePattern } from '@nestjs/microservices';

@Controller()
export class Main {

  @MessagePattern('add')
  add(data: number[]) {
    return data.reduce((a, b) => a + b);
  }
}
```

`Main` 클래스에서 `@nestjs/microservices` `@MessagePattern` 데코레이터로 장식된 `add`라는 메서드를 만들었습니다. `@MessagePattern` 데코레이터는 `add` 패턴이 있는 메시지를 수신할 때 이 메서드를 호출해야 한다고 Nest.js에 알려줍니다. 'add' 메서드는 숫자 배열을 입력으로 사용하고 숫자의 합계를 반환합니다.

다음으로 프로젝트 디렉터리에 `server.ts`라는 파일을 만듭니다. `server.ts`에서 `@nestjs/microservices` 모듈과 `Main` 클래스를 가져옵니다. 또한 `Server`라는 클래스를 만들고 `@nestjs/microservices` `@Microservice` 데코레이터로 장식합니다.

```typescript
import { Microservice } from '@nestjs/microservices';

import { Main } from './main';

@Microservice()
export class Server {
  constructor(private readonly main: Main) {}
}
```

`Server` 클래스에서 `@nestjs/microservices` `@Inject` 데코레이터를 사용하여 `Main` 클래스의 인스턴스를 주입했습니다. 또한 `@nestjs/microservices` `@Microservice` 데코레이터로 `Server` 클래스를 장식했습니다. `@Microservice` 데코레이터는 Nest.js에게 이 클래스가 마이크로서비스임을 알립니다.

마지막으로 프로젝트 디렉토리에 `package.json`이라는 파일을 생성합니다. `package.json`에서 마이크로 서비스를 시작할 `start`라는 스크립트를 추가합니다.

```json
{
  "name": "my-microservice",
  "version": "1.0.0",
  "scripts": {
    "start": "nest start"
  },
  "dependencies": {
    "@nestjs/common": "^5.4.0",
    "@nestjs/microservices": "^5.4.0"
  }
}
```

## 마이크로서비스 배포

이제 마이크로서비스를 만들었으니 서버에 배포해 보겠습니다. [Docker](https://www.docker.com/)를 사용하여 마이크로 서비스를 컨테이너로 패키징합니다. 그런 다음 [docker-compose](https://docs.docker.com/compose/)를 사용하여 컨테이너를 서버에 배포합니다.

먼저 프로젝트 디렉터리에 `Dockerfile`이라는 파일을 만듭니다. `Dockerfile`에서 [`node:10-alpine`](https://hub.docker.com/_/node/) Docker 이미지를 사용하고 마이크로서비스가 포트 `3000`에서 실행되도록 지정합니다. . 또한 프로젝트 디렉터리에서 컨테이너로 파일을 복사하고 종속성을 설치합니다.

```Dockerfile
FROM node:10-alpine

WORKDIR /usr/src/app

COPY . .

RUN npm install

EXPOSE 3000

CMD ["npm", "start"]
```

다음으로 프로젝트 디렉터리에 `docker-compose.yml`이라는 파일을 만듭니다. `docker-compose.yml`에서 우리가 만든 `Dockerfile`을 사용하고 포트 `3000`을 노출하도록 지정합니다.

```yaml
version: '3'

services:
  my-microservice:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
```

이제 `Dockerfile` 및 `docker-compose.yml` 파일이 있으므로 마이크로 서비스를 서버에 배포할 수 있습니다. [AWS Elastic Container Service(ECS)](https://aws.amazon.com/ecs/)를 사용하여 컨테이너를 AWS에 배포합니다.

먼저 프로젝트 디렉토리에 `ecs-params.yml`이라는 파일을 생성합니다. `ecs-params.yml`에서 컨테이너의 이름, 컨테이너가 노출될 포트, 컨테이너가 사용할 수 있는 메모리 및 CPU의 양을 지정합니다.

```yaml
version: 1
task_definition:
  task_execution_role:
    Ref: EcsTaskExecutionRole
  container_definitions:
    - name: my-microservice
      image: my-microservice
      portMappings:
        - containerPort: 3000
          hostPort: 3000
      memory: 512
      cpu: 256
```

이제 `ecs-params.yml` 파일이 있으므로 작업 정의를 만들 수 있습니다. 프로젝트 디렉터리에 `ecs-task-definition.json`이라는 파일을 생성합니다. `ecs-task-definition.json`에서 작업 정의의 이름, 작업에서 사용할 IAM 역할, `ecs-params.yml`에서 생성한 컨테이너 정의를 지정합니다.

```json
{
  "family": "my-microservice-task-definition",
  "executionRoleArn": "arn:aws:iam::123456789012:role/ecsTaskExecutionRole",
  "containerDefinitions": [
    {
      "name": "my-microservice",
      "image": "my-microservice",
      "portMappings": [
        {
          "containerPort": 3000,
          "hostPort": 3000
        }
      ],
      "memory": 512,
      "cpu": 256
    }
  ]
}
```

이제 작업 정의가 있으므로 작업 정의를 ECS에 등록할 수 있습니다. 프로젝트 디렉터리에 `ecs-register-task-definition.json`이라는 파일을 생성합니다. `ecs-register-task-definition.json`에서 작업 정의의 이름과 생성한 `ecs-task-definition.json` 파일을 지정합니다.

```json
{
  "taskDefinition": "my-microservice-task-definition",
  "cliInputJson": "file://ecs-task-definition.json"
}
```

마지막으로 서비스를 만들 수 있습니다. 프로젝트 디렉터리에 `ecs-create-service.json`이라는 파일을 생성합니다. `ecs-create-service.json`에서 서비스 이름, 서비스에서 사용할 작업 정의, 서비스에서 실행할 작업 수, 서비스에서 사용할 로드 밸런서를 지정합니다.

```json
{
  "service": "my-microservice-service",
  "taskDefinition": "my-microservice-task-definition",
  "desiredCount": 1,
  "loadBalancer": {
    "elbName": "my-load-balancer",
    "targetGroupArn": "arn:aws:elasticloadbalancing:us-east-1:123456789012:targetgroup/my-target-group/abcdef1234567890"
  }
}
```

이제 `ecs-create-service.json` 파일이 있으므로 서비스를 배포할 수 있습니다. [AWS 명령줄 인터페이스(CLI)](https://aws.amazon.com/cli/)를 사용하여 서비스를 배포합니다. 먼저 `aws ecs register-task-definition` 명령을 사용하여 작업 정의를 등록합니다.

```bash
aws ecs register-task-definition --cli-input-json file://ecs-register-task-definition.json
```

다음으로 `aws ecs create-service` 명령을 사용하여 서비스를 생성합니다.

```bash
aws ecs create-service --cli-input-json file://ecs-create-service.json
```

## 결론

이 기사에서는 TypeScript와 Nest.js를 사용하여 마이크로서비스를 개발하는 방법을 살펴보았습니다. 마이크로서비스에 TypeScript와 Nest.js를 사용할 때의 이점을 살펴보았습니다. 또한 간단한 마이크로서비스를 만들어 서버에 배포했습니다.