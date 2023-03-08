---
title: 위치 기반 서비스를 위해 TypeScript와 Google Maps API 통합
description: 
published: true
date: 2023-02-06T18:55:23.336Z
tags: 
editor: markdown
dateCreated: 2023-02-06T18:55:17.687Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Integrating TypeScript with Google Maps API for Location-Based Services***English** document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-google-maps-api-for-location-based-services)
{.links-list}


# 위치 기반 서비스를 위해 TypeScript와 Google Maps API 통합

TypeScript는 유형 검사 및 기타 이점을 가능하게 하는 JavaScript의 상위 집합입니다. Google Maps API는 대화형 지도 및 지오코딩을 지원하는 인기 있는 위치 서비스용 API입니다. 이 기사에서는 TypeScript를 Google Maps API와 통합하여 위치 기반 서비스를 만드는 방법을 보여줍니다.

## 타입스크립트란?

TypeScript는 유형 검사 및 기타 이점을 가능하게 하는 JavaScript의 상위 집합입니다. TypeScript는 기존 JavaScript 코드와 함께 사용하기 쉽고 점진적으로 채택할 수 있습니다.

## Google 지도 API란 무엇인가요?

Google Maps API는 대화형 지도 및 지오코딩을 지원하는 인기 있는 위치 서비스용 API입니다. API를 사용하여 지도, 검색, 내비게이션과 같은 위치 기반 서비스를 만들 수 있습니다.

## TypeScript를 Google Maps API와 통합하는 방법

TypeScript와 함께 Google Maps API를 사용하려면 TypeScript 선언 파일을 만들어야 합니다. TypeScript 선언 파일은 JavaScript 라이브러리에 대한 TypeScript 유형 정보를 포함하는 파일입니다. Google Maps API의 선언 파일은 GitHub에서 사용할 수 있습니다.

선언 파일을 다운로드했으면 다음 코드 줄을 사용하여 TypeScript 프로젝트에 포함할 수 있습니다.

```typescript
/// <reference path="google-maps-api.d.ts" />
```

이제 TypeScript 코드에서 Google Maps API를 사용할 수 있습니다. 예를 들어 다음 코드는 지도를 만들고 지도에 마커를 추가합니다.

```typescript
var map: google.maps.Map;
var marker: google.maps.Marker;

map = new google.maps.Map(document.getElementById('map'), {
  zoom: 8,
  center: {lat: -34.397, lng: 150.644}
});

marker = new google.maps.Marker({
  position: {lat: -34.397, lng: 150.644},
  map: map
});
```

## 자원

- [타입스크립트](https://www.typescriptlang.org/)
- [Google 지도 API](https://developers.google.com/maps/documentation/javascript/)
- [TypeScript 선언 파일](https://www.typescriptlang.org/docs/handbook/declaration-files/introduction.html)
- [google-maps-api.d.ts](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/google-maps/index.d.ts)