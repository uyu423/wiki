---
title: Kotlin 및 Express.js: Node.js 프레임워크로 웹 애플리케이션 구축
description: 
published: true
date: 2023-02-05T12:55:28.085Z
tags: 
editor: markdown
dateCreated: 2023-02-05T12:55:22.660Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and Express.js: Building a Web Application with a Node.js Framework***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-express-js-building-a-web-application-with-a-node-js-framework)
{.links-list}


# Kotlin 및 Express.js: Node.js 프레임워크로 웹 애플리케이션 구축

Kotlin은 다양한 프레임워크를 사용하여 웹 애플리케이션을 구축하는 데 사용할 수 있는 JVM 언어입니다. 이 기사에서는 Kotlin을 Express.js 프레임워크와 함께 사용하는 데 중점을 둘 것입니다. Express.js는 웹 애플리케이션을 만들기 위한 일련의 도구를 제공하는 Node.js 프레임워크입니다. Hapi.js 및 Koa.js와 같은 다른 Node.js 프레임워크와 함께 Kotlin을 사용할 수도 있습니다.

## 프로젝트 설정

시작하려면 Express.js 프레임워크를 사용하여 새로운 Kotlin 프로젝트를 생성해야 합니다. express-generator 도구를 사용하여 이 작업을 수행할 수 있습니다.

먼저 npm을 사용하여 도구를 설치해야 합니다.

```
npm install -g express-generator
```

다음으로 도구를 사용하여 새 프로젝트를 생성할 수 있습니다.

```
express --view=pug my-app
```

그러면 Pug 템플릿 엔진이 구성된 my-app 디렉토리에 새 프로젝트가 생성됩니다.

## 애플리케이션 실행

이제 새 프로젝트가 있으므로 프로젝트 디렉터리에서 다음 명령을 실행하여 애플리케이션을 시작할 수 있습니다.

```
npm start
```

그러면 http://localhost:3000에서 응용 프로그램이 시작됩니다. 브라우저에서 애플리케이션에 액세스할 수 있으며 기본 Express.js 시작 페이지가 표시되어야 합니다.

## 안녕하세요 세상

간단한 "Hello world" 경로를 만들어 시작하겠습니다. route/index.js 파일을 편집하면 됩니다.

먼저 Express.js 라우터를 가져와야 합니다.

```javascript
var express = require('express');
var router = express.Router();
```

다음으로 "/" 경로에 대한 새 경로를 추가할 수 있습니다.

```javascript
router.get('/', function(req, res, next) {
  res.send('Hello world');
});
```

이 경로는 브라우저에서 "/" 경로에 액세스할 때 "Hello world" 문자열을 렌더링합니다.

## 결론

이 기사에서는 Kotlin과 Express.js 프레임워크를 사용하여 웹 애플리케이션을 빌드하는 방법을 살펴보았습니다. 또한 경로를 만들고 템플릿을 렌더링하는 방법도 살펴보았습니다.

Kotlin 및 웹 개발에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [서버측 개발을 위한 Kotlin](https://kotlinlang.org/docs/reference/server-overview.html)
- [Kotlin, Spring Boot, MongoDB로 웹 앱 만들기](https://www.baeldung.com/kotlin-mongodb-spring-boot)
- [Full-Stack Kotlin: React 및 Spring Boot로 웹 애플리케이션 개발하기](https://www.baeldung.com/kotlin-react-spring-boot)