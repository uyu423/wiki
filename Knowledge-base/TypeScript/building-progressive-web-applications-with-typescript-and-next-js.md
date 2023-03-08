---
title: TypeScript 및 Next.js로 프로그레시브 웹 애플리케이션 구축
description: 
published: true
date: 2023-02-02T02:43:47.118Z
tags: 
editor: markdown
dateCreated: 2023-02-02T02:43:45.412Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building Progressive Web Applications with TypeScript and Next.js***English** document is available*](/en/Knowledge-base/TypeScript/building-progressive-web-applications-with-typescript-and-next-js)
{.links-list}


TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. 강력한 구성 요소를 구축하는 데 도움이 되는 클래스, 모듈 및 인터페이스를 제공합니다.

Next.js는 생산 준비가 된 서버 렌더링 앱을 쉽게 만들 수 있는 React 프레임워크입니다. 여기에는 자동 코드 분할, 정적 파일 제공, 경로 처리 및 범용 렌더링과 같은 기능이 포함됩니다.

이 기사에서는 TypeScript와 Next.js를 사용하여 프로그레시브 웹 애플리케이션(PWA)을 빌드하는 방법을 알아봅니다. JSON 파일에서 목록 구성 요소를 로드하는 간단한 PWA를 만드는 것으로 시작하겠습니다. 그런 다음 프로젝트에 TypeScript를 추가하고 구성 요소의 유형을 확인하기 위해 React 타이핑을 사용합니다. 마지막으로 코드 분할 및 경로 미리 가져오기와 같은 Next.js 기능을 사용하여 PWA의 성능을 개선하는 방법을 배웁니다.

## TypeScript와 Next.js로 간단한 PWA 만들기

JSON 파일에서 목록 구성 요소를 로드하는 간단한 Next.js 앱을 만드는 것으로 시작하겠습니다. 목록 구성 요소는 서버에서 렌더링되며 코드 분할 및 경로 미리 가져오기를 포함합니다.

먼저 새로운 Next.js 프로젝트를 생성해 보겠습니다.

```
npx create-next-app my-app
```

다음으로 다음 종속 항목을 설치해야 합니다.

```
npm install --save react react-dom next
```

이제 List 구성 요소를 만들 수 있습니다. `List.js`라는 새 파일을 만들고 다음 코드를 추가합니다.

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

이 구성 요소는 `items` 소품을 사용하여 항목 목록을 렌더링합니다. 각 항목에는 키와 텍스트가 있습니다.

다음으로 목록 항목이 포함된 JSON 파일을 만들어야 합니다. `listItems.json`이라는 새 파일을 만들고 다음 코드를 추가합니다.

```json
[
  { "id": 1, "text": "Item 1" },
  { "id": 2, "text": "Item 2" },
  { "id": 3, "text": "Item 3" }
]
```

이제 `List.js` 구성 요소에서 이 JSON 파일을 가져올 수 있습니다.

```js
import listItems from './listItems.json';
```

마지막으로 List 컴포넌트를 서버에 렌더링하도록 Next.js에 지시해야 합니다. `pages/index.js` 파일을 열고 내용을 다음 코드로 바꿉니다.

```js
import React from 'react';
import List from '../components/List';

const IndexPage = () => <List items={listItems} />;

export default IndexPage;
```

이렇게 하면 서버에서 목록 구성 요소를 렌더링하고 `listItems` JSON 데이터를 구성 요소에 소품으로 전달합니다.

이제 앱을 실행하면 목록 구성 요소가 페이지에 렌더링되는 것을 볼 수 있습니다.

```
npm run dev
```

## 프로젝트에 TypeScript 추가하기

다음으로 프로젝트에 TypeScript를 추가하고 구성 요소의 유형을 확인하기 위해 React 타이핑을 사용합니다.

먼저 TypeScript 컴파일러를 설치해야 합니다.

```
npm install --save-dev typescript
```

그런 다음 프로젝트의 루트에 `tsconfig.json` 파일을 만들어야 합니다. 이 파일에는 TypeScript 구성이 포함됩니다. `tsconfig.json` 파일에 다음 코드를 추가합니다.

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

이 구성은 TypeScript 컴파일러에게 최신 JavaScript 표준(ESNext)을 대상으로 지정하고 코드를 CommonJS 모듈인 것처럼 처리하도록 지시합니다.

다음으로 React 타이핑을 설치해야 합니다.

```
npm install --save-dev @types/react @types/react-dom
```

이제 `List.js` 구성 요소의 이름을 `List.tsx`로 바꾸고 TypeScript를 사용할 수 있습니다. 먼저 소품에 유형을 추가합니다.

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

우리는 `ListProps`라는 소품에 대한 인터페이스를 선언했습니다. 이 인터페이스는 소품의 모양을 정의합니다. 또한 `React.FC` 일반을 사용하여 구성 요소에 유형을 추가했습니다. 이 제네릭을 사용하면 소품 유형을 지정할 수 있습니다.

이제 구성 요소에 유효하지 않은 prop을 전달하려고 하면 유형 오류가 발생합니다.

```tsx
// TypeError: Type '{ items: number[]; }' is not assignable to type 'IntrinsicAttributes & ListProps'.
//   Property 'items' does not exist on type 'IntrinsicAttributes & ListProps'.ts(2322)
<List items={[1, 2, 3]} />
```

## Next.js 기능을 사용하여 성능 향상

마지막으로 코드 분할 및 경로 미리 가져오기와 같은 Next.js 기능을 사용하여 PWA의 성능을 개선하는 방법을 배웁니다.

### 코드 분할

Next.js에는 코드를 여러 묶음으로 분할할 수 있는 코드 분할이라는 기능이 포함되어 있습니다. 이렇게 하면 브라우저는 현재 페이지에 필요한 코드만 다운로드하고 실행할 수 있습니다.

List 구성 요소에서 코드 분할을 사용하려면 `React.lazy` 구성 요소를 사용해야 합니다. 이 구성 요소를 사용하면 런타임에 구성 요소를 동적으로 로드할 수 있습니다.

먼저 `React.lazy` 구성 요소를 가져오겠습니다.

```tsx
import React, { lazy } from 'react';
```

그런 다음 `lazy` 구성 요소를 사용하여 List 구성 요소를 동적으로 로드할 수 있습니다.

```tsx
const List = lazy(() => import('./List'));
```

이제 List 구성 요소는 필요할 때만 로드됩니다.

### 경로 미리 가져오기

Next.js에는 경로 프리페칭이라는 기능도 포함되어 있습니다. 이 기능을 사용하면 Next.js가 백그라운드에서 다른 페이지의 코드를 미리 가져올 수 있습니다. 이렇게 하면 사용자가 해당 페이지로 이동할 때 코드가 이미 다운로드되고 페이지가 더 빨리 로드됩니다.

경로 미리 가져오기를 사용하려면 Next.js의 'Link' 구성 요소를 사용해야 합니다. 이 구성 요소는 앱의 다른 페이지에 대한 링크를 생성합니다.

먼저 `Link` 구성요소를 가져오겠습니다.

```tsx
import Link from 'next/link';
```

그런 다음 `Link` 구성 요소를 사용하여 다른 페이지에 대한 링크를 만들 수 있습니다.

```tsx
<Link href="/page2" prefetch>
  <a>Navigate to page 2</a>
</Link>
```

이렇게 하면 앱에서 `/page2` 경로에 대한 링크가 생성됩니다. `prefetch` 소품은 Next.js에게 백그라운드에서 이 경로에 대한 코드를 미리 가져오라고 지시합니다.

## 결론

이 기사에서는 TypeScript 및 Next.js를 사용하여 프로그레시브 웹 애플리케이션(PWA)을 빌드하는 방법을 배웠습니다. JSON 파일에서 목록 구성 요소를 로드하는 간단한 PWA를 만드는 것으로 시작했습니다. 그런 다음 프로젝트에 TypeScript를 추가하고 구성 요소의 유형을 확인하기 위해 React 타이핑을 사용했습니다. 마지막으로 코드 분할 및 경로 미리 가져오기와 같은 Next.js 기능을 사용하여 PWA의 성능을 개선하는 방법을 배웠습니다.