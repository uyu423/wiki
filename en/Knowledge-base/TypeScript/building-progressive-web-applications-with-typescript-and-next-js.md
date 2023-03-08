---
title: Building Progressive Web Applications with TypeScript and Next.js
description: 
published: true
date: 2023-02-02T02:43:49.800Z
tags: 
editor: markdown
dateCreated: 2023-02-02T02:43:45.420Z
---

- [Creación de aplicaciones web progresivas con TypeScript y Next.js***Spanish** document is available*](/es/Knowledge-base/TypeScript/building-progressive-web-applications-with-typescript-and-next-js)
{.links-list}
- [使用 TypeScript 和 Next.js 构建渐进式 Web 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/TypeScript/building-progressive-web-applications-with-typescript-and-next-js)
{.links-list}
- [TypeScript 및 Next.js로 프로그레시브 웹 애플리케이션 구축***Korean** document is available*](/ko/Knowledge-base/TypeScript/building-progressive-web-applications-with-typescript-and-next-js)
{.links-list}


TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. It offers classes, modules, and interfaces to help you build robust components.

Next.js is a React framework that makes it easy to create production-ready server-rendered apps. It includes features like Automatic code splitting, Static file serving, Routes handling, and Universal rendering.

In this article, we'll learn how to build progressive web applications (PWAs) using TypeScript and Next.js. We'll start by creating a simple PWA that loads a List component from a JSON file. Then, we'll add TypeScript to our project and use the React typings for type-checking our components. Finally, we'll learn how to use Next.js features like code splitting and route prefetching to improve the performance of our PWA.

## Creating a simple PWA with TypeScript and Next.js

We'll start by creating a simple Next.js app that loads a List component from a JSON file. The List component will be server-rendered and will include code splitting and route prefetching.

First, let's create a new Next.js project:

```
npx create-next-app my-app
```

Next, we need to install the following dependencies:

```
npm install --save react react-dom next
```

Now, we can create our List component. Create a new file named `List.js` and add the following code:

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

This component will take an `items` prop and render a list of items. Each item will have a key and a text.

Next, we need to create a JSON file that contains our list items. Create a new file named `listItems.json` and add the following code:

```json
[
  { "id": 1, "text": "Item 1" },
  { "id": 2, "text": "Item 2" },
  { "id": 3, "text": "Item 3" }
]
```

Now, we can import this JSON file in our `List.js` component:

```js
import listItems from './listItems.json';
```

Finally, we need to tell Next.js to render our List component on the server. Open the `pages/index.js` file and replace the contents with the following code:

```js
import React from 'react';
import List from '../components/List';

const IndexPage = () => <List items={listItems} />;

export default IndexPage;
```

This will render our List component on the server and pass the `listItems` JSON data to the component as a prop.

Now, if we run our app, we should see our List component being rendered on the page:

```
npm run dev
```

## Adding TypeScript to our project

Next, we'll add TypeScript to our project and use the React typings for type-checking our components.

First, we need to install the TypeScript compiler:

```
npm install --save-dev typescript
```

Then, we need to create a `tsconfig.json` file in the root of our project. This file will contain our TypeScript configuration. Add the following code to the `tsconfig.json` file:

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

This configuration will tell the TypeScript compiler to target the latest JavaScript standard (ESNext) and to treat our code as if it were CommonJS modules.

Next, we need to install the React typings:

```
npm install --save-dev @types/react @types/react-dom
```

Now, we can rename our `List.js` component to `List.tsx` and start using TypeScript. First, we'll add types to our props:

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

We've declared an interface for our props called `ListProps`. This interface defines the shape of our props. We've also added types to our component using the `React.FC` generic. This generic allows us to specify the type of our props.

Now, if we try to pass an invalid prop to our component, we'll get a type error:

```tsx
// TypeError: Type '{ items: number[]; }' is not assignable to type 'IntrinsicAttributes & ListProps'.
//   Property 'items' does not exist on type 'IntrinsicAttributes & ListProps'.ts(2322)
<List items={[1, 2, 3]} />
```

## Using Next.js features to improve performance

Finally, we'll learn how to use Next.js features like code splitting and route prefetching to improve the performance of our PWA.

### Code splitting

Next.js includes a feature called code splitting that allows us to split our code into multiple bundles. This way, the browser can download and execute only the code that is required for the current page.

To use code splitting in our List component, we need to use the `React.lazy` component. This component allows us to dynamically load components at runtime.

First, let's import the `React.lazy` component:

```tsx
import React, { lazy } from 'react';
```

Then, we can use the `lazy` component to dynamically load our List component:

```tsx
const List = lazy(() => import('./List'));
```

Now, our List component will only be loaded when it is needed.

### Route prefetching

Next.js also includes a feature called route prefetching. This feature allows Next.js to prefetch the code for other pages in the background. This way, when the user navigates to those pages, the code will already be downloaded and the page will load faster.

To use route prefetching, we need to use the `Link` component from Next.js. This component will create a link to another page in our app.

First, let's import the `Link` component:

```tsx
import Link from 'next/link';
```

Then, we can use the `Link` component to create a link to another page:

```tsx
<Link href="/page2" prefetch>
  <a>Navigate to page 2</a>
</Link>
```

This will create a link to the `/page2` route in our app. The `prefetch` prop will tell Next.js to prefetch the code for this route in the background.

## Conclusion

In this article, we've learned how to build progressive web applications (PWAs) using TypeScript and Next.js. We've started by creating a simple PWA that loads a List component from a JSON file. Then, we've added TypeScript to our project and used the React typings for type-checking our components. Finally, we've learned how to use Next.js features like code splitting and route prefetching to improve the performance of our PWA.