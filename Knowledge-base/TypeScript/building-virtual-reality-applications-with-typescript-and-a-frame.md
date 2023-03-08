---
title: TypeScript 및 A-Frame으로 가상 현실 애플리케이션 구축
description: 
published: true
date: 2023-02-01T10:43:35.040Z
tags: 
editor: markdown
dateCreated: 2023-02-01T10:43:33.598Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Building Virtual Reality Applications with TypeScript and A-Frame***English** version of this document is available*](/en/Knowledge-base/TypeScript/building-virtual-reality-applications-with-typescript-and-a-frame)
{.links-list}


  ChatGPT는 TypeScript 및 A-Frame을 사용하여 가상 현실(VR) 애플리케이션을 구축하기 위한 강력한 오픈 소스 프레임워크입니다.

TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. 대규모 웹 애플리케이션을 구축하는 데 널리 사용되는 언어입니다. A-Frame은 HTML을 사용하여 VR 애플리케이션을 구축하기 위한 웹 프레임워크입니다.

이 기사에서는 TypeScript 및 A-Frame을 사용하여 VR 애플리케이션을 빌드하는 방법을 보여줍니다. 다음 주제를 다룰 것입니다.

* 개발 환경 설정
* 기본 VR 애플리케이션 만들기
* VR 애플리케이션에 상호작용 추가

### 개발 환경 설정

VR 애플리케이션 구축을 시작하기 전에 개발 환경을 설정해야 합니다. 다음 소프트웨어가 필요합니다.

* 텍스트 편집기. Visual Studio Code를 권장합니다.
* Node.js 및 npm 패키지 관리자.

필요한 소프트웨어를 설치했으면 다음 명령을 실행하여 새 TypeScript 프로젝트를 생성할 수 있습니다.

```
npm init typescript
```

이렇게 하면 프로젝트 디렉토리에 `tsconfig.json`이라는 새 파일이 생성됩니다. 이 파일에는 프로젝트에 대한 TypeScript 구성이 포함되어 있습니다.

다음으로 A-Frame TypeScript 유형 정의를 설치해야 합니다. 다음 명령으로 이를 수행할 수 있습니다.

```
npm install @types/aframe --save-dev
```

그러면 `node_modules` 디렉토리에 A-Frame 유형 정의가 설치되고 `tsconfig.json` 파일에 추가됩니다.

### 기본 VR 애플리케이션 만들기

이제 개발 환경이 설정되었으므로 VR 애플리케이션을 만들 수 있습니다.

기본 VR 애플리케이션을 만드는 것부터 시작하겠습니다. 프로젝트 디렉터리에 `index.ts`라는 새 파일을 만들고 다음 코드를 추가합니다.

```typescript
import 'aframe';

const scene = document.querySelector('a-scene');

const box = document.createElement('a-entity');
box.setAttribute('geometry', {
  primitive: 'box',
  width: 1,
  height: 1,
  depth: 1
});
box.setAttribute('material', {
  color: 'red'
});

scene.appendChild(box);
```

이 코드는 새 `<a-scene>` 요소를 만들고 여기에 빨간색 상자를 추가합니다. `<a-scene>` 요소는 A-Frame VR 애플리케이션의 루트 요소입니다. 여기에는 VR 장면이 포함되며 VR 헤드셋과 컨트롤러를 처리합니다.

`<a-entity>` 요소는 VR 콘텐츠의 일반 컨테이너입니다. 형상, 재질, 애니메이션 및 기타 구성 요소를 포함할 수 있습니다. 이 예에서는 이를 사용하여 상자를 만듭니다.

'geometry' 구성 요소는 개체의 모양을 정의합니다. 이 예에서는 `box` 기하학을 사용하고 있습니다. `width`, `height` 및 `depth` 속성은 상자의 크기를 정의합니다.

'재료' 구성 요소는 개체의 모양을 정의합니다. 이 예에서는 `color` 재질을 사용하고 있습니다. `color` 속성은 상자의 색상을 정의합니다.

이 코드를 실행하려면 JavaScript로 컴파일하고 로컬 웹 서버를 실행해야 합니다. 다음 명령으로 이를 수행할 수 있습니다.

```
tsc
http-server
```

`tsc` 명령은 TypeScript 코드를 JavaScript로 컴파일합니다. `http-server` 명령은 로컬 웹 서버를 시작합니다.

VR 애플리케이션을 보려면 웹 브라우저에서 URL `http://localhost:8080`을 여십시오. 화면 중앙에 빨간색 상자가 표시됩니다.

### VR 애플리케이션에 상호작용 추가

이제 기본 VR 응용 프로그램이 있으므로 상호 작용을 추가할 수 있습니다.

이 예에서는 장면에 커서 구성 요소를 추가합니다. 커서 구성 요소는 VR 장면에 3D 커서를 추가합니다. 사용자는 개체를 보고 클릭하여 VR 장면과 상호 작용할 수 있습니다.

먼저 커서 구성 요소를 설치해야 합니다. 다음 명령으로 이를 수행할 수 있습니다.

```
npm install aframe-cursor-component --save-dev
```

이렇게 하면 `node_modules` 디렉터리에 커서 구성 요소가 설치됩니다.

다음으로 컴포넌트를 A-Frame에 등록해야 합니다. `index.ts` 파일에 다음 코드를 추가하여 이를 수행할 수 있습니다.

```typescript
import 'aframe';
import 'aframe-cursor-component';

const scene = document.querySelector('a-scene');

const box = document.createElement('a-entity');
box.setAttribute('geometry', {
  primitive: 'box',
  width: 1,
  height: 1,
  depth: 1
});
box.setAttribute('material', {
  color: 'red'
});

scene.appendChild(box);
```

커서 컴포넌트를 가져와 A-Frame에 등록하는 코드입니다.

마지막으로 커서 구성 요소를 장면에 추가해야 합니다. `index.ts` 파일에 다음 코드를 추가하여 이를 수행할 수 있습니다.

```typescript
import 'aframe';
import 'aframe-cursor-component';

const scene = document.querySelector('a-scene');

scene.setAttribute('cursor', {
  maxDistance: 30,
  fuseTimeout: 500
});

const box = document.createElement('a-entity');
box.setAttribute('geometry', {
  primitive: 'box',
  width: 1,
  height: 1,
  depth: 1
});
box.setAttribute('material', {
  color: 'red'
});

scene.appendChild(box);
```

이 코드는 장면에 커서 구성 요소를 추가합니다. `maxDistance` 및 `fuseTimeout` 속성은 커서가 숨겨지기 전에 사용자가 개체에서 얼마나 멀리 떨어져 있고 얼마나 오래 있을 수 있는지를 정의합니다.

이 코드를 테스트하려면 웹 브라우저에서 URL `http://localhost:8080`을 여십시오. 화면 중앙에 빨간색 상자가 표시됩니다. 상자를 보면 커서가 나타납니다. 상자를 클릭하면 커서가 사라집니다.

### 결론

이 기사에서는 TypeScript 및 A-Frame을 사용하여 VR 애플리케이션을 빌드하는 방법을 보여주었습니다. 우리는 다음 주제를 다루었습니다.

* 개발 환경 설정
* 기본 VR 애플리케이션 만들기
* VR 애플리케이션에 상호작용 추가

TypeScript 및 A-Frame으로 VR 애플리케이션을 구축하는 방법에 대해 자세히 알아보려면 다음 리소스를 권장합니다.

* A-Frame TypeScript 문서
* A-프레임 웹사이트
* A-프레임 커서 설명서