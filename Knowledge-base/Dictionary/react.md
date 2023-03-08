---
title: React
description: 
published: true
date: 2023-01-31T13:57:54.551Z
tags: 
editor: markdown
dateCreated: 2023-01-31T13:57:52.915Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [React***English** version of this document is available*](/en/Knowledge-base/Dictionary/react)
{.links-list}


# 개요
React는 사용자 인터페이스를 구축하기 위한 JavaScript 라이브러리입니다. Facebook과 개별 개발자 및 회사 커뮤니티에서 유지 관리합니다. React는 단일 페이지 또는 모바일 애플리케이션 개발의 기반으로 사용할 수 있습니다.

# 역사
React는 Facebook의 소프트웨어 엔지니어인 Jordan Walke가 만들었습니다. 그는 2011년에 "FaxJS"라는 React의 초기 프로토타입을 처음 출시했습니다. React의 첫 번째 공개 릴리스는 2013년 5월 29일이었습니다. 그 이후로 React는 사용자 인터페이스 구축을 위한 가장 인기 있는 JavaScript 라이브러리 중 하나가 되었습니다.

# 설명
React는 사용자 인터페이스를 구축하기 위한 JavaScript 라이브러리입니다. 웹 응용 프로그램에서 사용할 수 있는 재사용 가능한 구성 요소를 만드는 데 사용됩니다. React는 단순하고 효율적이며 유연하게 설계되었습니다. 선언적 프로그래밍 스타일을 사용하여 더 쉽게 읽고 이해할 수 있습니다.

# 특징
React에는 웹 개발에 널리 사용되는 몇 가지 기능이 있습니다. 여기에는 다음이 포함됩니다.

- **가상 DOM:** React는 가상 DOM을 사용하여 UI를 효율적으로 업데이트합니다. 이를 통해 React는 전체 페이지를 다시 렌더링하지 않고도 UI를 변경할 수 있습니다.

- **JSX:** React는 개발자가 JavaScript 코드에서 HTML과 유사한 구문을 작성할 수 있도록 하는 JSX라는 구문 확장을 사용합니다.

- **React Native:** React Native는 개발자가 React를 사용하여 iOS 및 Android용 기본 앱을 만들 수 있는 모바일 개발 프레임워크입니다.

- **Flux:** Flux는 애플리케이션 내에서 데이터 흐름을 관리하는 데 도움이 되는 React용 애플리케이션 아키텍처입니다.

- **서버측 렌더링:** React는 서버측 렌더링을 지원하므로 개발자가 React 구성 요소를 클라이언트에 보내기 전에 서버에서 렌더링할 수 있습니다.

# 예
다음은 항목 목록을 표시하는 React 구성 요소의 예입니다.

```javascript
import React from 'react';

class List extends React.Component {
  render() {
    return (
      <ul>
        {this.props.items.map(item => (
          <li key={item.id}>{item.name}</li>
        ))}
      </ul>
    );
  }
}
```

# 장점과 단점
React에는 다음과 같은 몇 가지 장점이 있습니다.

- **쉽게 배우기:** React는 배우고 사용하기 쉬우므로 모든 기술 수준의 개발자에게 적합합니다.

- **성능:** React의 가상 DOM 및 서버 측 렌더링은 빠르고 효율적입니다.

- **재사용 가능한 구성 요소:** React 구성 요소는 재사용 가능하므로 복잡한 사용자 인터페이스를 쉽게 만들 수 있습니다.

그러나 React 사용에는 다음과 같은 몇 가지 단점도 있습니다.

- **가파른 학습 곡선:** React는 라이브러리를 처음 사용하는 개발자가 배우기 어려울 수 있습니다.

- **문서 부족:** React의 문서는 이해하기 어려울 수 있어 개발자가 시작하기 어려울 수 있습니다.

# 논란
React는 JSX 구문을 사용하기 때문에 논란의 대상이 되었습니다. 일부 개발자는 JSX가 "진짜" 프로그래밍 언어가 아니며 웹 개발에 사용해서는 안 된다고 주장했습니다. 다른 사람들은 JSX가 복잡한 사용자 인터페이스를 더 쉽게 작성할 수 있게 해주는 강력한 도구라고 주장했습니다.

# 관련 기술
React는 종종 다음과 같은 다른 기술과 함께 사용됩니다.

- **Redux:** Redux는 애플리케이션 내에서 데이터 흐름을 관리하는 데 도움이 되는 React용 상태 관리 라이브러리입니다.

- **GraphQL:** GraphQL은 서버에서 데이터를 더 쉽게 가져올 수 있는 API용 쿼리 언어입니다.

- **TypeScript:** TypeScript는 React 애플리케이션에 유형 안전성을 추가하는 유형이 지정된 JavaScript 상위 집합입니다.

# 여담
React는 사용자 인터페이스 구축을 위한 가장 인기 있는 JavaScript 라이브러리 중 하나가 되었습니다. Facebook, Airbnb 및 Netflix와 같은 많은 대기업에서 사용합니다. React는 또한 Instagram 및 Uber와 같은 가장 인기 있는 모바일 앱을 만드는 데 사용되었습니다.

# 기타
React는 오픈 소스 프로젝트이며 MIT 라이선스로 배포됩니다. 즉, 수수료나 로열티를 지불하지 않고도 누구나 무료로 React를 사용할 수 있습니다. React는 또한 대규모 개발자 커뮤니티에서 적극적으로 유지 관리하고 지원합니다.