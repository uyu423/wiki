---
title: 011: Nest.js에서 인증 구현
description: 
published: true
date: 2023-02-14T21:32:53.955Z
tags: 
editor: markdown
dateCreated: 2023-02-14T21:32:46.273Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [011: Implementing authentication in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/011-implementing-authentication-in-nest-js)
{.links-list}


# Nest.js에서 인증 구현

Nest.js는 Node.js 애플리케이션을 구축하기 위한 프레임워크입니다. TypeScript를 사용하며 Angular의 영향을 받습니다. Nest.js는 사용 및 유지 관리가 쉬운 코드를 구조화하는 방법을 제공합니다.

인증은 사용자의 신원을 확인하는 프로세스입니다. Nest.js는 애플리케이션에서 인증을 구현하는 방법을 제공합니다. 이 게시물에서는 Nest.js 애플리케이션에서 인증을 구현하는 방법을 배웁니다.

## 인증이란?

인증은 사용자의 ID를 확인하는 프로세스입니다. 무단 액세스로부터 리소스를 보호하는 데 사용됩니다. 인증은 일반적으로 사용자에게 사용자 이름과 암호를 제공하도록 요청하여 수행됩니다. 그런 다음 사용자 이름과 암호는 인증된 사용자 데이터베이스에 대해 확인됩니다.

## Nest.js가 무엇인가요?

Nest.js는 Node.js 애플리케이션을 구축하기 위한 프레임워크입니다. TypeScript를 사용하며 Angular의 영향을 받습니다. Nest.js는 사용 및 유지 관리가 쉬운 코드를 구조화하는 방법을 제공합니다.

## Nest.js를 사용하면 어떤 이점이 있나요?

Nest.js를 사용하면 다음과 같은 많은 이점이 있습니다.

- Nest.js는 사용 및 유지 관리가 쉬운 코드를 구조화하는 방법을 제공합니다.
- Nest.js는 배우고 사용하기 쉽습니다.
- Nest.js는 JavaScript의 상위 집합인 TypeScript를 기반으로 합니다. 이것은 Nest.js 코드가 읽고 이해하기 쉽다는 것을 의미합니다.
- Nest.js는 Angular의 영향을 받습니다. 이것은 Angular에 익숙한 사람들이 Nest.js 코드를 읽고 이해하기 쉽다는 것을 의미합니다.

## 타입스크립트란?

TypeScript는 JavaScript의 상위 집합입니다. 이것은 TypeScript 코드가 읽고 이해하기 쉽다는 것을 의미합니다. TypeScript도 유형이 지정되어 컴파일 시간에 오류를 포착할 수 있습니다. 이것은 TypeScript 코드를 더 안정적으로 만듭니다.

## JavaScript와 TypeScript의 차이점은 무엇인가요?

JavaScript와 TypeScript의 차이점은 TypeScript는 입력되고 JavaScript는 입력되지 않는다는 것입니다. 이는 TypeScript가 컴파일 타임에 오류를 포착할 수 있음을 의미합니다. 이것은 TypeScript 코드를 더 안정적으로 만듭니다.

## Node.js와 Nest.js의 차이점은 무엇인가요?

Node.js와 Nest.js의 차이점은 Nest.js가 Node.js 위에 구축된다는 것입니다. Nest.js는 사용 및 유지 관리가 쉬운 코드를 구조화하는 방법을 제공합니다.

## Nest.js는 어떻게 설치하나요?

Nest.js는 Node.js 패키지 관리자(npm)를 사용하여 설치할 수 있습니다. Nest.js를 설치하려면 터미널을 열고 다음 명령을 실행합니다.

```
npm install -g @nestjs/cli
```

## Nest.js 프로젝트는 어떻게 생성하나요?

Nest.js 프로젝트를 만들려면 터미널을 열고 다음 명령을 실행합니다.

```
nest new project-name
```

프로젝트 이름을 프로젝트 이름으로 바꿉니다. 이렇게 하면 project-name이라는 이름으로 새 Nest.js 프로젝트가 생성됩니다.

## Nest.js 프로젝트를 어떻게 실행하나요?

Nest.js 프로젝트를 실행하려면 터미널을 열고 프로젝트 디렉터리로 이동합니다. 그런 다음 다음 명령을 실행합니다.

```
nest start
```

그러면 Nest.js 서버가 시작됩니다. 서버는 http://localhost:3000에서 액세스할 수 있습니다.

## Nest.js에서 인증을 구현하는 단계는 무엇인가요?

Nest.js에서 인증을 구현하는 방법에는 여러 가지가 있습니다. 이 게시물에서는 Passport.js 라이브러리를 사용하여 인증을 구현합니다. Passport.js는 Node.js용으로 널리 사용되는 인증 라이브러리입니다.

Nest.js에서 인증을 구현하는 단계는 다음과 같습니다.

1. Passport.js 라이브러리를 설치합니다.
2. Passport.js를 구성합니다.
3. 로그인 페이지를 생성합니다.
4. 로그아웃 페이지를 생성합니다.
5. 인증으로 리소스를 보호합니다.

## 1단계: Passport.js 라이브러리 설치

첫 번째 단계는 Passport.js 라이브러리를 설치하는 것입니다. Passport.js는 Node.js용으로 널리 사용되는 인증 라이브러리입니다. Passport.js 라이브러리를 설치하려면 터미널을 열고 다음 명령을 실행합니다.

```
npm install passport
```

## 2단계: Passport.js 구성

다음 단계는 Passport.js를 구성하는 것입니다. Passport.js는 사용자의 신원을 확인하는 방법을 알아야 합니다. 이것은 전략을 제공함으로써 이루어집니다. Passport.js와 함께 사용할 수 있는 많은 전략이 있습니다. 이 게시물에서는 LocalStrategy를 사용합니다.

LocalStrategy는 사용자 이름과 암호를 사용하여 사용자의 신원을 확인하는 전략입니다. LocalStrategy를 사용하려면 콜백 함수를 제공해야 합니다. 이 콜백 함수는 Passport.js가 사용자의 신원을 확인해야 할 때 호출됩니다.

LocalStrategy 콜백 함수에는 다음 서명이 있습니다.

```
function(username, password, done) {

}
```

username 및 password 인수는 사용자가 제공한 사용자 이름 및 비밀번호입니다. 완료 콜백은 확인 결과를 반환하는 데 사용되는 함수입니다. 완료 콜백에는 다음 서명이 있습니다.

```
function(error, user, info) {

}
```

확인에 성공하면 사용자 인수에 사용자 개체가 포함됩니다. 확인에 실패하면 error 및 info 인수에 오류에 대한 정보가 포함됩니다.

LocalStrategy를 구성하려면 프로젝트 루트 디렉터리에 passport.js라는 파일을 만들어야 합니다. passport.js 파일은 다음과 같아야 합니다.

```javascript
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;

passport.use(new LocalStrategy(
  function(username, password, done) {
    //Verify the username and password here
  }
));
```

//Verify the username and password here 주석을 사용자 이름과 비밀번호를 확인하는 코드로 바꿉니다.

## 3단계: 로그인 페이지 만들기

다음 단계는 로그인 페이지를 만드는 것입니다. 로그인 페이지는 양식이 포함된 HTML 페이지입니다. 양식에는 사용자 이름과 암호에 대한 필드가 있습니다. 양식은 /login 경로에 제출됩니다.

로그인 페이지를 만들려면 프로젝트 루트 디렉터리에 login.html이라는 파일을 만듭니다. login.html 파일은 다음과 같아야 합니다.

```html
<html>
<body>
  <form action="/login" method="post">
    <label>Username:</label>
    <input type="text" name="username">
    <label>Password:</label>
    <input type="password" name="password">
    <input type="submit" value="Login">
  </form>
</body>
</html>
```

## 4단계: 로그아웃 페이지 만들기

다음 단계는 로그아웃 페이지를 만드는 것입니다. 로그아웃 페이지는 양식이 포함된 HTML 페이지입니다. 양식에는 사용자 이름 필드가 있습니다. 양식은 /logout 경로에 제출됩니다.

로그아웃 페이지를 생성하려면 프로젝트 루트 디렉터리에 logout.html이라는 파일을 생성합니다. logout.html 파일은 다음과 같아야 합니다.

```html
<html>
<body>
  <form action="/logout" method="post">
    <label>Username:</label>
    <input type="text" name="username">
    <input type="submit" value="Logout">
  </form>
</body>
</html>
```

## 5단계: 인증으로 리소스 보호

마지막 단계는 인증을 통해 리소스를 보호하는 것입니다. 이를 위해서는 사용자가 인증되었는지 확인하는 미들웨어 기능을 만들어야 합니다. 사용자가 인증되지 않은 경우 미들웨어 기능은 사용자를 로그인 페이지로 리디렉션합니다.

미들웨어 기능을 생성하려면 프로젝트 루트 디렉터리에 auth.js라는 파일을 생성합니다. auth.js 파일은 다음과 같아야 합니다.

```javascript
const passport = require('passport');

function isAuthenticated(req, res, next) {
  if (req.isAuthenticated()) {
    return next();
  }
  res.redirect('/login');
}

module.exports = {
  isAuthenticated: isAuthenticated
};
```

isAuthenticated() 함수는 미들웨어 함수입니다. 이 함수는 사용자가 인증되었는지 확인합니다. 사용자가 인증되지 않은 경우 함수는 사용자를 /login 페이지로 리디렉션합니다.

미들웨어 기능을 사용하여 모든 경로를 보호할 수 있습니다. 예를 들어 /admin 경로를 보호하기 위해 다음 코드를 사용할 수 있습니다.

```javascript
app.get('/admin', auth.isAuthenticated, (req, res) => {
  // The authenticated user can access this route
});
```

## 결론

이 게시물에서는 Nest.js 애플리케이션에서 인증을 구현하는 방법을 배웠습니다. Passport.js 라이브러리를 설치하고 LocalStrategy를 사용하도록 구성했습니다. 로그인 페이지와 로그아웃 페이지도 만들었습니다. 마지막으로 인증을 통해 리소스를 보호했습니다.