---
title: Testing TypeScript Applications with Jest and Supertest
description: 
published: true
date: 2023-02-13T03:55:39.562Z
tags: 
editor: markdown
dateCreated: 2023-02-13T03:55:32.837Z
---

- [Prueba de aplicaciones TypeScript con Jest y Supertest***Spanish** document is available*](/es/Knowledge-base/TypeScript/testing-typescript-applications-with-jest-and-supertest)
{.links-list}
- [使用 Jest 和 Supertest 测试 TypeScript 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/TypeScript/testing-typescript-applications-with-jest-and-supertest)
{.links-list}
- [Jest 및 Supertest로 TypeScript 애플리케이션 테스트***Korean** document is available*](/ko/Knowledge-base/TypeScript/testing-typescript-applications-with-jest-and-supertest)
{.links-list}


# Testing TypeScript Applications with Jest and Supertest

TypeScript is a powerful programming language that enables developers to build large-scale web applications. While TypeScript is not required to use Jest or Supertest, it can be helpful to use TypeScript in conjunction with these testing tools. This article will show you how to set up and use Jest and Supertest with TypeScript.

## Setting up Jest and Supertest with TypeScript

Before you can start using Jest and Supertest with TypeScript, you need to set up your project. First, install the dependencies:

```
npm install --save-dev jest @types/jest ts-jest supertest @types/supertest
```

Next, create a file called `jest.config.js` in the root of your project and add the following configuration:

```js
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node',
};
```

This tells Jest to use the TypeScript compiler and to run tests in a Node.js environment.

Finally, create a file called `tests.ts` in the root of your project and add the following code:

```ts
import supertest from 'supertest';

const request = supertest('http://localhost:3000');

test('GET /', async () => {
  const response = await request.get('/');
  expect(response.status).toEqual(200);
});
```

This code imports the `supertest` library and creates a new `request` object that will be used to make HTTP requests to the server. The `test` function is used to define a test case. In this case, the test case makes a `GET` request to `/` and checks that the response status code is `200`.

## Running tests

To run the tests, you can use the `jest` command:

```
jest
```

This will run all tests in your project. You can also run a specific test by passing the `test` name as an argument:

```
jest testName
```

## Writing tests

There are many different ways to write tests with Jest and Supertest. In this section, we'll look at a few common scenarios.

### Testing HTTP methods

Jest and Supertest can be used to test all HTTP methods: `GET`, `POST`, `PUT`, `DELETE`, etc. For example, the following test case tests a `POST` request:

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

This test case makes a `POST` request to `/users` with a JSON body. The `send` method is used to set the request body. The `status` and `body` properties of the response are compared to the expected values.

### Testing middleware

Jest and Supertest can also be used to test middleware. For example, the following test case tests a middleware function that is used to authenticate users:

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

This test case makes a `POST` request to `/auth` with a JSON body. The `send` method is used to set the request body. The `status` and `body` properties of the response are compared to the expected values.

### Testing error handling

Jest and Supertest can also be used to test error handling. For example, the following test case tests a middleware function that is used to handle errors:

```ts
test('GET /error', async () => {
  const response = await request.get('/error');
  expect(response.status).toEqual(500);
  expect(response.body).toEqual({
    error: 'Internal server error',
  });
});
```

This test case makes a `GET` request to `/error`. The `status` and `body` properties of the response are compared to the expected values.

## Conclusion

Jest and Supertest are powerful tools that can be used to test TypeScript applications. In this article, we've seen how to set up and use Jest and Supertest with TypeScript. We've also seen how to write tests for common scenarios.