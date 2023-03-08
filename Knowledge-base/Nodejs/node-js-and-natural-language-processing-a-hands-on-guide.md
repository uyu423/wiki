---
title: Node.js 및 자연어 처리: 실습 가이드
description: 
published: true
date: 2023-01-31T08:12:43.683Z
tags: 
editor: markdown
dateCreated: 2023-01-31T07:43:15.361Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Node.js and Natural Language Processing: A Hands-On Guide***English** version of this document is available*](/en/Knowledge-base/Nodejs/node-js-and-natural-language-processing-a-hands-on-guide)
{.links-list}

# Node.js와 자연어 처리: 실습 가이드

이 기사에서는 Node.js의 자연어 처리(NLP)를 살펴보겠습니다. NLP의 기본 사항과 가장 인기 있는 Node.js NLP 라이브러리를 시작하는 방법을 다룰 것입니다.

## 자연어 처리란?

자연어 처리(NLP)는 인간의 언어 처리를 다루는 컴퓨터 과학 및 인공 지능 분야입니다. NLP 알고리즘은 음성 인식, 텍스트 분류, 감정 분석 및 기계 번역과 같은 작업을 수행하는 데 사용됩니다.

## Node.js 및 NLP 시작하기

Node.js는 확장 가능한 백엔드 애플리케이션을 구축할 수 있는 JavaScript 런타임입니다. Node.js는 라이브러리 및 도구의 대규모 에코시스템으로 인해 NLP 애플리케이션에 널리 사용됩니다.

이 섹션에서는 NLP용으로 가장 인기 있는 Node.js 라이브러리 중 일부를 다룰 것입니다.

### 자연스러운

Natural은 Node.js에서 NLP용으로 널리 사용되는 라이브러리입니다. 여기에는 품사 태깅, 표제어 정리 및 워드넷 통합과 같은 다양한 기능이 포함됩니다.

Natural을 설치하려면 다음 명령을 실행합니다.

```
npm install natural
```

Natural이 설치되면 다음과 같이 Node.js 애플리케이션에서 사용할 수 있습니다.

```javascript
var natural = require('natural');

var tokenizer = new natural.WordTokenizer();

var text = "Node.js is a JavaScript runtime";

var tokens = tokenizer.tokenize(text);

console.log(tokens);
// [ 'Node.js', 'is', 'a', 'JavaScript', 'runtime' ]
```

### node-nlp

Node-nlp는 Node.js에서 널리 사용되는 또 다른 NLP 라이브러리입니다. 여기에는 텍스트 분류, 품사 태그 지정 및 명명된 엔터티 인식과 같은 기능이 포함됩니다.

Node-nlp를 설치하려면 다음 명령을 실행합니다.

```
npm install node-nlp
```

Node-nlp가 설치되면 Node.js 애플리케이션에서 다음과 같이 사용할 수 있습니다.

```javascript
var Nlp = require('node-nlp');

var text = "Node.js is a JavaScript runtime";

var results = Nlp.classify(text);

console.log(results);
// [ { label: 'Node.js', score: 0.9 } ]
```

### 타협

Compromise는 Node.js에서 널리 사용되는 또 다른 NLP 라이브러리입니다. 여기에는 품사 태깅, 토큰화 및 감정 분석과 같은 기능이 포함됩니다.

Compromise를 설치하려면 다음 명령을 실행하십시오.

```
npm install compromise
```

Compromise가 설치되면 Node.js 애플리케이션에서 다음과 같이 사용할 수 있습니다.

```javascript
var nlp = require('compromise');

var text = "Node.js is a JavaScript runtime";

var results = nlp.classify(text);

console.log(results);
// [ { label: 'Node.js', score: 0.9 } ]
```

## 결론

이 기사에서는 자연어 처리의 기본 사항과 NLP용으로 가장 인기 있는 Node.js 라이브러리를 시작하는 방법을 다루었습니다.