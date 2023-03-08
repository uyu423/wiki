---
title: 056: 점진적 개선과 함께 Nest.js 사용
description: 
published: true
date: 2023-02-15T19:32:25.087Z
tags: 
editor: markdown
dateCreated: 2023-02-15T19:32:17.539Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [056: Using Nest.js with progressive enhancement***English** document is available*](/en/Knowledge-base/Nest-js/Learning/056-using-nest-js-with-progressive-enhancement)
{.links-list}


# 점진적 향상과 함께 Nest.js 사용

Nest.js는 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. Express.js를 기반으로 하며 TypeScript를 사용합니다.

Nest.js는 서버 측 애플리케이션을 구축하기 위한 훌륭한 프레임워크입니다. Express.js를 기반으로 하고 TypeScript를 사용하므로 애플리케이션을 쉽게 개발, 유지 관리 및 확장할 수 있습니다.

그러나 Nest.js에도 단점이 없는 것은 아닙니다. 한 가지 주요 단점은 점진적 향상을 지원하지 않는다는 것입니다. 점진적 향상은 브라우저나 장치에 관계없이 모든 사용자에게 최적의 경험을 제공하는 웹 애플리케이션을 구축하기 위한 기술입니다.

Nest.js는 서버 측 렌더링을 사용하기 때문에 점진적 향상을 지원하지 않습니다. 이는 HTML이 서버에서 생성된 다음 브라우저로 전송됨을 의미합니다. 그런 다음 브라우저는 HTML을 렌더링합니다.

HTML이 모든 사용자에게 동일한 경우에는 문제가 되지 않습니다. 그러나 HTML이 사용자마다 다르면 점진적 향상이 불가능합니다.

이 문제에 대한 해결 방법이 있지만 이상적이지는 않습니다. 한 가지 해결 방법은 Angular 또는 React와 같은 클라이언트 측 프레임워크를 사용하는 것입니다. 이렇게 하면 초기 페이지 로드에 서버측 렌더링을 사용한 다음 후속 페이지 로드에 클라이언트측 렌더링을 사용할 수 있습니다.

또 다른 해결 방법은 초기 페이지 로드에 서버측 렌더링을 사용한 다음 후속 페이지 로드에 클라이언트측 렌더링을 사용하는 하이브리드 방식을 사용하는 것입니다. 이 접근 방식은 코드베이스를 복제해야 하므로 이상적이지 않습니다.

Nest.js를 점진적으로 개선하여 사용하는 가장 좋은 방법은 Angular 또는 React와 같은 클라이언트 측 프레임워크를 사용하는 것입니다. 이렇게 하면 초기 페이지 로드에 서버측 렌더링을 사용한 다음 후속 페이지 로드에 클라이언트측 렌더링을 사용할 수 있습니다.

점진적 향상 기능이 있는 Nest.js를 사용하는 경우 Angular 또는 React와 같은 클라이언트 측 프레임워크 사용을 고려해야 합니다.