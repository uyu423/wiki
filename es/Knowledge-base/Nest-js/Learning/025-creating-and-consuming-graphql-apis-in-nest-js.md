---
title: 025: Creación y consumo de API de GraphQL en Nest.js
description: 
published: true
date: 2023-02-15T05:32:27.474Z
tags: 
editor: markdown
dateCreated: 2023-02-15T05:32:25.792Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [025: Creating and consuming GraphQL APIs in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/025-creating-and-consuming-graphql-apis-in-nest-js)
{.links-list}


## Introducción

GraphQL es un lenguaje de consulta para API desarrollado por Facebook. Le permite solicitar datos específicos de una API y, a menudo, se usa con React. Nest.js es un marco para Node.js que facilita la creación de API de GraphQL. En esta publicación, aprenderemos cómo crear y consumir API de GraphQL en Nest.js.

## Crear una API de GraphQL en Nest.js

Crear una API de GraphQL en Nest.js es fácil. Primero, necesitamos instalar las siguientes dependencias:

```
npm install --save @nestjs/graphql graphql-tools graphql
```

Luego, podemos crear un archivo llamado `graphql.module.ts` en el directorio `src` y agregar el siguiente código:

```typescript
import { Module } from '@nestjs/common';
import { GraphQLModule } from '@nestjs/graphql';
import { join } from 'path';

@Module({
  imports: [
    GraphQLModule.forRoot({
      typePaths: ['./**/*.graphql'],
      definitions: {
        path: join(process.cwd(), 'src/graphql.ts'),
      },
    }),
  ],
})
export class GraphQLModule {}
```

En el código anterior, importamos el `GraphQLModule` de `@nestjs/graphql`. También estamos especificando la ruta a nuestros archivos de esquema de GraphQL y la ruta a nuestro archivo de definiciones generado.

A continuación, debemos crear un archivo llamado `graphql.ts` en el directorio `src` y agregar el siguiente código:

```typescript
import { gql } from '@nestjs/graphql';

export const typeDefs = gql`
  type Query {
    hello: String
  }
`;
```

En el código anterior, estamos importando la función `gql` desde `@nestjs/graphql`. Esta función nos permite escribir consultas GraphQL en una cadena. También estamos definiendo un tipo GraphQL llamado `Query` con un campo llamado `hello`.

Finalmente, necesitamos crear un archivo llamado `resolvers.ts` en el directorio `src` y agregar el siguiente código:

```typescript
import { Query, Resolver } from '@nestjs/graphql';

@Resolver('Query')
export class QueryResolver {
  @Query()
  hello() {
    return 'Hello, world!';
  }
}
```

En el código anterior, estamos importando los decoradores `Query` y `Resolver` desde `@nestjs/graphql`. También estamos creando una clase llamada `QueryResolver` que está decorada con el decorador `@Resolver`. Esta clase contiene un método llamado `hola` que está decorado con el decorador `@Query`. Este método devuelve la cadena `'¡Hola, mundo!'`.

Ahora que hemos creado nuestra API GraphQL, aprendamos cómo consumirla.

## Consumir una API de GraphQL en Nest.js

Hay dos formas de consumir una API GraphQL en Nest.js: usando un cliente REST o usando un cliente GraphQL.

### Uso de un cliente REST

Podemos usar un cliente REST como Postman para consumir nuestra API GraphQL. Primero, necesitamos iniciar nuestro servidor Nest.js:

```
nest start
```

Luego, podemos abrir Postman y realizar una solicitud POST a `http://localhost:3000/graphql`. En el cuerpo de la solicitud, debemos especificar lo siguiente:

```
{
  "query": "query { hello }"
}
```

El campo `query` contiene nuestra consulta GraphQL. En este caso, estamos consultando el campo `hola` en el tipo `Consulta`.

Cuando enviemos la solicitud, deberíamos ver la siguiente respuesta:

```
{
  "data": {
    "hello": "Hello, world!"
  }
}
```

### Uso de un cliente GraphQL

También podemos usar un cliente GraphQL como Apollo Client para consumir nuestra API GraphQL. Primero, necesitamos instalar las siguientes dependencias:

```
npm install --save apollo-client apollo-link-http apollo-cache-inmemory
```

Luego, podemos crear un archivo llamado `app.js` en el directorio `src` y agregar el siguiente código:

```javascript
import { ApolloClient } from 'apollo-client';
import { HttpLink } from 'apollo-link-http';
import { InMemoryCache } from 'apollo-cache-inmemory';

const client = new ApolloClient({
  link: new HttpLink({
    uri: 'http://localhost:3000/graphql',
  }),
  cache: new InMemoryCache(),
});

client
  .query({
    query: `
      query {
        hello
      }
    `,
  })
  .then((result) => console.log(result));
```

En el código anterior, estamos importando `ApolloClient`, `HttpLink` e `InMemoryCache` desde `apollo-client`. También estamos creando una instancia de `ApolloClient` con un `HttpLink` y un `InMemoryCache`. Luego hacemos una consulta al campo `hola` en el tipo `Query` y registramos el resultado en la consola.

Cuando ejecutamos el código anterior, deberíamos ver el siguiente resultado:

```
{
  data: {
    hello: 'Hello, world!'
  }
}
```

## Conclusión

En esta publicación, aprendimos cómo crear y consumir API de GraphQL en Nest.js. También aprendimos a usar un cliente REST y un cliente GraphQL para consumir nuestra API GraphQL.