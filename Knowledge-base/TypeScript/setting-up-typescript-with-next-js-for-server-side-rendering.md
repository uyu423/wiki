---
title: 서버 측 렌더링을 위해 Next.js로 TypeScript 설정
description: 
published: true
date: 2023-02-14T13:55:32.282Z
tags: 
editor: markdown
dateCreated: 2023-02-14T13:55:30.715Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Setting Up TypeScript with Next.js for Server-Side Rendering***English** document is available*](/en/Knowledge-base/TypeScript/setting-up-typescript-with-next-js-for-server-side-rendering)
{.links-list}


# 서버 측 렌더링을 위해 Next.js로 TypeScript 설정

TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. 강력한 구성 요소를 구축하는 데 도움이 되는 클래스, 모듈 및 인터페이스를 제공합니다. 그리고 서버 사이드 렌더링(SSR)을 위해 React와 함께 사용할 수 있습니다.

이 기사에서는 Next.js로 TypeScript를 설정하는 방법을 보여줍니다. Next.js와 함께 TypeScript를 사용할 때의 몇 가지 이점을 살펴보고 시작하는 방법을 보여드리겠습니다.

## Next.js에서 TypeScript를 사용하는 이유는 무엇인가요?

TypeScript를 Next.js와 함께 사용하면 몇 가지 이점이 있습니다.

TypeScript는 오류를 조기에 발견하는 데 도움이 됩니다. 이는 TypeScript가 유형이 지정된 언어이기 때문에 변수, 함수 등의 유형을 지정할 수 있습니다. 이렇게 하면 런타임까지 감지되지 않는 오류를 방지할 수 있습니다.

TypeScript는 또한 코드를 더 읽기 쉽고 유지 관리하기 쉽게 만들 수 있습니다. TypeScript의 유형 주석을 사용하여 변수, 함수 등의 유형을 문서화할 수 있기 때문입니다. 이렇게 하면 다른 개발자가 코드를 더 쉽게 이해할 수 있습니다.

TypeScript를 Next.js와 함께 사용하는 또 다른 이점은 개발 워크플로를 개선할 수 있다는 것입니다. 이는 TypeScript 컴파일러가 코드에서 작업하는 동안 오류가 있는지 확인할 수 있기 때문입니다. 이렇게 하면 테스트하기 전에 코드가 컴파일될 때까지 기다리는 것과 비교하여 많은 시간을 절약할 수 있습니다.

## 시작하기

Next.js와 함께 TypeScript를 사용할 때의 몇 가지 이점을 살펴보았으니 이제 시작하겠습니다.

먼저 Node.js와 TypeScript가 설치되어 있는지 확인하세요. 그런 다음 프로젝트의 새 디렉터리를 만듭니다.

다음으로 TypeScript로 프로젝트를 초기화합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
$ tsc --init
```

이렇게 하면 프로젝트에 tsconfig.json 파일이 생성됩니다. 이 파일에는 프로젝트에 대한 TypeScript 구성이 포함되어 있습니다.

다음으로 프로젝트에 next.config.js라는 새 파일을 만듭니다. 이 파일에는 프로젝트의 Next.js 구성이 포함되어 있습니다.

다음으로 next.config.js 파일에 다음 코드를 추가합니다.

```js
const withTypeScript = require('@zeit/next-typescript');

module.exports = withTypeScript();
```

그러면 TypeScript를 사용하도록 Next.js가 구성됩니다.

다음으로 프로젝트에 pages/index.tsx라는 새 파일을 만듭니다. 이 파일에는 프로젝트의 React 코드가 포함되어 있습니다.

페이지/index.tsx 파일에 다음 코드를 추가합니다.

```js
import * as React from 'react';

export default class extends React.Component {
  static getInitialProps({ req }) {
    const userAgent = req ? req.headers['user-agent'] : navigator.userAgent;
    return { userAgent };
  }

  render() {
    return (
      <div>
        Hello, world!
      </div>
    );
  }
}
```

이 코드는 간단한 "Hello, world!"를 렌더링합니다. 메시지.

마지막으로 다음 명령을 실행하여 개발 서버를 시작합니다.

```
$ npm run dev
```

이제 "Hello, world!"가 표시되어야 합니다. 브라우저에 표시되는 메시지.

## 외부 리소스

- [타입스크립트](https://www.typescriptlang.org/)
- [리액트](https://reactjs.org/)
- [Next.js](https://nextjs.org/)