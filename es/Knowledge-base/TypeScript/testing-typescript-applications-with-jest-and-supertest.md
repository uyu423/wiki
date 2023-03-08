---
title: Prueba de aplicaciones TypeScript con Jest y Supertest
description: 
published: true
date: 2023-02-13T03:55:34.491Z
tags: 
editor: markdown
dateCreated: 2023-02-13T03:55:32.805Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Testing TypeScript Applications with Jest and Supertest***English** document is available*](/en/Knowledge-base/TypeScript/testing-typescript-applications-with-jest-and-supertest)
{.links-list}


# Prueba de aplicaciones TypeScript con Jest y Supertest

TypeScript es un poderoso lenguaje de programación que permite a los desarrolladores crear aplicaciones web a gran escala. Si bien no se requiere TypeScript para usar Jest o Supertest, puede ser útil usar TypeScript junto con estas herramientas de prueba. Este artículo le mostrará cómo configurar y usar Jest y Supertest con TypeScript.

## Configuración de Jest y Supertest con TypeScript

Antes de que pueda comenzar a usar Jest y Supertest con TypeScript, debe configurar su proyecto. Primero, instala las dependencias:

```
npm install --save-dev jest @types/jest ts-jest supertest @types/supertest
```

A continuación, cree un archivo llamado `jest.config.js` en la raíz de su proyecto y agregue la siguiente configuración:

```js
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node',
};
```

Esto le dice a Jest que use el compilador TypeScript y ejecute pruebas en un entorno Node.js.

Finalmente, cree un archivo llamado `tests.ts` en la raíz de su proyecto y agregue el siguiente código:

```ts
import supertest from 'supertest';

const request = supertest('http://localhost:3000');

test('GET /', async () => {
  const response = await request.get('/');
  expect(response.status).toEqual(200);
});
```

Este código importa la biblioteca `supertest` y crea un nuevo objeto `request` que se utilizará para realizar solicitudes HTTP al servidor. La función `test` se utiliza para definir un caso de prueba. En este caso, el caso de prueba realiza una solicitud `GET` a `/` y verifica que el código de estado de respuesta sea `200`.

## Ejecutando pruebas

Para ejecutar las pruebas, puedes usar el comando `jest`:

```
jest
```

Esto ejecutará todas las pruebas en su proyecto. También puede ejecutar una prueba específica pasando el nombre de `prueba` como argumento:

```
jest testName
```

## Pruebas de escritura

Hay muchas formas diferentes de escribir pruebas con Jest y Supertest. En esta sección, veremos algunos escenarios comunes.

### Prueba de métodos HTTP

Jest y Supertest se pueden usar para probar todos los métodos HTTP: `GET`, `POST`, `PUT`, `DELETE`, etc. Por ejemplo, el siguiente caso de prueba prueba una solicitud `POST`:

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

Este caso de prueba realiza una solicitud `POST` a `/users` con un cuerpo JSON. El método `send` se utiliza para establecer el cuerpo de la solicitud. Las propiedades `status` y `body` de la respuesta se comparan con los valores esperados.

### Prueba de software intermedio

Jest y Supertest también se pueden usar para probar middleware. Por ejemplo, el siguiente caso de prueba prueba una función de middleware que se utiliza para autenticar a los usuarios:

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

Este caso de prueba realiza una solicitud `POST` a `/auth` con un cuerpo JSON. El método `send` se utiliza para establecer el cuerpo de la solicitud. Las propiedades `status` y `body` de la respuesta se comparan con los valores esperados.

### Probando el manejo de errores

Jest y Supertest también se pueden usar para probar el manejo de errores. Por ejemplo, el siguiente caso de prueba prueba una función de middleware que se usa para manejar errores:

```ts
test('GET /error', async () => {
  const response = await request.get('/error');
  expect(response.status).toEqual(500);
  expect(response.body).toEqual({
    error: 'Internal server error',
  });
});
```

Este caso de prueba realiza una solicitud `GET` a `/error`. Las propiedades `status` y `body` de la respuesta se comparan con los valores esperados.

## Conclusión

Jest y Supertest son herramientas poderosas que se pueden usar para probar aplicaciones de TypeScript. En este artículo, hemos visto cómo configurar y usar Jest y Supertest con TypeScript. También hemos visto cómo escribir pruebas para escenarios comunes.