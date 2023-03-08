---
title: TypeScript 애플리케이션에서 역할 기반 액세스 제어 구현
description: 
published: true
date: 2023-02-01T08:05:50.332Z
tags: 
editor: markdown
dateCreated: 2023-02-01T08:05:46.878Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Implementing Role-Based Access Control in TypeScript Applications***English** version of this document is available*](/en/Knowledge-base/TypeScript/implementing-role-based-access-control-in-typescript-applications)
{.links-list}


  TypeScript 애플리케이션에서 역할 기반 액세스 제어 구현

RBAC(역할 기반 액세스 제어)는 애플리케이션에서 일반적으로 사용되는 권한에 대한 모델입니다. RBAC에서 각 사용자에게는 하나 이상의 역할이 할당되며 각 역할에는 일련의 권한이 있습니다. 이 모델은 유연하고 확장 가능하며 다양한 사용자에게 애플리케이션의 다양한 부분에 대한 다양한 수준의 액세스를 제공하는 데 사용할 수 있습니다.

이 기사에서는 node-acl 패키지를 사용하여 TypeScript 애플리케이션에서 RBAC를 구현하는 방법을 보여줍니다. 먼저 두 명의 사용자와 두 개의 역할이 있는 간단한 애플리케이션을 만듭니다. 그런 다음 애플리케이션에 RBAC를 추가하고 이를 사용하여 사용자 역할에 따라 애플리케이션의 특정 부분에 대한 액세스를 제한합니다.

## 신청

두 명의 사용자와 두 개의 역할이 있는 간단한 TypeScript 애플리케이션을 만드는 것부터 시작하겠습니다. 사용자와 역할은 단순성을 위해 애플리케이션에 하드 코딩됩니다. 실제 애플리케이션에서는 이 정보를 데이터베이스에 저장할 가능성이 높습니다.

애플리케이션에는 홈페이지와 프로필 페이지의 두 페이지가 있습니다. 홈페이지는 모든 사용자가 액세스할 수 있지만 프로필 페이지는 로그인한 사용자만 액세스할 수 있습니다.

홈 페이지는 다음과 같이 표시됩니다.

![홈페이지](https://i.imgur.com/P0jrQbu.png)

프로필 페이지는 다음과 같습니다.

![프로필 페이지](https://i.imgur.com/TK7gNcu.png)

사용자는 홈 페이지의 로그인 양식을 사용하여 애플리케이션에 로그인 및 로그아웃할 수 있습니다. 사용자가 로그인하면 사용자 이름이 프로필 페이지에 표시됩니다.

RBAC에 초점을 맞추기 위해 이 문서에서는 전체 인증 시스템을 구현하지 않습니다. 대신 사용자가 로그인할 때 단순히 세션 변수를 설정합니다. 실제 애플리케이션에서는 JSON 웹 토큰과 같은 보다 안전한 인증 방법을 사용하고 싶을 것입니다.

애플리케이션 코드는 이 [GitHub 리포지토리](https://github.com/auth0-blog/typescript-rbac-app)에서 사용할 수 있습니다.

## 프로젝트 설정

RBAC 구현을 시작하기 전에 프로젝트를 설정해야 합니다. 먼저 새로운 TypeScript 프로젝트를 생성해야 합니다. TypeScript 웹사이트에서 [TypeScript 템플릿](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)을 사용하여 이 작업을 수행할 수 있습니다.

프로젝트가 생성되면 프로젝트에 필요한 종속성을 설치해야 합니다. 이 경우 RBAC를 구현하기 위해서는 [Express](https://expressjs.com/) 웹 프레임워크와 [node-acl](https://www.npmjs.com/package/node-acl) 패키지가 필요합니다. . npm을 사용하여 이러한 종속성을 설치할 수 있습니다.

```
npm install express node-acl --save
```

또한 [TypeScript](https://www.typescriptlang.org/) 컴파일러와 [Webpack](https://webpack.js.org/) 모듈 번들러를 설치해야 합니다. npm을 사용하여 이러한 종속성을 설치할 수도 있습니다.

```
npm install typescript webpack webpack-cli --save-dev
```

## RBAC 구현

이제 프로젝트가 설정되었으므로 RBAC 구현을 시작할 수 있습니다. 먼저 `src` 디렉토리에 `acl.ts`라는 새 파일을 생성합니다. 이 파일에는 node-acl 패키지를 설정하고 사용하기 위한 코드가 포함됩니다.

먼저 node-acl 패키지와 Express Request 및 Response 인터페이스를 가져와야 합니다. ACL 데이터를 메모리에 저장하는 데 사용할 node-acl MemoryBackend도 가져올 것입니다.

```typescript
import * as acl from 'acl';
import { Request, Response } from 'express';
import { MemoryBackend } from 'acl';
```

다음으로 node-acl MemoryBackend의 새 인스턴스를 생성해야 합니다. 또한 ACL을 만들고 관리하는 데 사용할 node-acl acl 클래스의 새 인스턴스를 만듭니다.

```typescript
const backend = new MemoryBackend();
const acl = new acl(backend);
```

이제 백엔드 및 ACL 인스턴스가 설정되었으므로 애플리케이션에 대한 역할 및 권한 생성을 시작할 수 있습니다.

`user`와 `admin`이라는 두 가지 역할을 만드는 것으로 시작하겠습니다. `사용자` 역할에는 사용자가 홈 페이지를 볼 수 있는 `보기` 권한이 있습니다. `admin` 역할에는 `view` 및 `edit` 권한이 있으며 관리자는 프로필 페이지를 보고 편집할 수 있습니다.

```typescript
acl.allow([
  {
    roles: ['user'],
    allows: [
      { resources: '/', permissions: 'view' }
    ]
  },
  {
    roles: ['admin'],
    allows: [
      { resources: '/', permissions: 'view' },
      { resources: '/profile', permissions: 'edit' }
    ]
  }
]);
```

또한 'guest' 역할을 생성해야 합니다. 이 역할에는 권한이 없으므로 게스트가 애플리케이션의 어떤 부분에도 액세스할 수 없습니다.

```typescript
acl.addRoleParents('guest', []);
```

이제 역할과 권한이 설정되었으므로 ACL을 확인하여 사용자에게 특정 리소스에 대한 액세스 권한이 있는지 확인하는 미들웨어 기능을 만들어야 합니다.

먼저 Express Request 및 Response 인터페이스를 가져와야 합니다. node-acl acl 클래스도 가져옵니다.

```typescript
import { Request, Response } from 'express';
import { acl } from 'acl';
```

다음으로 `checkPermission`이라는 새로운 미들웨어 함수를 생성합니다.

```typescript
function checkPermission(resource: string, action: string) {
  return (req: Request, res: Response, next: Function) => {
    acl.isAllowed(req.session.user, resource, action, (err: Error, allowed: boolean) => {
      if (err) {
        next(err);
      } else if (allowed) {
        next();
      } else {
        res.status(403).send('Forbidden');
      }
    });
  };
}
```

이 미들웨어 기능은 사용자가 액세스하려는 리소스와 해당 리소스에서 수행하려는 작업의 두 가지 인수를 사용합니다. acl 인스턴스의 `isAllowed` 메서드는 사용자가 리소스에 액세스할 수 있는 권한이 있는지 확인하는 데 사용됩니다. 사용자에게 권한이 없으면 '403' 상태 코드가 반환됩니다.

## 애플리케이션에 RBAC 추가

이제 미들웨어 기능이 설정되었으므로 애플리케이션에 추가할 수 있습니다.

먼저 `express` 및 `body-parser` 패키지를 가져와야 합니다. 이전 섹션에서 만든 `./acl` 파일도 가져옵니다.

```typescript
import * as express from 'express';
import * as bodyParser from 'body-parser';
import * as acl from './acl';
```

다음으로 새 Express 애플리케이션을 만들고 `body-parser` 미들웨어를 사용하도록 구성합니다.

```typescript
const app = express();
app.use(bodyParser.json());
```

이제 경로 추가를 시작할 수 있습니다.

추가할 첫 번째 경로는 `GET /` 경로입니다. 이 경로는 애플리케이션의 홈 페이지를 렌더링합니다.

```typescript
app.get('/', (req: Request, res: Response) => {
  res.send(`
    <html>
      <head>
        <title>Home</title>
      </head>
      <body>
        <h1>Home</h1>
        ${req.session.user ? `<p>Welcome, ${req.session.user}!</p>` : ''}
        <a href="/profile">Profile</a>
      </body>
    </html>
  `);
});
```

다음으로 `GET /profile` 경로를 추가합니다. 이 경로는 응용 프로그램의 프로필 페이지를 렌더링합니다.

```typescript
app.get('/profile', checkPermission('/profile', 'view'), (req: Request, res: Response) => {
  res.send(`
    <html>
      <head>
        <title>Profile</title>
      </head>
      <body>
        <h1>Profile</h1>
        <p>Welcome, ${req.session.user}!</p>
        <a href="/">Home</a>
      </body>
    </html>
  `);
});
```

이 경로에 `checkPermission` 미들웨어 기능을 추가했습니다. 이렇게 하면 '보기' 권한이 있는 사용자만 이 경로에 액세스할 수 있습니다.

마지막으로 `POST /login` 경로를 추가합니다. 이 경로는 사용자가 애플리케이션에 로그인 및 로그아웃하는 데 사용됩니다.

```typescript
app.post('/login', (req: Request, res: Response) => {
  const { user } = req.body;
  req.session.user = user;
  res.redirect('/');
});
```

이 경로는 세션 개체의 `user` 속성을 요청 본문에 전달된 사용자 이름으로 설정합니다.

## 애플리케이션 테스트

이제 애플리케이션을 설정했으므로 테스트하여 RBAC가 예상대로 작동하는지 확인할 수 있습니다.

먼저 애플리케이션을 빌드해야 합니다. `webpack` 명령을 사용하여 이 작업을 수행할 수 있습니다.

```
webpack
```

다음으로 애플리케이션을 시작해야 합니다. `node` 명령을 사용하여 이를 수행할 수 있습니다.

```
node ./dist/bundle.js
```

이제 웹 브라우저에서 애플리케이션을 열고 테스트할 수 있습니다.

로그인하지 않고 `/profile` 경로에 액세스하려고 하면 다음 오류 메시지가 표시됩니다.

![오류 메시지](https://i.imgur.com/vALDKd7.png)

이는 `guest` 역할에 `/profile` 경로에 대한 `보기` 권한을 부여하지 않았기 때문에 예상되는 동작입니다.

`user` 역할로 로그인하면 홈페이지에 액세스할 수 있지만 프로필 페이지에는 액세스할 수 없어야 합니다.

![홈페이지](https://i.imgur.com/P0jrQbu.png)

![프로필 페이지](https://i.imgur.com/TK7gNcu.png)

이는 `user` 역할에 `/` 경로에 대한 `view` 권한만 부여했기 때문에 예상되는 동작입니다.

`admin` 역할로 로그인하면 홈페이지와 프로필 페이지에 액세스할 수 있어야 합니다.

![홈페이지](https://i.imgur.com/P0jrQbu.png)

![프로필 페이지](https://i.imgur.com/TK7gNcu.png)

이는 `admin` 역할에 `/` 및 `/profile` 경로에 대한 `view` 및 `edit` 권한을 부여했기 때문에 예상되는 동작입니다.

## 결론

이 기사에서는 node-acl 패키지를 사용하여 TypeScript 애플리케이션에서 RBAC를 구현하는 방법을 보여주었습니다. 우리는 2명의 사용자와 2개의 역할을 가진 간단한 애플리케이션을 만들었습니다. 그런 다음 RBAC를 응용 프로그램에 추가하고 이를 사용하여 사용자 역할에 따라 응용 프로그램의 특정 부분에 대한 액세스를 제한했습니다.

RBAC에 대해 자세히 알아보려면 다음 리소스를 참조하십시오.

- Wikipedia의 [역할 기반 액세스 제어](https://en.wikipedia.org/wiki/Role-based_access_control)
- [node-acl 문서](https://github.com/OptimalBits/node-acl)
- [익스프레스 문서](https://expressjs.com/en/guide/rbac.html)