---
title: 使用 Jest 和 Supertest 测试 TypeScript 应用程序
description: 
published: true
date: 2023-02-13T03:55:34.400Z
tags: 
editor: markdown
dateCreated: 2023-02-13T03:55:32.802Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Testing TypeScript Applications with Jest and Supertest***English** document is available*](/en/Knowledge-base/TypeScript/testing-typescript-applications-with-jest-and-supertest)
{.links-list}


# 使用 Jest 和 Supertest 测试 TypeScript 应用程序

TypeScript 是一种功能强大的编程语言，使开发人员能够构建大型 Web 应用程序。虽然 TypeScript 不是使用 Jest 或 Supertest 所必需的，但将 TypeScript 与这些测试工具结合使用会很有帮助。本文将向您展示如何通过 TypeScript 设置和使用 Jest 和 Supertest。

## 使用 TypeScript 设置 Jest 和 Supertest

在开始将 Jest 和 Supertest 与 TypeScript 结合使用之前，您需要设置项目。首先，安装依赖项：

```
npm install --save-dev jest @types/jest ts-jest supertest @types/supertest
```

接下来，在项目的根目录中创建一个名为 jest.config.js 的文件并添加以下配置：

```js
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node',
};
```

这告诉 Jest 使用 TypeScript 编译器并在 Node.js 环境中运行测试。

最后，在项目的根目录中创建一个名为“tests.ts”的文件并添加以下代码：

```ts
import supertest from 'supertest';

const request = supertest('http://localhost:3000');

test('GET /', async () => {
  const response = await request.get('/');
  expect(response.status).toEqual(200);
});
```

此代码导入 `supertest` 库并创建一个新的 `request` 对象，该对象将用于向服务器发出 HTTP 请求。 `test` 函数用于定义测试用例。在这种情况下，测试用例向 `/` 发出 `GET` 请求并检查响应状态代码是否为 `200`。

## 运行测试

要运行测试，您可以使用 `jest` 命令：

```
jest
```

这将运行您项目中的所有测试。您还可以通过将“test”名称作为参数传递来运行特定测试：

```
jest testName
```

## 编写测试

使用 Jest 和 Supertest 编写测试有许多不同的方法。在本节中，我们将了解一些常见的场景。

### 测试 HTTP 方法

Jest 和 Supertest 可用于测试所有 HTTP 方法：`GET`、`POST`、`PUT`、`DELETE` 等。例如，以下测试用例测试 `POST` 请求：

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

此测试用例使用 JSON 主体向“/users”发出“POST”请求。 `send` 方法用于设置请求正文。将响应的“status”和“body”属性与预期值进行比较。

### 测试中间件

Jest 和 Supertest 也可以用来测试中间件。例如，以下测试用例测试用于对用户进行身份验证的中间件功能：

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

此测试用例使用 JSON 主体向 `/auth` 发出 `POST` 请求。 `send` 方法用于设置请求正文。将响应的“status”和“body”属性与预期值进行比较。

### 测试错误处理

Jest 和 Supertest 也可以用来测试错误处理。例如，以下测试用例测试用于处理错误的中间件函数：

```ts
test('GET /error', async () => {
  const response = await request.get('/error');
  expect(response.status).toEqual(500);
  expect(response.body).toEqual({
    error: 'Internal server error',
  });
});
```

此测试用例向 `/error` 发出 `GET` 请求。将响应的“status”和“body”属性与预期值进行比较。

## 结论

Jest 和 Supertest 是可用于测试 TypeScript 应用程序的强大工具。在本文中，我们了解了如何通过 TypeScript 设置和使用 Jest 和 Supertest。我们还了解了如何为常见场景编写测试。