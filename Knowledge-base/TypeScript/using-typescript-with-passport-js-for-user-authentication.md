---
title: 사용자 인증을 위해 Passport.js와 함께 TypeScript 사용
description: 
published: true
date: 2023-02-10T16:17:46.989Z
tags: 
editor: markdown
dateCreated: 2023-02-10T16:17:45.293Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Using TypeScript with Passport.js for User Authentication***English** document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-passport-js-for-user-authentication)
{.links-list}


# 사용자 인증을 위해 Passport.js와 함께 TypeScript 사용

Passport.js는 Node.js를 위한 유연한 인증 미들웨어입니다. 사용자 이름과 암호, Facebook, Twitter 등을 포함한 다양한 전략을 사용하여 사용자를 인증하는 데 사용할 수 있습니다.

TypeScript는 정적 유형 검사 및 기타 기능을 추가하는 JavaScript의 상위 집합입니다. TypeScript는 대규모 애플리케이션에서 널리 사용되며 모듈, 클래스 및 인터페이스에 대한 지원으로 Passport.js 작업에 적합합니다.

이 기사에서는 Passport.js와 함께 TypeScript를 사용하여 사용자 인증 시스템을 구축하는 방법을 살펴보겠습니다. TypeScript와 Express.js로 프로젝트를 설정하는 것부터 시작하겠습니다. 그런 다음 Passport.js를 설치하고 TypeScript와 함께 사용하도록 구성합니다. 마지막으로 간단한 사용자 이름 및 암호 인증 전략을 구현하기 위해 몇 가지 TypeScript 코드를 추가합니다.

## TypeScript 프로젝트 설정

시작하려면 새 TypeScript 프로젝트를 만들어야 합니다. [Express.js](https://expressjs.com/) 웹 프레임워크와 [TypeScript Node Starter](https://github.com/ Microsoft/TypeScript-Node-Starter) 프로젝트 템플릿을 사용하겠습니다.

먼저 TypeScript 컴파일러와 Express.js 프레임워크를 설치합니다. 또한 몇 가지 다른 모듈이 필요합니다.

```
npm install -g typescript
npm install express
npm install @types/express -D
```

다음으로 TypeScript Node Starter 템플릿을 사용하여 새 프로젝트를 만듭니다.

```
npx tsc --init
```

이렇게 하면 프로젝트에 `tsconfig.json` 파일이 생성됩니다. 이 파일을 열고 다음 설정을 추가합니다.

```json
{
    "compilerOptions": {
        "target": "es6",
        "module": "commonjs",
        "outDir": "dist",
        "strict": true
    }
}
```

이 설정은 TypeScript 코드를 Express.js와 호환되는 ES6 JavaScript로 컴파일합니다. 컴파일된 코드는 `dist` 디렉토리에 출력됩니다.

## Passport.js 설치

이제 프로젝트가 설정되었으므로 Passport.js를 설치할 수 있습니다. 다음 명령을 실행합니다.

```
npm install passport
```

이렇게 하면 Passport.js 모듈이 설치되고 `package.json` 파일에 추가됩니다.

## Passport.js 구성

Passport.js는 사용자 인증을 위해 다양한 "전략"을 사용하는 모듈식 접근 방식을 사용합니다. 사용자 이름과 암호, Facebook, Twitter 등을 사용하여 인증하는 전략이 있습니다. 이 기사에서는 사용자 이름 및 비밀번호 인증 전략에 중점을 둘 것입니다.

Passport.js 전략을 사용하려면 해당 모듈을 설치해야 합니다. 사용자 이름 및 암호 전략의 경우 [passport-local](https://github.com/jaredhanson/passport-local) 모듈을 사용합니다. 다음 명령을 실행하여 설치하십시오.

```
npm install passport-local
```

모듈이 설치되면 이를 사용하도록 Passport.js를 구성해야 합니다. 우리는 이것을 `app.ts` 파일에서 할 것입니다. 먼저 `passport-local` 모듈을 가져와야 합니다.

```javascript
import passportLocal from "passport-local";
```

다음으로 'passport-local' 전략을 사용하도록 Passport.js를 구성해야 합니다. `configurePassport` 함수에서 이 작업을 수행합니다.

```javascript
function configurePassport(passport: passport.Passport) {
    passport.use(new passportLocal.Strategy());
}
```

이렇게 하면 'passport-local' 전략을 사용하도록 Passport.js가 구성됩니다. 'passport-local' 전략은 사용자 이름과 비밀번호를 사용하여 사용자를 인증합니다.

## 인증 구현

이제 Passport.js를 구성했으므로 인증 구현을 시작할 수 있습니다. 우리는 이것을 `app.ts` 파일에서 할 것입니다.

먼저 `passport-local` 모듈을 가져와야 합니다.

```javascript
import passportLocal from "passport-local";
```

다음으로 'passport-local' 전략을 사용하도록 Passport.js를 구성해야 합니다. `configurePassport` 함수에서 이 작업을 수행합니다.

```javascript
function configurePassport(passport: passport.Passport) {
    passport.use(new passportLocal.Strategy());
}
```

이렇게 하면 'passport-local' 전략을 사용하도록 Passport.js가 구성됩니다. 'passport-local' 전략은 사용자 이름과 비밀번호를 사용하여 사용자를 인증합니다.

Passport.js가 구성되면 사용자를 인증하는 코드를 작성할 수 있습니다. 우리는 이것을 `login` 함수에서 할 것입니다:

```javascript
async function login(req: express.Request, res: express.Response) {
    passport.authenticate("local", (err, user, info) => {
        if (err) {
            // Handle errors
        }

        if (!user) {
            // Redirect to login page
        }

        // Login successful, redirect to home page
    })(req, res);
}
```

이 코드는 `passport-local` 전략을 사용하여 사용자를 인증합니다. 인증에 성공하면 사용자는 홈 페이지로 리디렉션됩니다. 그렇지 않으면 로그인 페이지로 리디렉션됩니다.

## 외부 리소스

- [Passport.js 문서](http://passportjs.org/docs)
- [여권-로컬 문서](https://github.com/jaredhanson/passport-local)
- [TypeScript 설명서](https://www.typescriptlang.org/docs/handbook/basic-types.html)