---
title: TypeScript 및 Express.js에서 세션 및 쿠키 작업
description: 
published: true
date: 2023-03-02T03:32:23.952Z
tags: 
editor: markdown
dateCreated: 2023-03-02T03:32:16.940Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Working with Sessions and Cookies in TypeScript and Express.js***English** document is available*](/en/Knowledge-base/TypeScript/working-with-sessions-and-cookies-in-typescript-and-express-js)
{.links-list}



# TypeScript 및 Express.js에서 세션 및 쿠키 작업

세션과 쿠키는 웹 개발의 중요한 부분입니다. 이를 통해 사용자에 대한 데이터를 서버에 저장하고 나중에 액세스할 수 있습니다. 이 기사에서는 TypeScript 및 Express.js에서 세션 및 쿠키로 작업하는 방법을 배웁니다.

## 세션과 쿠키란 무엇입니까?

세션과 쿠키는 서버의 사용자에 대한 데이터를 저장하는 두 가지 방법입니다. 세션은 서버에 저장되고 쿠키는 사용자 컴퓨터에 저장됩니다.

쿠키는 종종 사용자의 기본 설정이나 로그인 정보와 같은 데이터를 저장하는 데 사용됩니다. 세션은 사용자의 장바구니와 같이 나중에 액세스하려는 데이터를 저장하는 데 사용됩니다.

## 쿠키 생성 및 저장 방법

쿠키를 생성하고 저장하기 위해 `cookie-parser` 미들웨어를 사용할 수 있습니다. 이 미들웨어는 요청에서 쿠키를 구문 분석하여 `req.cookies` 개체에서 사용할 수 있도록 합니다.

```javascript
var express = require('express');
var cookieParser = require('cookie-parser');

var app = express();
app.use(cookieParser());
```

`cookie-parser` 미들웨어가 설정되면 `res.cookie()` 함수를 사용하여 쿠키를 생성할 수 있습니다. 이 함수는 쿠키 이름과 쿠키 값이라는 두 가지 인수를 사용합니다.

```javascript
res.cookie('name', 'value');
```

## 쿠키를 읽는 방법

`cookie-parser` 미들웨어를 설정하면 `req.cookies` 개체를 사용하여 쿠키를 읽을 수 있습니다. 예를 들어 이름이 `name`인 쿠키가 있으면 다음과 같이 읽을 수 있습니다.

```javascript
var name = req.cookies.name;
```

## 쿠키를 삭제하는 방법

쿠키를 삭제하려면 `res.clearCookie()` 함수를 사용할 수 있습니다. 이 함수는 쿠키 이름을 인수로 사용합니다.

```javascript
res.clearCookie('name');
```

## 세션 생성 및 저장 방법

세션을 생성하고 저장하기 위해 `express-session` 미들웨어를 사용할 수 있습니다. 이 미들웨어는 세션 데이터를 서버에 저장합니다.

```javascript
var express = require('express');
var session = require('express-session');

var app = express();
app.use(session({
  secret: 'secret',
  resave: false,
  saveUninitialized: true
}));
```

`express-session` 미들웨어가 설정되면 `req.session` 객체를 사용하여 세션을 생성할 수 있습니다. 이 개체에는 세션 데이터를 설정하는 데 사용할 수 있는 `.set()` 함수가 있습니다. `.set()` 함수는 세션 이름과 세션 값이라는 두 가지 인수를 사용합니다.

```javascript
req.session.set('name', 'value');
```

## 세션을 읽는 방법

세션을 읽으려면 `req.session` 개체를 사용할 수 있습니다. 이 개체에는 세션 데이터를 가져오는 데 사용할 수 있는 `.get()` 함수가 있습니다. `.get()` 함수는 세션 이름을 인수로 사용합니다.

```javascript
var name = req.session.get('name');
```

## 세션 삭제 방법

세션을 삭제하려면 `req.session.destroy()` 함수를 사용할 수 있습니다. 이 기능은 세션을 파괴하고 모든 세션 데이터를 제거합니다.

```javascript
req.session.destroy();
```

## 결론

이 기사에서는 TypeScript 및 Express.js에서 세션 및 쿠키로 작업하는 방법을 배웠습니다. 쿠키와 세션을 만들고 읽고 삭제하는 방법을 살펴보았습니다.