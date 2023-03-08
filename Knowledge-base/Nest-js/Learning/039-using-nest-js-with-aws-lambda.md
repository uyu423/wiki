---
title: 039: AWS Lambda와 함께 Nest.js 사용
description: 
published: true
date: 2023-02-09T03:17:45.429Z
tags: 
editor: markdown
dateCreated: 2023-02-09T03:17:43.707Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [039: Using Nest.js with AWS Lambda***English** document is available*](/en/Knowledge-base/Nest-js/Learning/039-using-nest-js-with-aws-lambda)
{.links-list}


# 039: AWS Lambda와 함께 Nest.js 사용하기

AWS Lambda는 서버를 프로비저닝하거나 관리하지 않고도 코드를 실행할 수 있는 서버리스 컴퓨팅 플랫폼입니다. Nest.js는 효율적이고 확장 가능한 Node.js 서버 측 애플리케이션을 구축하기 위한 프레임워크입니다.

이 게시물에서는 AWS Lambda와 함께 Nest.js를 사용하는 방법을 보여드리겠습니다. 간단한 Nest.js 애플리케이션을 만들어 AWS Lambda에 배포합니다.

## Nest.js 애플리케이션 만들기

먼저 Nest.js 애플리케이션을 만들어야 합니다. Nest.js CLI를 사용하여 새 프로젝트를 생성할 수 있습니다.

```
$ nest new nest-lambda
```

이렇게 하면 `nest-lambda`라는 폴더에 새 Nest.js 프로젝트가 생성됩니다.

다음으로 `@nestjs/aws-lambda` 패키지를 설치해야 합니다. 이 패키지는 AWS Lambda용 Nest.js 어댑터를 제공합니다.

```
$ cd nest-lambda
$ npm install --save @nestjs/aws-lambda
```

이제 `@nestjs/aws-lambda` 패키지가 설치되었으므로 `src` 폴더에 `main.ts`라는 새 파일을 생성할 수 있습니다. 이 파일에는 Nest.js 애플리케이션이 포함됩니다.

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

이 파일에서는 Nest.js에서 `NestFactory` 및 `AppModule`을 가져왔습니다. 그런 다음 'NestFactory'를 사용하여 새로운 Nest.js 애플리케이션을 만들었습니다. `AppModule`을 `NestFactory`에 전달했습니다. 마지막으로 `listen` 메서드를 호출하여 포트 3000에서 Nest.js 애플리케이션을 시작했습니다.

## AWS Lambda에 배포

이제 Nest.js 애플리케이션이 있으므로 AWS Lambda에 배포할 수 있습니다. 먼저 AWS 계정을 생성해야 합니다. 계정이 있으면 새 AWS Lambda 함수를 생성할 수 있습니다.

Lambda 콘솔에서 "Create Function" 버튼을 클릭합니다.

![만들기 기능](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-create-function.png)

"함수 만들기" 페이지에서 "처음부터 작성" 옵션을 선택합니다.

![스크래치에서 작성자](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-author-from-scratch.png)

"함수 구성" 페이지에서 함수 이름을 입력하고 "Node.js 12.x" 런타임을 선택합니다. 그런 다음 아래로 스크롤하여 "함수 만들기" 버튼을 클릭합니다.

![configure-function](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-configure-function.png)

함수가 생성되면 "함수 코드" 편집기가 표시됩니다. 이 편집기에서 Nest.js 애플리케이션 코드를 추가합니다.

먼저 `@nestjs/aws-lambda` 패키지를 설치해야 합니다. `npm` 명령을 사용하여 이 작업을 수행할 수 있습니다.

```
$ npm install --save @nestjs/aws-lambda
```

다음으로 `main.ts` 파일을 "함수 코드" 편집기에 추가합니다.

![기능 코드](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-function-code.png)

코드를 추가했으면 함수에 대한 "처리기"를 선택해야 합니다. 핸들러는 Lambda 함수의 진입점입니다. 우리의 경우 핸들러는 `main.handler`입니다.

![핸들러](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-handler.png)

이제 기능을 구성했으므로 아래로 스크롤하여 "저장" 버튼을 클릭할 수 있습니다.

![저장](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-save.png)

기능이 저장되면 "테스트" 버튼을 클릭하여 테스트할 수 있습니다.

![테스트](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-test.png)

"테스트 이벤트 구성" 페이지에서 새 테스트 이벤트를 만들 수 있습니다. 이 이벤트에서는 `httpMethod`를 `GET`으로, `path`를 `/`로 설정합니다. 그런 다음 "만들기" 버튼을 클릭합니다.

![configure-test-event](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-configure-test-event.png)

테스트 이벤트가 생성되면 "테스트" 버튼을 클릭하여 함수를 실행할 수 있습니다.

![테스트-2](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-test-2.png)

모든 것이 잘 되었다면 '200' 상태 코드와 함께 "실행 결과" 섹션이 표시되어야 합니다.

![실행 결과](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-execution-result.png)

## 결론

이 게시물에서는 AWS Lambda와 함께 Nest.js를 사용하는 방법을 보여주었습니다. 간단한 Nest.js 애플리케이션을 만들어 AWS Lambda에 배포했습니다.