---
title: 035: Nest.js를 React와 함께 사용하기
description: 
published: true
date: 2023-02-02T00:18:31.537Z
tags: 
editor: markdown
dateCreated: 2023-02-02T00:18:29.874Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [035: Using Nest.js with React***English** document is available*](/en/Knowledge-base/Nest-js/Learning/035-using-nest-js-with-react)
{.links-list}


# 소개

Nest.js는 확장 가능한 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. JavaScript의 상위 집합인 TypeScript를 사용하고 기능 및 객체 지향 프로그래밍의 요소를 결합합니다.

React는 사용자 인터페이스를 구축하기 위한 JavaScript 라이브러리입니다. 선언적이고 효율적이며 유연합니다.

이번 포스트에서는 Nest.js를 React와 함께 사용하는 방법을 알아보겠습니다.

# 프로젝트 설정

우리는 create-react-app CLI를 사용하여 React 프로젝트를 생성할 것입니다.

```
npx create-react-app nestjs-react-app
```

그러면 다음 구조로 `nestjs-react-app`이라는 디렉토리가 생성됩니다.

```
nestjs-react-app/
├── README.md
├── node_modules/
├── package.json
├── .gitignore
├── public/
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
└── src/
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
    └── serviceWorker.js
```

우리는 프로젝트의 React 및 Nest.js 부분 모두에 TypeScript를 사용할 것입니다.

먼저 TypeScript 컴파일러와 React 및 React-DOM에 대한 유형 정의를 설치해야 합니다.

```
npm install --save-dev typescript @types/react @types/react-dom
```

다음으로 React 및 React-DOM 정의를 포함하도록 `tsconfig.json` 파일을 수정해야 합니다.

```
{
  "compilerOptions": {
    ...
  },
  "include": [
    "src/**/*"
  ],
  "exclude": [
    "node_modules",
    "**/*.spec.ts"
  ]
}
```

또한 React 및 React-DOM 정의를 포함하도록 `jsconfig.json` 파일을 수정해야 합니다.

```
{
  "compilerOptions": {
    "target": "es6",
    "jsx": "react"
  },
  "include": [
    "src/**/*"
  ]
}
```

이제 TypeScript를 설정했으므로 다음 명령을 사용하여 Nest.js를 설치할 수 있습니다.

```
npm install --save @nestjs/core @nestjs/common rxjs reflect-metadata
```

# Nest.js 서버 생성

먼저 `src` 디렉토리에 `server.ts`라는 파일을 생성합니다. 이 파일에는 Nest.js 서버용 코드가 포함됩니다.

```
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

`server.ts` 파일에서 먼저 `@nestjs/core`에서 `NestFactory` 및 `AppModule`을 가져옵니다.

NestFactory는 Nest.js 애플리케이션 인스턴스를 생성하는 데 사용됩니다. `AppModule`은 우리 애플리케이션의 코드를 포함하는 모듈입니다.

그런 다음 Nest.js 서버를 시작하는 데 사용할 `bootstrap`이라는 `async` 함수를 정의합니다.

`bootstrap` 함수 내에서 `NestFactory`를 사용하여 `AppModule`의 인스턴스를 만든 다음 `listen` 메서드를 호출하여 서버를 시작합니다.

# React 프런트엔드 만들기

먼저 `src` 디렉토리에 `App.tsx`라는 파일을 생성합니다. 이 파일에는 React 프런트엔드용 코드가 포함됩니다.

```
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <h1>Hello, world!</h1>
    </div>
  );
}

export default App;
```

`App.tsx` 파일에서 먼저 React와 `App.css` 파일을 가져옵니다.

그런 다음 `div` 요소를 반환하는 `App`이라는 함수를 정의합니다. `div` 요소 안에는 "Hello, world!"라는 텍스트를 포함하는 `h1` 요소가 있습니다.

마지막으로 프로그램의 다른 부분에서 사용할 수 있도록 `App` 함수를 내보냅니다.

# React와 Nest.js 연결하기

다음 코드를 포함하도록 `server.ts` 파일을 수정하여 시작하겠습니다.

```
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { NestExpressApplication } from '@nestjs/platform-express';
import { join } from 'path';

async function bootstrap() {
  const app = await NestFactory.create<NestExpressApplication>(
    AppModule,
  );
  app.useStaticAssets(join(__dirname, '..', 'public'));
  app.setBaseViewsDir(join(__dirname, '..', 'views'));
  app.setViewEngine('hbs');
  await app.listen(3000);
}
bootstrap();
```

`server.ts` 파일에서 먼저 `@nestjs/core`에서 `NestFactory`, `AppModule` 및 `NestExpressApplication`을 가져옵니다.

또한 `path` 모듈에서 `join` 기능을 가져옵니다.

NestFactory는 Nest.js 애플리케이션 인스턴스를 생성하는 데 사용됩니다. `AppModule`은 우리 애플리케이션의 코드를 포함하는 모듈입니다. 'NestExpressApplication'은 Express 서버를 구성하는 데 사용됩니다.

그런 다음 Nest.js 서버를 시작하는 데 사용할 `bootstrap`이라는 `async` 함수를 정의합니다.

`bootstrap` 함수 내에서 `NestFactory`를 사용하여 `AppModule`의 인스턴스를 만든 다음 `useStaticAssets` 및 `setBaseViewsDir` 메서드를 호출하여 Express 서버를 구성합니다.

마지막으로 `listen` 메서드를 호출하여 서버를 시작합니다.

# Nest.js에서 React 렌더링

다음 코드를 포함하도록 `server.ts` 파일을 수정하여 시작하겠습니다.

```
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { NestExpressApplication } from '@nestjs/platform-express';
import { join } from 'path';
import { renderFile } from 'pug';

async function bootstrap() {
  const app = await NestFactory.create<NestExpressApplication>(
    AppModule,
  );
  app.useStaticAssets(join(__dirname, '..', 'public'));
  app.setBaseViewsDir(join(__dirname, '..', 'views'));
  app.setViewEngine('pug');
  app.get('/', (req, res) => {
    res.render('index', {
      message: 'Hello, world!',
    });
  });
  await app.listen(3000);
}
bootstrap();
```

`server.ts` 파일에서 먼저 `pug` 모듈에서 `NestFactory`, `AppModule`, `NestExpressApplication`, `join` 함수 및 `renderFile` 함수를 가져옵니다.

NestFactory는 Nest.js 애플리케이션 인스턴스를 생성하는 데 사용됩니다. `AppModule`은 우리 애플리케이션의 코드를 포함하는 모듈입니다. 'NestExpressApplication'은 Express 서버를 구성하는 데 사용됩니다.

그런 다음 Nest.js 서버를 시작하는 데 사용할 `bootstrap`이라는 `async` 함수를 정의합니다.

`bootstrap` 함수 내에서 `NestFactory`를 사용하여 `AppModule`의 인스턴스를 만든 다음 `useStaticAssets`, `setBaseViewsDir` 및 `setViewEngine` 메서드를 호출하여 Express 서버를 구성합니다.

다음으로 `index.pug` 템플릿을 렌더링하는 `/` 경로에 대한 경로 핸들러를 정의합니다.

마지막으로 `listen` 메서드를 호출하여 서버를 시작합니다.

# Nest.js에서 React로 데이터 전달

다음 코드를 포함하도록 `server.ts` 파일을 수정하여 시작하겠습니다.

```
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { NestExpressApplication } from '@nestjs/platform-express';
import { join } from 'path';
import { renderFile } from 'pug';

async function bootstrap() {
  const app = await NestFactory.create<NestExpressApplication>(
    AppModule,
  );
  app.useStaticAssets(join(__dirname, '..', 'public'));
  app.setBaseViewsDir(join(__dirname, '..', 'views'));
  app.setViewEngine('pug');
  app.get('/', (req, res) => {
    res.render('index', {
      message: 'Hello, world!',
    });
  });
  await app.listen(3000);
}
bootstrap();
```

`server.ts` 파일에서 먼저 `pug` 모듈에서 `NestFactory`, `AppModule`, `NestExpressApplication`, `join` 함수 및 `renderFile` 함수를 가져옵니다.

NestFactory는 Nest.js 애플리케이션 인스턴스를 생성하는 데 사용됩니다. `AppModule`은 우리 애플리케이션의 코드를 포함하는 모듈입니다. 'NestExpressApplication'은 Express 서버를 구성하는 데 사용됩니다.

그런 다음 Nest.js 서버를 시작하는 데 사용할 `bootstrap`이라는 `async` 함수를 정의합니다.

`bootstrap` 함수 내에서 `NestFactory`를 사용하여 `AppModule`의 인스턴스를 만든 다음 `useStaticAssets`, `setBaseViewsDir` 및 `setViewEngine` 메서드를 호출하여 Express 서버를 구성합니다.

다음으로 `index.pug` 템플릿을 렌더링하는 `/` 경로에 대한 경로 핸들러를 정의합니다.

마지막으로 `listen` 메서드를 호출하여 서버를 시작합니다.

# React에서 Nest.js로 데이터 전달

다음 코드를 포함하도록 `App.tsx` 파일을 수정하여 시작하겠습니다.

```
import React from 'react';
import './App.css';

function App() {
  const [message, setMessage] = React.useState('Hello, world!');
  return (
    <div className="App">
      <h1>{message}</h1>
      <button onClick={() => setMessage('Nest.js is awesome!')}>
        Click me!
      </button>
    </div>
  );
}

export default App;
```

`App.tsx` 파일에서 먼저 React와 `App.css` 파일을 가져옵니다.

그런 다음 `div` 요소를 반환하는 `App`이라는 함수를 정의합니다. `div` 요소 안에는 "Hello, world!"라는 텍스트를 포함하는 `h1` 요소가 있습니다.

또한 클릭 시 `h1` 요소의 텍스트를 "Nest.js is awesome!"으로 변경하는 `button` 요소도 있습니다.

마지막으로 프로그램의 다른 부분에서 사용할 수 있도록 `App` 함수를 내보냅니다.

# 결론

이번 포스트에서는 Nest.js를 React와 함께 사용하는 방법에 대해 알아보았습니다.

프로젝트 설정부터 시작한 다음 Nest.js 서버를 만들었습니다.

다음으로 React 프런트엔드를 만들고 React와 Nest.js를 연결했습니다.

마지막으로 Nest.js에서 React로, React에서 Nest.js로 데이터를 전달하는 방법을 살펴보았습니다.