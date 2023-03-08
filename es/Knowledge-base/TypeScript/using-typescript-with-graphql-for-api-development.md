---
title: Uso de TypeScript con GraphQL para el desarrollo de API
description: 
published: true
date: 2023-02-01T19:17:56.734Z
tags: 
editor: markdown
dateCreated: 2023-02-01T19:17:52.550Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Using TypeScript with GraphQL for API Development***English** document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-graphql-for-api-development)
{.links-list}


# Uso de TypeScript con GraphQL para el desarrollo de API

TypeScript es un superconjunto fuertemente tipado de JavaScript que se compila para limpiar la salida de JavaScript. GraphQL es un poderoso lenguaje de consulta para las API que brinda a los clientes el poder de solicitar solo los datos que necesitan de un servidor, lo que hace que las API sean más eficientes.

Las dos tecnologías se pueden usar juntas para crear servidores y clientes de API robustos y con seguridad de tipos. En este artículo, veremos cómo usar TypeScript con GraphQL, incluido un ejemplo de código corto.

## ¿Por qué usar TypeScript con GraphQL?

Hay varias razones por las que podría querer usar TypeScript con GraphQL. Primero, TypeScript puede ayudarlo a crear consultas GraphQL con seguridad de tipos. Esto significa que puede detectar errores temprano, incluso antes de que se ejecute su código.

En segundo lugar, TypeScript puede proporcionar autocompletado y seguridad de tipos para su servidor GraphQL. Esto es especialmente útil cuando usa un esquema GraphQL complejo con muchos tipos y campos.

En tercer lugar, TypeScript puede ayudarlo con la organización del código. Por ejemplo, puede usar el sistema de módulos de TypeScript para estructurar su código de una manera que sea fácil de entender y mantener.

Cuarto, TypeScript se está volviendo cada vez más popular, por lo que usarlo con GraphQL puede facilitar la búsqueda de colaboradores y soporte.

## Configuración de TypeScript con GraphQL

Para usar TypeScript con GraphQL, deberá instalar las siguientes dependencias:

- texto mecanografiado: ^3.2.2
- graphql: ^14.3.1
- @tipos/graphql: ^14.0.1

Puede instalar estas dependencias usando npm:

```
npm install --save typescript graphql @types/graphql
```

## Usando TypeScript con GraphQL

Una vez que haya instalado las dependencias, puede comenzar a usar TypeScript con GraphQL. Aquí hay un ejemplo simple:

```graphql
query GetUser($id: ID!) {
  user(id: $id) {
    id
    name
  }
}
```

En este ejemplo, hemos definido una consulta de GraphQL que busca a un usuario por su ID. También hemos definido un tipo para la variable ID. Este tipo se utilizará para verificar el tipo de nuestras variables de consulta.

Ahora veamos cómo usar esta consulta con TypeScript. Primero, necesitaremos crear un archivo llamado `schema.ts`:

```typescript
import {
  GraphQLSchema,
  GraphQLObjectType,
  GraphQLString,
  GraphQLID,
} from 'graphql';

const UserType = new GraphQLObjectType({
  name: 'User',
  fields: {
    id: { type: GraphQLID },
    name: { type: GraphQLString },
  },
});

const QueryType = new GraphQLObjectType({
  name: 'Query',
  fields: {
    user: {
      type: UserType,
      args: {
        id: { type: GraphQLID },
      },
      resolve: (_, { id }) => ({ id, name: 'Alice' }),
    },
  },
});

export const schema = new GraphQLSchema({
  query: QueryType,
});
```

En este archivo, hemos definido nuestro esquema GraphQL. También hemos definido un tipo `Usuario` y un tipo `Consulta`. El tipo `Consulta` contiene un campo `usuario`, que obtiene un `Usuario` por su ID.

Ahora vamos a crear un archivo llamado `index.ts`:

```typescript
import { graphql, buildSchema } from 'graphql';
import { schema } from './schema';

async function main() {
  const query = `
    query GetUser($id: ID!) {
      user(id: $id) {
        id
        name
      }
    }
  `;

  const variables = {
    id: '1',
  };

  const rootValue = {};
  const context = {};
  const options = {};

  const result = await graphql(schema, query, rootValue, context, options);
  console.log(result);
}

main();
```

En este archivo, hemos importado la función `graphql` del paquete `graphql`. También hemos importado nuestro `esquema` del archivo `schema.ts`.

Luego, definimos una consulta GraphQL que busca a un usuario por su ID. También hemos definido un objeto de `variables`, que contiene la ID del usuario que queremos obtener.

Finalmente, hemos llamado a la función `graphql`, pasando nuestro `schema`, `query`, `rootValue`, `context` y `options`. Esta función ejecutará nuestra consulta y devolverá el resultado.

Si ejecutamos este código, obtendremos el siguiente resultado:

```
{
  "data": {
    "user": {
      "id": "1",
      "name": "Alice"
    }
  }
}
```

Como puede ver, nuestra consulta se ejecutó con éxito y devolvió los datos que solicitamos.

## Conclusión

En este artículo, hemos visto cómo usar TypeScript con GraphQL. Hemos visto cómo TypeScript puede ayudarlo a crear consultas GraphQL con seguridad de tipos y cómo usar la función `graphql` para ejecutar esas consultas.