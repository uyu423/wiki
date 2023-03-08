---
title: 023: Nest.js에서 템플릿 사용하기
description: 
published: true
date: 2023-02-15T04:32:33.147Z
tags: 
editor: markdown
dateCreated: 2023-02-15T04:32:31.160Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [023: Using templates with Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/023-using-templates-with-nest-js)
{.links-list}


## 소개

Nest.js는 확장 가능한 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. 대규모 개발을 위한 정적 유형 검사 및 강력한 도구를 제공하는 언어인 TypeScript를 사용합니다.

Nest.js 애플리케이션은 개발자가 코드를 애플리케이션 전체에서 재사용할 수 있는 더 작은 조각으로 나눌 수 있는 모듈식 접근 방식을 사용하여 구축됩니다. Nest.js에는 서비스 및 기타 종속성을 구성 요소에 쉽게 주입할 수 있는 종속성 주입 시스템이 내장되어 있습니다.

Nest.js의 가장 강력한 기능 중 하나는 템플릿 사용입니다. Nest.js 템플릿은 널리 사용되는 AngularJS 템플릿 시스템을 기반으로 하며 HTML을 모듈화하고 작성해야 하는 코드의 양을 줄이는 방법을 제공합니다.

이 게시물에서는 Nest.js에서 템플릿을 사용하는 방법을 살펴보겠습니다. 간단한 Nest.js 애플리케이션을 생성하여 시작한 다음 템플릿을 추가합니다. 마지막으로 템플릿을 사용하여 데이터베이스에서 데이터를 렌더링하는 방법을 배웁니다.

## Nest.js 애플리케이션 만들기

새 Nest.js 애플리케이션을 만들어 시작해 보겠습니다. Nest.js CLI를 사용하여 새 애플리케이션을 생성합니다. 먼저 Nest.js CLI가 설치되어 있는지 확인하세요. 설치되어 있지 않은 경우 npm을 사용하여 설치할 수 있습니다.

```
npm install -g @nestjs/cli
```

Nest.js CLI가 설치되면 이를 사용하여 새 애플리케이션을 생성할 수 있습니다. 애플리케이션을 "template-app"이라고 합니다.

```
nest new template-app
```

이렇게 하면 "template-app"이라는 새 디렉토리가 생성되고 기본 Nest.js 애플리케이션에 필요한 파일이 생성됩니다.

## 템플릿 추가

기본 Nest.js 애플리케이션이 있으므로 템플릿을 추가해 보겠습니다. Nest.js는 Nest.js View라는 내장 템플릿 엔진과 함께 제공됩니다. Nest.js View는 널리 사용되는 AngularJS 템플릿 엔진을 기반으로 하며 HTML을 모듈화하고 작성해야 하는 코드의 양을 줄이는 방법을 제공합니다.

Nest.js 애플리케이션에 템플릿을 추가하려면 "src/views" 디렉토리에 "template.html"이라는 새 파일을 만들어야 합니다. "src/views" 디렉토리는 Nest.js가 템플릿을 찾는 곳입니다.

"template.html" 파일에 간단한 HTML 템플릿을 추가합니다.

```html
<html>
  <head>
    <title>Template App</title>
  </head>
  <body>
    <h1>Hello, World!</h1>
  </body>
</html>
```

이제 템플릿이 있으므로 Nest.js 애플리케이션에서 사용하겠습니다.

## 템플릿 사용

템플릿을 사용하려면 Nest.js에 템플릿을 찾을 위치를 알려야 합니다. "src/main.ts" 파일의 "view" 객체에 "template" 속성을 추가하여 이를 수행할 수 있습니다.

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.setViewEngine({
    type: 'html',
    template: './src/views/template.html',
  });

  await app.listen(3000);
}
bootstrap();
```

"템플릿" 속성은 템플릿 파일을 찾을 위치를 Nest.js에 알려줍니다. 이 경우 "src/views" 디렉토리에서 "template.html" 파일을 찾도록 Nest.js에 지시합니다.

템플릿을 찾을 위치를 Nest.js에 알려주었으므로 템플릿을 사용하여 데이터를 렌더링할 수 있습니다.

## 렌더링 데이터

템플릿에서 데이터를 렌더링하려면 "렌더링" 기능을 사용해야 합니다. "렌더링" 함수는 데이터 개체와 응답 개체라는 두 가지 인수를 사용합니다. 데이터 개체에는 렌더링하려는 데이터가 포함되어 있으며 응답 개체는 렌더링된 HTML을 클라이언트에 보내는 데 사용됩니다.

한 가지 예를 살펴보겠습니다. 이 예에서는 템플릿에서 사용자 목록을 렌더링합니다.

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.setViewEngine({
    type: 'html',
    template: './src/views/template.html',
  });

  app.get('/users', (req, res) => {
    const users = [
      {
        name: 'John Doe',
        age: 30,
      },
      {
        name: 'Jane Doe',
        age: 31,
      },
    ];

    res.render('users', { users });
  });

  await app.listen(3000);
}
bootstrap();
```

이 예에서는 사용자 목록을 렌더링하는 Nest.js 애플리케이션에 새 경로를 추가했습니다. "렌더링" 기능을 사용하여 "사용자" 템플릿을 렌더링하고 사용자 목록이 포함된 데이터 개체를 전달합니다.

이제 Nest.js 템플릿에서 데이터를 렌더링하는 방법을 살펴보았으므로 템플릿에서 데이터에 액세스하는 방법을 살펴보겠습니다.

## 템플릿의 데이터에 액세스

템플릿의 데이터에 액세스하려면 "render" 함수의 "data" 인수를 사용합니다. "data" 인수는 렌더링하려는 데이터를 포함하는 개체입니다.

"template.html" 파일에서 다음과 같이 "render" 함수를 사용하여 전달한 데이터에 액세스할 수 있습니다.

```html
<html>
  <head>
    <title>Template App</title>
  </head>
  <body>
    <h1>Users</h1>
    <ul>
      <li>
        {{ users[0].name }} - {{ users[0].age }}
      </li>
      <li>
        {{ users[1].name }} - {{ users[1].age }}
      </li>
    </ul>
  </body>
</html>
```

이 예제에서는 "render" 함수의 "data" 인수를 사용하여 전달한 사용자 목록에 액세스합니다. 그런 다음 사용자 목록을 반복하고 이름과 나이를 렌더링합니다.

이제 Nest.js에서 템플릿을 사용하는 방법을 살펴보았으므로 더 읽을 수 있는 몇 가지 리소스를 살펴보겠습니다.

## 더 읽을 수 있는 리소스

- [Nest.js 보기](https://docs.nestjs.com/v/6/view)
- [AngularJS](https://angularjs.org/)
- [핸들바](https://handlebarsjs.com/)