---
title: 035: Using Nest.js with React
description: 
published: true
date: 2023-02-02T00:18:34.181Z
tags: 
editor: markdown
dateCreated: 2023-02-02T00:18:29.884Z
---

- [035: Uso de Nest.js con React***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/035-using-nest-js-with-react)
{.links-list}
- [035: 将 Nest.js 与 React 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/035-using-nest-js-with-react)
{.links-list}
- [035: Nest.js를 React와 함께 사용하기***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/035-using-nest-js-with-react)
{.links-list}


# Introduction

Nest.js is a Node.js framework for building scalable server-side applications. It uses TypeScript, a superset of JavaScript, and combines elements of both functional and object-oriented programming.

React is a JavaScript library for building user interfaces. It is declarative, efficient, and flexible.

In this post, we will see how to use Nest.js with React.

# Setting up the project

We will be using the create-react-app CLI to generate a React project.

```
npx create-react-app nestjs-react-app
```

This will create a directory called `nestjs-react-app` with the following structure:

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

We will be using TypeScript for both the React and Nest.js parts of the project.

First, we need to install the TypeScript compiler and the type definitions for React and React-DOM:

```
npm install --save-dev typescript @types/react @types/react-dom
```

Next, we need to modify the `tsconfig.json` file to include the React and React-DOM definitions:

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

We also need to modify the `jsconfig.json` file to include the React and React-DOM definitions:

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

Now that we have TypeScript set up, we can install Nest.js using the following command:

```
npm install --save @nestjs/core @nestjs/common rxjs reflect-metadata
```

# Creating the Nest.js server

We will start by creating a file called `server.ts` in the `src` directory. This file will contain the code for our Nest.js server.

```
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

In the `server.ts` file, we first import the `NestFactory` and `AppModule` from `@nestjs/core`.

The `NestFactory` is used to create a Nest.js application instance. The `AppModule` is a module that contains the code for our application.

We then define an `async` function called `bootstrap` which will be used to start our Nest.js server.

Inside the `bootstrap` function, we create an instance of our `AppModule` using the `NestFactory` and then we call the `listen` method to start the server.

# Creating the React frontend

We will start by creating a file called `App.tsx` in the `src` directory. This file will contain the code for our React frontend.

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

In the `App.tsx` file, we first import React and the `App.css` file.

We then define a function called `App` which returns a `div` element. Inside the `div` element, we have a `h1` element which contains the text "Hello, world!".

Finally, we export the `App` function so that it can be used in other parts of the program.

# Connecting React and Nest.js

We will start by modifying the `server.ts` file to include the following code:

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

In the `server.ts` file, we first import the `NestFactory`, `AppModule`, and `NestExpressApplication` from `@nestjs/core`.

We also import the `join` function from the `path` module.

The `NestFactory` is used to create a Nest.js application instance. The `AppModule` is a module that contains the code for our application. The `NestExpressApplication` is used to configure the Express server.

We then define an `async` function called `bootstrap` which will be used to start our Nest.js server.

Inside the `bootstrap` function, we create an instance of our `AppModule` using the `NestFactory` and then we call the `useStaticAssets` and `setBaseViewsDir` methods to configure the Express server.

Finally, we call the `listen` method to start the server.

# Rendering React in Nest.js

We will start by modifying the `server.ts` file to include the following code:

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

In the `server.ts` file, we first import the `NestFactory`, `AppModule`, `NestExpressApplication`, `join` function, and `renderFile` function from the `pug` module.

The `NestFactory` is used to create a Nest.js application instance. The `AppModule` is a module that contains the code for our application. The `NestExpressApplication` is used to configure the Express server.

We then define an `async` function called `bootstrap` which will be used to start our Nest.js server.

Inside the `bootstrap` function, we create an instance of our `AppModule` using the `NestFactory` and then we call the `useStaticAssets`, `setBaseViewsDir`, and `setViewEngine` methods to configure the Express server.

Next, we define a route handler for the `/` path which renders a `index.pug` template.

Finally, we call the `listen` method to start the server.

# Passing data from Nest.js to React

We will start by modifying the `server.ts` file to include the following code:

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

In the `server.ts` file, we first import the `NestFactory`, `AppModule`, `NestExpressApplication`, `join` function, and `renderFile` function from the `pug` module.

The `NestFactory` is used to create a Nest.js application instance. The `AppModule` is a module that contains the code for our application. The `NestExpressApplication` is used to configure the Express server.

We then define an `async` function called `bootstrap` which will be used to start our Nest.js server.

Inside the `bootstrap` function, we create an instance of our `AppModule` using the `NestFactory` and then we call the `useStaticAssets`, `setBaseViewsDir`, and `setViewEngine` methods to configure the Express server.

Next, we define a route handler for the `/` path which renders a `index.pug` template.

Finally, we call the `listen` method to start the server.

# Passing data from React to Nest.js

We will start by modifying the `App.tsx` file to include the following code:

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

In the `App.tsx` file, we first import React and the `App.css` file.

We then define a function called `App` which returns a `div` element. Inside the `div` element, we have a `h1` element which contains the text "Hello, world!".

We also have a `button` element which, when clicked, will change the text in the `h1` element to "Nest.js is awesome!".

Finally, we export the `App` function so that it can be used in other parts of the program.

# Conclusion

In this post, we saw how to use Nest.js with React.

We started by setting up the project and then we created the Nest.js server.

Next, we created the React frontend and connected React and Nest.js.

Finally, we saw how to pass data from Nest.js to React and from React to Nest.js.