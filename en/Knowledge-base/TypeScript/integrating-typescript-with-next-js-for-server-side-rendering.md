---
title: Integrating TypeScript with Next.js for Server-side Rendering
description: 
published: true
date: 2023-02-01T14:04:53.824Z
tags: 
editor: markdown
dateCreated: 2023-02-01T14:04:50.364Z
---

- [서버 측 렌더링을 위해 TypeScript와 Next.js 통합***Korean** version of this document is available*](/ko/Knowledge-base/TypeScript/integrating-typescript-with-next-js-for-server-side-rendering)
{.links-list}
- [将 TypeScript 与 Next.js 集成以进行服务器端渲染***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/TypeScript/integrating-typescript-with-next-js-for-server-side-rendering)
{.links-list}


  Note: This template is for a specific article. If you are not writing this article, please delete this text and replace it with your own content.

# Integrating TypeScript with Next.js for Server-side Rendering

If you're looking to use TypeScript with [Next.js](https://nextjs.org/), you're in luck! Next.js has first-class TypeScript support and it's easy to get up and running with TypeScript in your Next.js project. In this article, we'll take a look at how to set up TypeScript with Next.js and how to use TypeScript with Next.js' [server-side rendering](https://nextjs.org/docs/basic-features/pages#server-side-rendering) feature.

## Setting up TypeScript in Next.js

The first thing we need to do is create a new Next.js project. We can do this using [`create-next-app`](https://github.com/zeit/next.js/tree/canary/packages/create-next-app), which is a command line tool that sets up a new Next.js project for you.

To install `create-next-app`, we need to run the following command:

```
npm init next-app
```

Once `create-next-app` is installed, we can create a new Next.js project by running the following command:

```
create-next-app my-app
```

This will create a new directory called `my-app` with the basic files needed for a Next.js project.

Next, we need to install TypeScript. We can do this by running the following command:

```
npm install --save-dev typescript
```

Once TypeScript is installed, we can create a `tsconfig.json` file in the root of our project. This file tells TypeScript how we want our code to be compiled.

The `tsconfig.json` file should look like this:

```json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "commonjs",
    "jsx": "preserve",
    "outDir": "./build",
    "strict": true
  },
  "exclude": [
    "node_modules"
  ]
}
```

Next, we need to create a `.babelrc` file in the root of our project. This file tells [Babel](https://babeljs.io/) how we want our code to be compiled.

The `.babelrc` file should look like this:

```json
{
  "presets": [
    "next/babel"
  ]
}
```

Now that we have TypeScript and Babel set up, we can create a `.tsx` file in the `pages` directory. This file will be our page that will be server-side rendered.

The `.tsx` file should look like this:

```jsx
import * as React from 'react'

export default function Page() {
  return <div>Hello, world!</div>
}
```

Now that we have our page created, we can start our Next.js development server by running the following command:

```
npm run dev
```

If we navigate to http://localhost:3000, we should see our page being server-side rendered.

## Using TypeScript with Next.js' server-side rendering

Now that we have our project set up, let's take a look at how we can use TypeScript with Next.js' server-side rendering feature.

First, we need to create a file called `api.ts` in the `pages` directory. This file will contain our [`getInitialProps`](https://nextjs.org/docs/basic-features/pages#getinitialprops) function.

The `api.ts` file should look like this:

```js
import { NextPageContext } from 'next'

export default function Page(ctx: NextPageContext) {
  return {
    hello: 'world'
  }
}
```

Next, we need to update our `.tsx` file to call the `api.ts` file. We do this by adding the [`getInitialProps`](https://nextjs.org/docs/basic-features/pages#getinitialprops) property to our `Page` component.

The `.tsx` file should now look like this:

```jsx
import * as React from 'react'
import { PageProps } from 'api'

export default function Page(props: PageProps) {
  return <div>Hello, {props.hello}!</div>
}
```

If we navigate to http://localhost:3000, we should see our page being server-side rendered with the data from our `api.ts` file.

## Wrapping up

In this article, we've seen how to set up TypeScript with Next.js and how to use TypeScript with Next.js' server-side rendering feature. With TypeScript and Next.js, you can easily build type-safe, server-side rendered React applications.