---
title: 서버 측 렌더링을 위해 TypeScript와 Next.js 통합
description: 
published: true
date: 2023-02-01T14:04:51.858Z
tags: 
editor: markdown
dateCreated: 2023-02-01T14:04:50.365Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Integrating TypeScript with Next.js for Server-side Rendering***English** version of this document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-next-js-for-server-side-rendering)
{.links-list}


  참고: 이 템플릿은 특정 기사용입니다. 이 글을 작성하지 않는 경우 이 텍스트를 삭제하고 자신의 콘텐츠로 교체하십시오.

# 서버 측 렌더링을 위해 TypeScript를 Next.js와 통합

TypeScript를 [Next.js](https://nextjs.org/)와 함께 사용하려는 경우 운이 좋습니다! Next.js는 최고 수준의 TypeScript 지원을 제공하며 Next.js 프로젝트에서 TypeScript를 쉽게 시작하고 실행할 수 있습니다. 이 문서에서는 Next.js로 TypeScript를 설정하는 방법과 Next.js의 [서버 측 렌더링](https://nextjs.org/docs/basic-features)에서 TypeScript를 사용하는 방법을 살펴보겠습니다. /pages#server-side-rendering) 기능.

## Next.js에서 TypeScript 설정하기

가장 먼저 해야 할 일은 새로운 Next.js 프로젝트를 만드는 것입니다. 이를 설정하는 명령줄 도구인 [`create-next-app`](https://github.com/zeit/next.js/tree/canary/packages/create-next-app)을 사용하여 이를 수행할 수 있습니다. 새로운 Next.js 프로젝트를 시작하세요.

`create-next-app`을 설치하려면 다음 명령을 실행해야 합니다.

```
npm init next-app
```

`create-next-app`이 설치되면 다음 명령을 실행하여 새로운 Next.js 프로젝트를 생성할 수 있습니다.

```
create-next-app my-app
```

그러면 Next.js 프로젝트에 필요한 기본 파일이 있는 `my-app`이라는 새 디렉토리가 생성됩니다.

다음으로 TypeScript를 설치해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
npm install --save-dev typescript
```

TypeScript가 설치되면 프로젝트의 루트에 `tsconfig.json` 파일을 만들 수 있습니다. 이 파일은 TypeScript에 코드를 컴파일하는 방법을 알려줍니다.

`tsconfig.json` 파일은 다음과 같아야 합니다.

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

다음으로 프로젝트의 루트에 `.babelrc` 파일을 생성해야 합니다. 이 파일은 [Babel](https://babeljs.io/)에 코드를 컴파일하는 방법을 알려줍니다.

`.babelrc` 파일은 다음과 같아야 합니다.

```json
{
  "presets": [
    "next/babel"
  ]
}
```

이제 TypeScript와 Babel이 설정되었으므로 `pages` 디렉토리에 `.tsx` 파일을 만들 수 있습니다. 이 파일은 서버 측에서 렌더링될 페이지가 됩니다.

`.tsx` 파일은 다음과 같아야 합니다.

```jsx
import * as React from 'react'

export default function Page() {
  return <div>Hello, world!</div>
}
```

이제 페이지가 생성되었으므로 다음 명령을 실행하여 Next.js 개발 서버를 시작할 수 있습니다.

```
npm run dev
```

http://localhost:3000으로 이동하면 페이지가 서버측에서 렌더링되는 것을 볼 수 있습니다.

## Next.js의 서버측 렌더링과 함께 TypeScript 사용

이제 프로젝트가 설정되었으므로 Next.js의 서버 측 렌더링 기능과 함께 TypeScript를 사용하는 방법을 살펴보겠습니다.

먼저 `pages` 디렉토리에 `api.ts`라는 파일을 만들어야 합니다. 이 파일에는 [`getInitialProps`](https://nextjs.org/docs/basic-features/pages#getinitialprops) 함수가 포함됩니다.

`api.ts` 파일은 다음과 같아야 합니다.

```js
import { NextPageContext } from 'next'

export default function Page(ctx: NextPageContext) {
  return {
    hello: 'world'
  }
}
```

다음으로 `.tsx` 파일을 업데이트하여 `api.ts` 파일을 호출해야 합니다. 이를 위해 [`getInitialProps`](https://nextjs.org/docs/basic-features/pages#getinitialprops) 속성을 `Page` 구성 요소에 추가합니다.

`.tsx` 파일은 이제 다음과 같아야 합니다.

```jsx
import * as React from 'react'
import { PageProps } from 'api'

export default function Page(props: PageProps) {
  return <div>Hello, {props.hello}!</div>
}
```

http://localhost:3000으로 이동하면 페이지가 `api.ts` 파일의 데이터로 서버측에서 렌더링되는 것을 볼 수 있습니다.

## 마무리

이 기사에서는 Next.js로 TypeScript를 설정하는 방법과 Next.js의 서버 측 렌더링 기능으로 TypeScript를 사용하는 방법을 살펴보았습니다. TypeScript 및 Next.js를 사용하면 유형이 안전한 서버 측 렌더링 React 애플리케이션을 쉽게 구축할 수 있습니다.