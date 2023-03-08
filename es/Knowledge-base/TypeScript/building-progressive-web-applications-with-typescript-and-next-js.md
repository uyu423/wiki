---
title: Creación de aplicaciones web progresivas con TypeScript y Next.js
description: 
published: true
date: 2023-02-02T02:43:47.124Z
tags: 
editor: markdown
dateCreated: 2023-02-02T02:43:45.413Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Building Progressive Web Applications with TypeScript and Next.js***English** document is available*](/en/Knowledge-base/TypeScript/building-progressive-web-applications-with-typescript-and-next-js)
{.links-list}


TypeScript es un superconjunto escrito de JavaScript que se compila en JavaScript simple. Ofrece clases, módulos e interfaces para ayudarlo a crear componentes sólidos.

Next.js es un marco de React que facilita la creación de aplicaciones renderizadas por servidor listas para producción. Incluye funciones como la división automática de código, el servicio de archivos estáticos, el manejo de rutas y el renderizado universal.

En este artículo, aprenderemos a crear aplicaciones web progresivas (PWA) con TypeScript y Next.js. Comenzaremos creando un PWA simple que cargue un componente List desde un archivo JSON. Luego, agregaremos TypeScript a nuestro proyecto y usaremos los tipos de React para verificar el tipo de nuestros componentes. Finalmente, aprenderemos a usar las funciones de Next.js, como la división de código y la obtención previa de rutas, para mejorar el rendimiento de nuestra PWA.

## Creando un PWA simple con TypeScript y Next.js

Comenzaremos creando una aplicación Next.js simple que cargue un componente List desde un archivo JSON. El componente List se renderizará en el servidor e incluirá la división de código y la captación previa de rutas.

Primero, creemos un nuevo proyecto Next.js:

```
npx create-next-app my-app
```

A continuación, necesitamos instalar las siguientes dependencias:

```
npm install --save react react-dom next
```

Ahora, podemos crear nuestro componente Lista. Cree un nuevo archivo llamado `List.js` y agregue el siguiente código:

```js
import React from 'react';

const List = ({ items }) => (
  <ul>
    {items.map(item => (
      <li key={item.id}>{item.text}</li>
    ))}
  </ul>
);

export default List;
```

Este componente tomará un apoyo `elementos` y generará una lista de elementos. Cada elemento tendrá una clave y un texto.

A continuación, debemos crear un archivo JSON que contenga los elementos de nuestra lista. Cree un nuevo archivo llamado `listItems.json` y agregue el siguiente código:

```json
[
  { "id": 1, "text": "Item 1" },
  { "id": 2, "text": "Item 2" },
  { "id": 3, "text": "Item 3" }
]
```

Ahora, podemos importar este archivo JSON en nuestro componente `List.js`:

```js
import listItems from './listItems.json';
```

Finalmente, debemos decirle a Next.js que represente nuestro componente List en el servidor. Abra el archivo `pages/index.js` y reemplace el contenido con el siguiente código:

```js
import React from 'react';
import List from '../components/List';

const IndexPage = () => <List items={listItems} />;

export default IndexPage;
```

Esto renderizará nuestro componente List en el servidor y pasará los datos JSON `listItems` al componente como accesorio.

Ahora, si ejecutamos nuestra aplicación, deberíamos ver nuestro componente de lista representado en la página:

```
npm run dev
```

## Agregando TypeScript a nuestro proyecto

A continuación, agregaremos TypeScript a nuestro proyecto y usaremos los tipos de React para verificar el tipo de nuestros componentes.

Primero, necesitamos instalar el compilador de TypeScript:

```
npm install --save-dev typescript
```

Luego, necesitamos crear un archivo `tsconfig.json` en la raíz de nuestro proyecto. Este archivo contendrá nuestra configuración de TypeScript. Agregue el siguiente código al archivo `tsconfig.json`:

```json
{
  "compilerOptions": {
    "jsx": "react",
    "target": "esnext",
    "module": "commonjs",
    "strict": true
  },
  "include": ["src"]
}
```

Esta configuración le indicará al compilador de TypeScript que apunte al último estándar de JavaScript (ESNext) y que trate nuestro código como si fueran módulos de CommonJS.

A continuación, necesitamos instalar los tipos de React:

```
npm install --save-dev @types/react @types/react-dom
```

Ahora, podemos cambiar el nombre de nuestro componente `List.js` a `List.tsx` y comenzar a usar TypeScript. Primero, agregaremos tipos a nuestros accesorios:

```tsx
import React from 'react';

interface ListProps {
  items: {
    id: number;
    text: string;
  }[];
}

const List: React.FC<ListProps> = ({ items }) => (
  <ul>
    {items.map(item => (
      <li key={item.id}>{item.text}</li>
    ))}
  </ul>
);

export default List;
```

Hemos declarado una interfaz para nuestros accesorios llamada `ListProps`. Esta interfaz define la forma de nuestros accesorios. También hemos agregado tipos a nuestro componente usando el genérico `React.FC`. Este genérico nos permite especificar el tipo de nuestros props.

Ahora, si tratamos de pasar una propiedad inválida a nuestro componente, obtendremos un error de tipo:

```tsx
// TypeError: Type '{ items: number[]; }' is not assignable to type 'IntrinsicAttributes & ListProps'.
//   Property 'items' does not exist on type 'IntrinsicAttributes & ListProps'.ts(2322)
<List items={[1, 2, 3]} />
```

## Uso de las funciones de Next.js para mejorar el rendimiento

Finalmente, aprenderemos a usar las funciones de Next.js, como la división de código y la obtención previa de rutas, para mejorar el rendimiento de nuestra PWA.

### División de código

Next.js incluye una función llamada división de código que nos permite dividir nuestro código en varios paquetes. De esta manera, el navegador puede descargar y ejecutar solo el código que se requiere para la página actual.

Para usar la división de código en nuestro componente List, necesitamos usar el componente `React.lazy`. Este componente nos permite cargar componentes dinámicamente en tiempo de ejecución.

Primero, importemos el componente `React.lazy`:

```tsx
import React, { lazy } from 'react';
```

Luego, podemos usar el componente `lazy` para cargar dinámicamente nuestro componente Lista:

```tsx
const List = lazy(() => import('./List'));
```

Ahora, nuestro componente Lista solo se cargará cuando sea necesario.

### Búsqueda previa de ruta

Next.js también incluye una característica llamada búsqueda previa de ruta. Esta función permite a Next.js obtener previamente el código para otras páginas en segundo plano. De esta forma, cuando el usuario navegue a esas páginas, el código ya estará descargado y la página cargará más rápido.

Para usar la búsqueda previa de rutas, necesitamos usar el componente `Link` de Next.js. Este componente creará un enlace a otra página en nuestra aplicación.

Primero, importemos el componente `Link`:

```tsx
import Link from 'next/link';
```

Luego, podemos usar el componente `Enlace` para crear un enlace a otra página:

```tsx
<Link href="/page2" prefetch>
  <a>Navigate to page 2</a>
</Link>
```

Esto creará un enlace a la ruta `/page2` en nuestra aplicación. El accesorio `prefetch` le indicará a Next.js que obtenga previamente el código para esta ruta en segundo plano.

## Conclusión

En este artículo, aprendimos a crear aplicaciones web progresivas (PWA) con TypeScript y Next.js. Comenzamos creando un PWA simple que carga un componente List desde un archivo JSON. Luego, agregamos TypeScript a nuestro proyecto y usamos los tipos de React para verificar el tipo de nuestros componentes. Finalmente, aprendimos a usar las funciones de Next.js, como la división de código y la obtención previa de rutas, para mejorar el rendimiento de nuestra PWA.