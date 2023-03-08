---
title: Angular로 프로그레시브 웹 앱(PWA)을 구축하는 방법
description: 
published: true
date: 2023-02-06T07:55:34.138Z
tags: 
editor: markdown
dateCreated: 2023-02-06T07:55:32.530Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Build a Progressive Web App (PWA) with Angular***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-progressive-web-app-pwa-with-angular)
{.links-list}


# Angular로 프로그레시브 웹 앱(PWA)을 구축하는 방법

## PWA란?

PWA(Progressive Web App)는 최신 웹 기술을 사용하여 사용자에게 앱과 같은 경험을 제공하는 웹 애플리케이션입니다. PWA는 반응이 빠르고 빠르며 사용자의 홈 화면에 설치할 수 있습니다.

## 왜 PWA를 구축해야 할까요?

PWA는 향상된 성능, 오프라인 기능 및 앱과 유사한 기능을 포함하여 기존 웹 앱에 비해 많은 이점을 제공합니다.

## Angular로 PWA를 구축하는 방법

Angular는 PWA를 구축하는 데 널리 사용되는 프레임워크입니다. 이 기사에서는 Angular로 PWA를 만드는 방법을 보여줍니다.

### 1. 새 Angular 프로젝트 만들기

먼저 새 Angular 프로젝트를 만들어야 합니다. Angular CLI를 사용하여 이 작업을 수행할 수 있습니다.

다음 명령을 실행하여 새 Angular 프로젝트를 만듭니다.

```
ng new my-pwa
```

이렇게 하면 Angular 프로젝트와 함께 `my-pwa`라는 새 폴더가 생성됩니다.

### 2. PWA 기능 추가

다음으로 Angular 프로젝트에 PWA 기능을 추가해야 합니다. @angular/pwa 패키지를 사용하여 이를 수행할 수 있습니다.

먼저 @angular/pwa 패키지를 설치합니다.

```
npm install @angular/pwa --save
```

다음으로 PWA 매니페스트를 `index.html` 파일에 추가합니다.

```html
<link rel="manifest" href="/manifest.json">
```

마지막으로 서비스 작업자 파일을 생성합니다.

```
ng generate service-worker
```

그러면 `src/` 폴더에 `ngsw-worker.js`라는 파일이 생성됩니다.

### 3. PWA 테스트

이제 Angular 프로젝트에 PWA 기능을 추가했으므로 PWA를 테스트할 수 있습니다.

PWA를 테스트하려면 로컬 서버를 실행해야 합니다. Angular CLI에는 개발 서버가 포함되어 있으므로 이를 사용할 수 있습니다.

다음 명령을 실행하여 개발 서버를 시작하십시오.

```
ng serve
```

이제 브라우저를 열고 http://localhost:4200/으로 이동합니다. Angular 앱이 실행되는 것을 볼 수 있습니다.

PWA 기능을 테스트하려면 Chrome용 [Lighthouse](https://developers.google.com/web/tools/lighthouse/) 확장 프로그램을 설치해야 합니다.

Lighthouse를 설치했으면 확장 프로그램을 열고 "보고서 생성" 버튼을 클릭합니다.

Lighthouse가 앱을 분석하고 보고서를 제공합니다. 보고서는 앱이 PWA 체크리스트를 통과했는지 여부를 알려줍니다.

앱이 체크리스트를 통과하지 못한 경우 더 많은 PWA 기능을 추가해 보세요. 예를 들어 [푸시 알림](https://developers.google.com/web/fundamentals/getting-started/codelabs/push-notifications/) 또는 [백그라운드 동기화](https://developers.google. com/web/fundamentals/getting-started/primers/background-sync).

## 결론

이 기사에서는 Angular를 사용하여 프로그레시브 웹 앱을 빌드하는 방법을 설명했습니다. PWA는 향상된 성능, 오프라인 기능 및 앱과 유사한 기능을 포함하여 기존 웹 앱에 비해 많은 이점을 제공합니다. Angular를 사용하면 웹 앱에 PWA 기능을 쉽게 추가할 수 있습니다.