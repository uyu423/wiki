---
title: 검색 및 분석을 위해 Elasticsearch와 함께 TypeScript 사용
description: 
published: true
date: 2023-02-26T15:32:19.686Z
tags: 
editor: markdown
dateCreated: 2023-02-26T15:32:18.298Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Using TypeScript with Elasticsearch for Search and Analytics***English** document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-elasticsearch-for-search-and-analytics)
{.links-list}


# 검색 및 분석을 위해 Elasticsearch와 함께 TypeScript 사용

Elasticsearch는 다양한 프로그래밍 언어와 함께 사용할 수 있는 강력한 검색 및 분석 엔진입니다. TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript의 상위 집합이므로 개발에 적합합니다.

이 기사에서는 검색 및 분석을 위해 Elasticsearch와 함께 TypeScript를 사용하는 방법을 살펴보겠습니다. Elasticsearch 및 TypeScript의 기본 사항, 개발 환경을 설정하는 방법 및 데이터를 쿼리하는 방법을 다룰 것입니다.

## 엘라스틱서치란?

Elasticsearch는 무료 오픈 소스 분산 검색 및 분석 엔진입니다. Apache Lucene 검색 라이브러리 위에 구축되었으며 전체 텍스트 검색, 집계 및 지리 공간 지원을 비롯한 다양한 기능 세트를 제공합니다.

Elasticsearch는 Wikipedia, Github 및 Stackoverflow와 같은 큰 이름에서 사용되며 빠르고 관련성 높은 검색 결과가 필요한 애플리케이션에 이상적입니다.

## 타입스크립트란?

TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. 클래스, 모듈 및 인터페이스 시스템에 대한 지원을 제공하므로 개발을 위한 탁월한 선택입니다.

TypeScript는 대규모 애플리케이션 개발을 위해 설계되었으며 JavaScript로 트랜스컴파일됩니다. 일반적인 실수를 조기에 포착하고 코드를 유지 관리하기 쉽게 만드는 데 도움이 됩니다.

## 개발 환경 설정

Elasticsearch에서 TypeScript를 사용하기 전에 개발 환경을 설정해야 합니다.

Node.js가 설치되어 있다고 가정하면 다음 명령을 사용하여 TypeScript 컴파일러를 설치할 수 있습니다.

```
npm install -g typescript
```

다음으로 Node.js용 Elasticsearch 클라이언트를 설치해야 합니다. 다음 명령을 사용하여 이를 수행할 수 있습니다.

```
npm install elasticsearch
```

## 데이터 쿼리

이제 개발 환경이 설정되었으므로 코드를 작성해 보겠습니다.

다음 예제는 Node.js 클라이언트를 사용하여 Elasticsearch 인덱스에서 데이터를 쿼리하는 방법을 보여줍니다. 먼저 클라이언트 인스턴스를 만들어야 합니다.

```javascript
var elasticsearch = require('elasticsearch');
var client = new elasticsearch.Client({
  host: 'localhost:9200',
  log: 'trace'
});
```

다음으로 `search` 메서드를 사용하여 데이터를 쿼리할 수 있습니다.

```javascript
client.search({
  index: 'myindex',
  type: 'mytype',
  body: {
    query: {
      match: {
        title: 'elasticsearch'
      }
    }
  }
}).then(function (resp) {
  var hits = resp.hits.hits;
}, function (err) {
  console.trace(err.message);
});
```

위의 예에서 `title` 필드가 용어 `elasticsearch`와 일치하는 `mytype` 유형의 문서에 대해 `myindex` 인덱스를 쿼리하고 있습니다.

## 결론

이 기사에서는 검색 및 분석을 위해 Elasticsearch와 함께 TypeScript를 사용하는 방법을 살펴보았습니다. Elasticsearch 및 TypeScript의 기본 사항, 개발 환경을 설정하는 방법 및 데이터를 쿼리하는 방법을 다루었습니다.