---
title: Uso de TypeScript y GraphQL en una aplicación Next.js
description: 
published: true
date: 2023-02-01T19:57:48.419Z
tags: 
editor: markdown
dateCreated: 2023-02-01T19:57:48.419Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Using TypeScript and GraphQL in a Next.js App***English** document is available*](/en/Knowledge-base/TypeScript/using-typescript-and-graphql-in-a-next-js-app)
{.links-list}

  
# Uso de TypeScript y GraphQL en una aplicación Next.js

TypeScript es un superconjunto escrito de JavaScript que se compila para limpiar la salida de JavaScript. GraphQL es un lenguaje de consulta para API y un tiempo de ejecución para cumplir con esas consultas con sus datos existentes.

En este artículo, mostraremos cómo usar TypeScript y GraphQL en una aplicación Next.js. Usaremos las siguientes bibliotecas:

- [Mecanografiado](https://www.typescriptlang.org/)
- [GraphQL](https://graphql.org/)
- [Apolo GraphQL](https://www.apollographql.com/)

## ¿Qué es Next.js?

Next.js es un marco React que facilita la creación de aplicaciones React escalables y de alto rendimiento. Next.js proporciona características como la representación del lado del servidor, la generación de sitios estáticos y la obtención de datos que se pueden usar para crear aplicaciones React complejas.

Next.js tiene opiniones sobre cómo estructura su aplicación React y aplica un conjunto de convenciones que lo ayudan a escribir código bien organizado. Next.js también se basa en webpack, por lo que se beneficia de todas las funciones que ofrece webpack.

## Configuración de un proyecto Next.js

Para crear un nuevo proyecto Next.js, podemos usar la herramienta CLI [create-next-app](https://github.com/zeit/next.js/tree/canary/packages/create-next-app).

```bash
npx crear-siguiente-aplicación mi-aplicación
```

Esto creará un nuevo directorio llamado `my-app` con el andamiaje básico para una aplicación Next.js.

Next.js viene con [compatibilidad con TypeScript](https://nextjs.org/blog/next-9# built-in-typescript-support) lista para usar, por lo que no necesitamos instalar ninguna dependencia adicional.

## Agregando mecanografiado

Comencemos agregando TypeScript a nuestro proyecto. Podemos hacer esto creando un archivo `tsconfig.json` en la raíz de nuestro proyecto:

```json
{
  "Opciones del compilador": {
    "objetivo": "siguiente",
    "módulo": "siguiente",
    "jsx": "preservar",
    "estricto": cierto,
    "noImplicitAny": falso,
    "módulos aislados": cierto,
    "esModuleInterop": verdadero,
    "permitirJs": falso,
    "preservarConstEnums": verdadero,
    "suppressImplicitAnyIndexErrors": verdadero
  }
}
```

Esta es una configuración básica de TypeScript que nos permitirá usar TypeScript en toda nuestra aplicación.

A continuación, debemos actualizar nuestro archivo `package.json` para usar el compilador de TypeScript:

```json
{
  "guiones": {
    "dev": "siguiente",
    "construir": "siguiente compilación",
    "inicio": "próximo inicio",
    "prueba": "echo \"Error: no se especificó ninguna prueba\" && exit 1",
    "comprobación de tipo": "tsc"
  },
  ...
}
```

Hemos agregado un nuevo script llamado `type-check` que compilará nuestro código TypeScript. Podemos ejecutar este script con el siguiente comando:

```bash
npm ejecutar verificación de tipo
```

## Agregando GraphQL

Ahora que hemos configurado TypeScript, podemos agregar GraphQL a nuestro proyecto. Usaremos la biblioteca [Apollo GraphQL](https://www.apollographql.com/) para agregar compatibilidad con GraphQL a nuestra aplicación.

Primero, necesitamos instalar las dependencias de Apollo GraphQL:

```bash
npm install @apollo/react-hooks apollo-boost graphql graphql-tag prop-types
```

A continuación, debemos crear un nuevo archivo llamado `apollo.js` en el directorio `/lib`. Este archivo se utilizará para configurar el cliente Apollo GraphQL.

```js
importar { ApolloClient } desde 'apollo-boost';

exportar const cliente = nuevo ApolloClient({
  uri: 'https://my-graphql-endpoint.com/graphql',
});
```

En este archivo, estamos creando un nuevo cliente Apollo y configurándolo con el URI de nuestro punto final GraphQL.

Ahora que tenemos nuestro cliente Apollo configurado, podemos comenzar a usar GraphQL en nuestra aplicación.

## Consultando datos con GraphQL

Para consultar datos con GraphQL, primero debemos crear una consulta GraphQL. Las consultas de GraphQL generalmente se escriben en un archivo con una extensión `.graphql`.

Vamos a crear un nuevo archivo llamado `getPosts.graphql` en el directorio `/queries`:

```graphql
consulta GetPosts {
  publicaciones {
    identificación
    título
    cuerpo
  }
}
```

Esta consulta obtendrá una lista de publicaciones de nuestro punto final de GraphQL.

Ahora que tenemos nuestra consulta, podemos usar el gancho React [useQuery](https://www.apollographql.com/docs/react/api/react-hooks/# usequery) para ejecutarla.

Vamos a crear un nuevo archivo llamado `Posts.js` en el directorio `/pages`:

```js
importar { useQuery } desde '@apollo/react-hooks';
importar gql desde 'graphql-tag';

constante GET_POSTS = gql`
  consulta GetPosts {
    publicaciones {
      identificación
      título
      cuerpo
    }
  }
`;

función Publicaciones () {
  const { datos, cargando, error } = useQuery(GET_POSTS);

  si (cargando) {
    volver <div>Cargando...</div>;
  }

  si (error) {
    volver <div>¡Error!</div>;
  }

  retorno (
    <ul>
      {datos.publicaciones.mapa(publicación => (
        <li clave={post.id}>
          <h2>{publicación.título}</h2>
          <p>{publicación.cuerpo}</p>
        </li>
      ))}
    </ul>
  );
}

exportar publicaciones predeterminadas;
```

En este archivo, primero importamos el gancho `useQuery` y la etiqueta `gql` de la biblioteca Apollo GraphQL. También estamos importando nuestra consulta `GET_POSTS`.

A continuación, estamos usando el gancho `useQuery` para ejecutar nuestra consulta. El hook `useQuery` devuelve un objeto con propiedades `data`, `loading` y `error`.

Si la consulta aún se está cargando, mostraremos un indicador de carga. Si hay un error, mostraremos un mensaje de error. De lo contrario, mostraremos una lista de publicaciones.

## Agregando mecanografiado

Podemos agregar TypeScript a nuestras consultas de GraphQL creando un archivo `.d.ts` para cada consulta.

Vamos a crear un nuevo archivo llamado `getPosts.d.ts` en el directorio `/queries`:

```mecanografiado
importar { Publicación } desde '../tipos/publicación';

interfaz de exportación GetPostsData {
  publicaciones: publicación[];
}
```

Este archivo define la forma de los datos que esperamos recibir de nuestra consulta `getPosts`.

Ahora podemos actualizar nuestro archivo `Posts.js` para usar las definiciones de TypeScript que creamos:

```js
importar { useQuery } desde '@apollo/react-hooks';
importar gql desde 'graphql-tag';
importar { GetPostsData } de '../consultas/getPosts';

constante GET_POSTS = gql`
  consulta GetPosts {
    publicaciones {
      identificación
      título
      cuerpo
    }
  }
`;

función Mensajes () {
  const { datos, cargando, error } = useQuery<GetPostsData>(GET_POSTS);

  si (cargando) {
    volver <div>Cargando...</div>;
  }

  si (error) {
    volver <div>¡Error!</div>;
  }

  retorno (
    <ul>
      {datos.publicaciones.mapa(publicación => (
        <li clave={post.id}>
          <h2>{publicación.título}</h2>
          <p>{publicación.cuerpo}</p>
        </li>
      ))}
    </ul>
  );
}

exportar publicaciones predeterminadas;
```

En este archivo, hemos importado la interfaz `GetPostsData` desde nuestro archivo `getPosts.d.ts`. También hemos actualizado el enlace `useQuery` para escribir la propiedad `data` como `GetPostsData`.

## Mecanografiado y GraphQL

TypeScript y GraphQL son dos tecnologías que se pueden usar juntas para crear aplicaciones escalables y de alto rendimiento. En este artículo, mostramos cómo usar TypeScript y GraphQL en una aplicación Next.js.