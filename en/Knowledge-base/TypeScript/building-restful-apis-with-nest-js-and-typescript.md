---
title: Building RESTful APIs with Nest.js and TypeScript
description: 
published: true
date: 2023-02-15T14:55:46.802Z
tags: 
editor: markdown
dateCreated: 2023-02-15T14:55:39.212Z
---

- [Creación de API RESTful con Nest.js y TypeScript***Spanish** document is available*](/es/Knowledge-base/TypeScript/building-restful-apis-with-nest-js-and-typescript)
{.links-list}
- [使用 Nest.js 和 TypeScript 构建 RESTful API***Chinese Simplified** document is available*](/zh/Knowledge-base/TypeScript/building-restful-apis-with-nest-js-and-typescript)
{.links-list}
- [Nest.js 및 TypeScript로 RESTful API 구축***Korean** document is available*](/ko/Knowledge-base/TypeScript/building-restful-apis-with-nest-js-and-typescript)
{.links-list}


# Building RESTful APIs with Nest.js and TypeScript

Nest.js is a Node.js framework for building server-side applications. It uses TypeScript, a superset of JavaScript that adds static type checking and other features, and provides a good platform for building RESTful APIs.

In this article, we'll look at how to build a RESTful API using Nest.js and TypeScript. We'll start by looking at the project structure and then move on to creating the API endpoints. We'll also look at how to use TypeScript with Nest.js.

## Project Structure

The project structure for a Nest.js project is similar to that of a Node.js project. There is a src directory for the source code and a test directory for the tests. The src directory contains a main.ts file, which is the entry point for the application. The tests directory contains a main.spec.ts file, which is the entry point for the tests.

The project also has a tsconfig.json file, which is used to configure the TypeScript compiler. The file contains options for the compiler, such as the target JavaScript version and the module type.

The project also has a package.json file, which contains metadata for the project, such as the dependencies and scripts.

## Creating the API Endpoints

The first thing we need to do is create the API endpoints. We'll do this in the src/main.ts file.

We'll start by importing the express module and creating an Express application. We'll also import the body-parser module and the cors module.

```javascript
import * as express from 'express';
import * as bodyParser from 'body-parser';
import * as cors from 'cors';

const app = express();
```

Next, we'll configure the Express application. We'll set the port to 3000 and enable the body parser and the cors middleware.

```javascript
app.set('port', 3000);
app.use(bodyParser.json());
app.use(cors());
```

Now, we'll create the API endpoints. We'll start with a GET endpoint for retrieving a list of users.

```javascript
app.get('/users', (req, res) => {
  // ...
});
```

Next, we'll create a POST endpoint for creating a new user.

```javascript
app.post('/users', (req, res) => {
  // ...
});
```

Finally, we'll create a PUT endpoint for updating an existing user.

```javascript
app.put('/users/:id', (req, res) => {
  // ...
});
```

## Using TypeScript with Nest.js

Nest.js and TypeScript work well together. Nest.js provides decorators that make it easy to use TypeScript with Nest.js.

For example, the @Controller decorator can be used to create a controller. The @Get decorator can be used to create a GET endpoint. The @Post decorator can be used to create a POST endpoint.

```typescript
import { Controller, Get, Post, Put } from '@nestjs/common';

@Controller('/users')
export class UserController {

  @Get()
  getUsers() {
    // ...
  }

  @Post()
  createUser() {
    // ...
  }

  @Put(':id')
  updateUser() {
    // ...
  }

}
```