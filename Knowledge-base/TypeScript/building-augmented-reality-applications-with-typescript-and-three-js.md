---
title: TypeScript 및 Three.js로 증강 현실 애플리케이션 구축
description: 
published: true
date: 2023-01-31T17:17:19.080Z
tags: 
editor: markdown
dateCreated: 2023-01-31T17:17:17.446Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Building Augmented Reality Applications with TypeScript and Three.js***English** version of this document is available*](/en/Knowledge-base/TypeScript/building-augmented-reality-applications-with-typescript-and-three-js)
{.links-list}



# TypeScript 및 Three.js로 증강 현실 애플리케이션 구축

ARKit 및 ARCore의 출시로 증강 현실(AR)이 더욱 주류가 되고 있습니다. 이 새로운 SDK를 통해 개발자는 iOS 및 Android 기기에서 수백만 명의 사용자를 위한 AR 경험을 만들 수 있습니다.

그러나 AR 애플리케이션 개발은 어려울 수 있습니다. SDK는 지속적으로 변경되며 개발자가 시작하는 데 도움이 되는 리소스가 거의 없습니다.

이 기사에서는 TypeScript 및 Three.js를 사용하여 웹용 AR 애플리케이션을 만드는 방법을 보여줍니다. 개발 환경 설정, 간단한 AR 장면 생성, 웹 서버에 애플리케이션 배포에 대해 다룹니다.

## 개발 환경 설정

AR 애플리케이션 구축을 시작하기 전에 개발 환경을 설정해야 합니다.

먼저 [Node.js](https://nodejs.org/en/)를 설치해야 합니다. Node.js는 웹 브라우저 외부에서 JavaScript 코드를 실행할 수 있게 해주는 JavaScript 런타임입니다. Node.js를 사용하여 애플리케이션용 로컬 웹 서버를 실행합니다.

다음으로 [TypeScript](https://www.typescriptlang.org/)를 설치해야 합니다. TypeScript는 정적 유형 검사 및 기타 기능을 추가하는 JavaScript의 상위 집합입니다. TypeScript를 사용하여 AR 애플리케이션을 작성할 것입니다.

마지막으로 [Three.js](https://threejs.org/)를 설치해야 합니다. Three.js는 3D 그래픽을 만들기 위한 JavaScript 라이브러리입니다. Three.js를 사용하여 AR 장면을 만들 것입니다.

## 간단한 AR 장면 만들기

이제 개발 환경이 설정되었으므로 AR 장면을 만들 수 있습니다.

먼저 새 TypeScript 파일을 만들고 Three.js를 가져와야 합니다.

```typescript
import * as THREE from 'three';
```

다음으로 새 Three.js 장면을 만들어야 합니다.

```typescript
const scene = new THREE.Scene();
```

이제 장면에 몇 가지 개체를 추가할 수 있습니다. 간단한 큐브부터 시작하겠습니다.

```typescript
const geometry = new THREE.BoxGeometry(1, 1, 1);
const material = new THREE.MeshBasicMaterial({ color: 0xff0000 });
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);
```

마지막으로 장면을 렌더링해야 합니다.

```typescript
const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

renderer.render(scene, camera);
```

모든 것이 잘 되었다면 웹 브라우저에 빨간색 큐브가 표시되어야 합니다.

## 애플리케이션 배포

이제 기본 AR 장면이 있으므로 이를 웹 서버에 배포해야 합니다.

먼저 [http-server](https://www.npmjs.com/package/http-server) Node.js 모듈을 설치해야 합니다.

```
npm install -g http-server
```

다음으로 TypeScript 코드를 JavaScript로 컴파일해야 합니다.

```
tsc main.ts
```

마지막으로 웹 서버를 시작할 수 있습니다.

```
http-server
```

이제 http://localhost:8080에서 애플리케이션에 액세스할 수 있습니다.

## 결론

이 기사에서는 TypeScript와 Three.js를 사용하여 웹용 AR 애플리케이션을 만드는 방법을 살펴보았습니다. 지금까지 개발 환경 설정, 간단한 AR 장면 생성, 웹 서버에 애플리케이션 배포에 대해 다뤘습니다.

AR 개발에 대해 자세히 알아보려면 다음 리소스를 확인하세요.

- [ARKit 101](https://www.raywenderlich.com/160517/arkit-101-using-arkit-build-augmented-reality-apps)
- [ARCore 101](https://www.raywenderlich.com/166886/arcore-101-arkit-equivalent-android)
- [A-프레임](https://aframe.io/)