---
title: Jest 및 Supertest로 TypeScript 애플리케이션 테스트
description: 
published: true
date: 2023-02-13T03:55:34.375Z
tags: 
editor: markdown
dateCreated: 2023-02-13T03:55:32.802Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Testing TypeScript Applications with Jest and Supertest***English** document is available*](/en/Knowledge-base/TypeScript/testing-typescript-applications-with-jest-and-supertest)
{.links-list}


# Jest와 Supertest로 TypeScript 애플리케이션 테스트하기

TypeScript는 개발자가 대규모 웹 애플리케이션을 구축할 수 있게 해주는 강력한 프로그래밍 언어입니다. Jest 또는 Supertest를 사용하는 데 TypeScript가 필수는 아니지만 이러한 테스트 도구와 함께 TypeScript를 사용하면 도움이 될 수 있습니다. 이 기사에서는 TypeScript와 함께 Jest 및 Supertest를 설정하고 사용하는 방법을 보여줍니다.

## TypeScript로 Jest 및 Supertest 설정

TypeScript와 함께 Jest 및 Supertest를 사용하려면 먼저 프로젝트를 설정해야 합니다. 먼저 종속 항목을 설치합니다.

```
npm install --save-dev jest @types/jest ts-jest supertest @types/supertest
```

다음으로 프로젝트의 루트에 `jest.config.js`라는 파일을 만들고 다음 구성을 추가합니다.

```js
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node',
};
```

이것은 Jest에게 TypeScript 컴파일러를 사용하고 Node.js 환경에서 테스트를 실행하도록 지시합니다.

마지막으로 프로젝트의 루트에 `tests.ts`라는 파일을 만들고 다음 코드를 추가합니다.

```ts
import supertest from 'supertest';

const request = supertest('http://localhost:3000');

test('GET /', async () => {
  const response = await request.get('/');
  expect(response.status).toEqual(200);
});
```

이 코드는 `supertest` 라이브러리를 가져오고 서버에 HTTP 요청을 하는 데 사용할 새 `request` 개체를 만듭니다. 'test' 함수는 테스트 사례를 정의하는 데 사용됩니다. 이 경우 테스트 케이스는 `/`에 `GET` 요청을 하고 응답 상태 코드가 `200`인지 확인합니다.

## 테스트 실행

테스트를 실행하려면 `jest` 명령을 사용할 수 있습니다.

```
jest
```

이렇게 하면 프로젝트의 모든 테스트가 실행됩니다. `test` 이름을 인수로 전달하여 특정 테스트를 실행할 수도 있습니다.

```
jest testName
```

## 테스트 작성

Jest와 Supertest로 테스트를 작성하는 방법에는 여러 가지가 있습니다. 이 섹션에서는 몇 가지 일반적인 시나리오를 살펴보겠습니다.

### HTTP 메서드 테스트

Jest와 Supertest는 `GET`, `POST`, `PUT`, `DELETE` 등 모든 HTTP 메서드를 테스트하는 데 사용할 수 있습니다. 예를 들어 다음 테스트 케이스는 `POST` 요청을 테스트합니다.

```ts
test('POST /users', async () => {
  const response = await request.post('/users')
    .send({
      name: 'John',
      age: 20,
    });
  expect(response.status).toEqual(201);
  expect(response.body).toEqual({
    id: 1,
    name: 'John',
    age: 20,
  });
});
```

이 테스트 사례는 JSON 본문을 사용하여 `/users`에 대한 `POST` 요청을 만듭니다. `send` 메서드는 요청 본문을 설정하는 데 사용됩니다. 응답의 `status` 및 `body` 속성이 예상 값과 비교됩니다.

### 미들웨어 테스트

Jest와 Supertest는 미들웨어를 테스트하는 데에도 사용할 수 있습니다. 예를 들어 다음 테스트 사례는 사용자를 인증하는 데 사용되는 미들웨어 기능을 테스트합니다.

```ts
test('POST /auth', async () => {
  const response = await request.post('/auth')
    .send({
      username: 'test',
      password: 'test',
    });
  expect(response.status).toEqual(200);
  expect(response.body).toEqual({
    token: 'abcdefg',
  });
});
```

이 테스트 사례는 JSON 본문을 사용하여 `/auth`에 대한 `POST` 요청을 만듭니다. `send` 메서드는 요청 본문을 설정하는 데 사용됩니다. 응답의 `status` 및 `body` 속성이 예상 값과 비교됩니다.

### 오류 처리 테스트

Jest와 Supertest는 오류 처리를 테스트하는 데에도 사용할 수 있습니다. 예를 들어 다음 테스트 사례는 오류를 처리하는 데 사용되는 미들웨어 기능을 테스트합니다.

```ts
test('GET /error', async () => {
  const response = await request.get('/error');
  expect(response.status).toEqual(500);
  expect(response.body).toEqual({
    error: 'Internal server error',
  });
});
```

이 테스트 케이스는 `/error`에 `GET` 요청을 합니다. 응답의 `status` 및 `body` 속성이 예상 값과 비교됩니다.

## 결론

Jest와 Supertest는 TypeScript 애플리케이션을 테스트하는 데 사용할 수 있는 강력한 도구입니다. 이 기사에서는 TypeScript와 함께 Jest 및 Supertest를 설정하고 사용하는 방법을 살펴보았습니다. 일반적인 시나리오에 대한 테스트를 작성하는 방법도 살펴보았습니다.