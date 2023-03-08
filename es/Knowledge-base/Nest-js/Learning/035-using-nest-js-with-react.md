---
title: 035: Uso de Nest.js con React
description: 
published: true
date: 2023-02-02T00:18:31.684Z
tags: 
editor: markdown
dateCreated: 2023-02-02T00:18:29.882Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [035: Using Nest.js with React***English** document is available*](/en/Knowledge-base/Nest-js/Learning/035-using-nest-js-with-react)
{.links-list}


# Introducción

Nest.js es un marco de Node.js para crear aplicaciones escalables del lado del servidor. Utiliza TypeScript, un superconjunto de JavaScript, y combina elementos de programación tanto funcional como orientada a objetos.

React es una biblioteca de JavaScript para crear interfaces de usuario. Es declarativo, eficiente y flexible.

En esta publicación, veremos cómo usar Nest.js con React.

# Configurando el proyecto

Usaremos la CLI create-react-app para generar un proyecto React.

```
npx create-react-app nestjs-react-app
```

Esto creará un directorio llamado `nestjs-react-app` con la siguiente estructura:

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

Usaremos TypeScript para las partes React y Nest.js del proyecto.

Primero, necesitamos instalar el compilador de TypeScript y las definiciones de tipo para React y React-DOM:

```
npm install --save-dev typescript @types/react @types/react-dom
```

A continuación, debemos modificar el archivo `tsconfig.json` para incluir las definiciones de React y React-DOM:

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

También necesitamos modificar el archivo `jsconfig.json` para incluir las definiciones de React y React-DOM:

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

Ahora que tenemos configurado TypeScript, podemos instalar Nest.js usando el siguiente comando:

```
npm install --save @nestjs/core @nestjs/common rxjs reflect-metadata
```

# Creando el servidor Nest.js

Comenzaremos creando un archivo llamado `server.ts` en el directorio `src`. Este archivo contendrá el código para nuestro servidor Nest.js.

```
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

En el archivo `server.ts`, primero importamos `NestFactory` y `AppModule` desde `@nestjs/core`.

La `NestFactory` se usa para crear una instancia de la aplicación Nest.js. El `AppModule` es un módulo que contiene el código de nuestra aplicación.

Luego definimos una función `async` llamada `bootstrap` que se usará para iniciar nuestro servidor Nest.js.

Dentro de la función `bootstrap`, creamos una instancia de nuestro `AppModule` usando `NestFactory` y luego llamamos al método `listen` para iniciar el servidor.

# Creando la interfaz React

Comenzaremos creando un archivo llamado `App.tsx` en el directorio `src`. Este archivo contendrá el código para nuestra interfaz React.

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

En el archivo `App.tsx`, primero importamos React y el archivo `App.css`.

Luego definimos una función llamada `App` que devuelve un elemento `div`. Dentro del elemento `div`, tenemos un elemento `h1` que contiene el texto "¡Hola, mundo!".

Finalmente, exportamos la función `App` para que pueda usarse en otras partes del programa.

# Conexión de React y Nest.js

Comenzaremos modificando el archivo `server.ts` para incluir el siguiente código:

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

En el archivo `server.ts`, primero importamos `NestFactory`, `AppModule` y `NestExpressApplication` desde `@nestjs/core`.

También importamos la función `join` desde el módulo `path`.

La `NestFactory` se usa para crear una instancia de la aplicación Nest.js. El `AppModule` es un módulo que contiene el código de nuestra aplicación. La `NestExpressApplication` se utiliza para configurar el servidor Express.

Luego definimos una función `async` llamada `bootstrap` que se usará para iniciar nuestro servidor Nest.js.

Dentro de la función `bootstrap`, creamos una instancia de nuestro `AppModule` usando `NestFactory` y luego llamamos a los métodos `useStaticAssets` y `setBaseViewsDir` para configurar el servidor Express.

Finalmente, llamamos al método `listen` para iniciar el servidor.

# Representación de React en Nest.js

Comenzaremos modificando el archivo `server.ts` para incluir el siguiente código:

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

En el archivo `server.ts`, primero importamos la función `NestFactory`, `AppModule`, `NestExpressApplication`, `join` y `renderFile` del módulo `pug`.

La `NestFactory` se usa para crear una instancia de la aplicación Nest.js. El `AppModule` es un módulo que contiene el código de nuestra aplicación. La `NestExpressApplication` se utiliza para configurar el servidor Express.

Luego definimos una función `async` llamada `bootstrap` que se usará para iniciar nuestro servidor Nest.js.

Dentro de la función `bootstrap`, creamos una instancia de nuestro `AppModule` usando `NestFactory` y luego llamamos a los métodos `useStaticAssets`, `setBaseViewsDir` y `setViewEngine` para configurar el servidor Express.

A continuación, definimos un controlador de ruta para la ruta `/` que representa una plantilla `index.pug`.

Finalmente, llamamos al método `listen` para iniciar el servidor.

# Pasar datos de Nest.js a React

Comenzaremos modificando el archivo `server.ts` para incluir el siguiente código:

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

En el archivo `server.ts`, primero importamos la función `NestFactory`, `AppModule`, `NestExpressApplication`, `join` y `renderFile` del módulo `pug`.

La `NestFactory` se usa para crear una instancia de la aplicación Nest.js. El `AppModule` es un módulo que contiene el código de nuestra aplicación. La `NestExpressApplication` se utiliza para configurar el servidor Express.

Luego definimos una función `async` llamada `bootstrap` que se usará para iniciar nuestro servidor Nest.js.

Dentro de la función `bootstrap`, creamos una instancia de nuestro `AppModule` usando `NestFactory` y luego llamamos a los métodos `useStaticAssets`, `setBaseViewsDir` y `setViewEngine` para configurar el servidor Express.

A continuación, definimos un controlador de ruta para la ruta `/` que representa una plantilla `index.pug`.

Finalmente, llamamos al método `listen` para iniciar el servidor.

# Pasar datos de React a Nest.js

Comenzaremos modificando el archivo `App.tsx` para incluir el siguiente código:

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

En el archivo `App.tsx`, primero importamos React y el archivo `App.css`.

Luego definimos una función llamada `App` que devuelve un elemento `div`. Dentro del elemento `div`, tenemos un elemento `h1` que contiene el texto "¡Hola, mundo!".

También tenemos un elemento `button` que, al hacer clic en él, cambiará el texto del elemento `h1` a "¡Nest.js es increíble!".

Finalmente, exportamos la función `App` para que pueda usarse en otras partes del programa.

# Conclusión

En esta publicación, vimos cómo usar Nest.js con React.

Comenzamos configurando el proyecto y luego creamos el servidor Nest.js.

A continuación, creamos la interfaz de React y conectamos React y Nest.js.

Finalmente, vimos cómo pasar datos de Nest.js a React y de React a Nest.js.