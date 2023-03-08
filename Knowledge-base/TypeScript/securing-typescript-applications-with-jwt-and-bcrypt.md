---
title: JWT 및 Bcrypt로 TypeScript 애플리케이션 보호
description: 
published: true
date: 2023-02-07T18:18:08.515Z
tags: 
editor: markdown
dateCreated: 2023-02-07T18:18:06.775Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Securing TypeScript Applications with JWT and Bcrypt***English** document is available*](/en/Knowledge-base/TypeScript/securing-typescript-applications-with-jwt-and-bcrypt)
{.links-list}


# JWT 및 Bcrypt로 TypeScript 애플리케이션 보호

웹 애플리케이션에서 보안의 중요성은 아무리 강조해도 지나치지 않습니다. 이 기사에서는 JWT(JSON Web Tokens)와 bcrypt라는 TypeScript 애플리케이션 보안을 위한 두 가지 인기 있는 방법을 살펴보겠습니다. 이러한 각 기술을 사용하여 TypeScript 애플리케이션을 보호하는 방법을 살펴보고 각 접근 방식과 관련된 몇 가지 잠재적 위험에 대해서도 알아봅니다.

## JSON 웹 토큰(JWT)이란?

JWT(JSON Web Token)는 두 당사자 간에 데이터를 안전하게 전송하는 널리 사용되는 방법입니다. JWT는 세 부분으로 구성됩니다.

- **헤더**: 여기에는 JWT 서명을 생성하는 데 사용되는 알고리즘과 JWT 유형(일반적으로 "JWT")이 포함됩니다.
- **Payload**: 전송할 데이터를 담고 있습니다. 이 데이터는 일반적으로 Base64를 사용하여 인코딩됩니다.
- **서명**: 페이로드의 데이터가 변조되지 않았음을 확인하기 위해 사용됩니다. 서명은 헤더와 페이로드, 비밀 키를 사용하여 생성됩니다.

JWT의 일반적인 사용 사례 중 하나는 웹 애플리케이션과 백엔드 서버 간에 인증된 사용자에 대한 정보를 전송하는 것입니다. 예를 들어 사용자가 웹 애플리케이션에 로그인하면 JWT를 사용하여 사용자에 대한 정보(예: 사용자 이름 및 이메일 주소)를 백엔드 서버로 전송할 수 있습니다. 그런 다음 백엔드 서버는 이 정보를 사용하여 사용자에게 맞는 응답을 생성할 수 있습니다.

JWT의 또 다른 일반적인 사용 사례는 웹 애플리케이션에서 백엔드 서버로 사용자 세션에 대한 정보를 전송하는 것입니다. 이것은 쿠키에 민감한 정보(예: 사용자의 세션 ID)를 저장하지 않기 위해 종종 수행됩니다. 사용자 세션이 만료되면 JWT를 사용하여 백엔드 서버에서 사용자 세션을 무효화할 수 있습니다.

## 비크립트란?

Bcrypt는 계산 비용이 많이 드는 암호 해싱 기능입니다. 이것은 공격자가 암호를 무차별 대입하는 것을 어렵게 만들기 때문에 중요합니다.

Bcrypt는 일반적으로 솔트와 함께 사용됩니다. 솔트는 암호 해싱 함수를 계산하기 더 어렵게 만드는 데 사용되는 임의로 생성된 문자열입니다. 소금은 일반적으로 해시된 암호와 함께 저장됩니다.

## JWT를 사용하여 TypeScript 애플리케이션을 보호하는 방법은 무엇입니까?

TypeScript 애플리케이션에서 JWT를 사용하는 가장 일반적인 방법은 [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken) 패키지를 사용하는 것입니다. 이 패키지는 JWT를 쉽게 생성하고 확인할 수 있도록 도와주는 일련의 도우미 기능을 제공합니다.

jsonwebtoken을 사용하려면 먼저 설치해야 합니다.

```
npm install jsonwebtoken
```

jsonwebtoken이 설치되면 이를 사용하여 JWT를 생성할 수 있습니다.

```javascript
const jwt = require('jsonwebtoken');

const payload = {
  userId: 123,
  email: 'user@example.com',
  name: 'John Doe',
};

const secret = 'secret';

const token = jwt.sign(payload, secret);
```

`jwt.sign()` 함수는 페이로드와 비밀의 두 가지 인수를 사용합니다. 페이로드는 JWT에서 인코딩하려는 데이터이며 암호는 JWT 서명을 생성하는 데 사용됩니다.

JWT를 생성하면 백엔드 서버로 전송할 수 있습니다. 그런 다음 백엔드 서버는 `jwt.verify()` 함수를 사용하여 JWT를 확인할 수 있습니다.

```javascript
const jwt = require('jsonwebtoken');

const token = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEyMywiZW1haWwiOiJ1c2VyQGV4YW1wbGUuY29tIiwibmFtZSI6IkpvaG4gRG9lIn0.S30gaSmqhzPZU6mxPiwm53cH-j2dhYfBYuYTR3LsyiE';

const secret = 'secret';

const payload = jwt.verify(token, secret);
```

`jwt.verify()` 함수는 토큰과 비밀의 두 가지 인수를 사용합니다. 토큰은 확인하려는 JWT이고 암호는 JWT 서명을 확인하는 데 사용됩니다.

JWT가 유효한 경우 `jwt.verify()` 함수는 디코딩된 페이로드를 반환합니다. JWT가 유효하지 않으면 `jwt.verify()` 함수에서 오류가 발생합니다.

## bcrypt를 사용하여 TypeScript 애플리케이션을 보호하는 방법은 무엇입니까?

TypeScript 애플리케이션에서 bcrypt를 사용하는 가장 일반적인 방법은 [bcryptjs](https://www.npmjs.com/package/bcryptjs) 패키지를 사용하는 것입니다. 이 패키지는 bcrypt 해시를 쉽게 생성하고 확인할 수 있는 일련의 도우미 기능을 제공합니다.

bcryptjs를 사용하려면 먼저 설치해야 합니다.

```
npm install bcryptjs
```

bcryptjs가 설치되면 이를 사용하여 암호를 해시할 수 있습니다.

```javascript
const bcrypt = require('bcryptjs');

const password = 'secret';

const salt = bcrypt.genSaltSync(10);

const hash = bcrypt.hashSync(password, salt);
```

`bcrypt.hashSync()` 함수는 암호와 소금의 두 가지 인수를 사용합니다. 암호는 우리가 해시하려는 암호이며 소금은 암호 해싱 기능을 계산하기 더 어렵게 만드는 데 사용됩니다.

해시를 생성하면 백엔드 서버로 전송할 수 있습니다. 그러면 백엔드 서버는 `bcrypt.compareSync()` 함수를 사용하여 해시와 암호를 비교할 수 있습니다.

```javascript
const bcrypt = require('bcryptjs');

const password = 'secret';

const hash = '$2a$10$2znyB6.qE1T.1S7X3C5NU.7bHJNz5KUzHJZzM6DQLN8tm4Gxe6Ay';

bcrypt.compareSync(password, hash); // true
```

`bcrypt.compareSync()` 함수는 암호와 해시라는 두 가지 인수를 사용합니다. 암호는 비교하려는 암호이고 해시는 비교하려는 bcrypt 해시입니다.

암호가 유효하면 `bcrypt.compareSync()` 함수는 `true`를 반환합니다. 암호가 유효하지 않으면 `bcrypt.compareSync()` 함수는 `false`를 반환합니다.

## JWT와 관련된 잠재적 위험은 무엇입니까?

JWT와 관련된 한 가지 잠재적 위험은 페이로드의 데이터가 암호화되지 않는다는 것입니다. 즉, 공격자가 JWT를 획득하면 페이로드의 데이터를 볼 수 있습니다.

JWT와 관련된 또 다른 잠재적 함정은 JWT 서명을 생성하는 데 사용되는 비밀이 비밀로 유지되어야 한다는 것입니다. 비밀이 손상되면 공격자는 자신이 선택한 데이터로 자체 JWT를 생성할 수 있습니다.

## bcrypt와 관련된 잠재적 위험은 무엇입니까?

bcrypt와 관련된 한 가지 잠재적 함정은 그것이 단방향 해싱 함수라는 것입니다. 즉, 일단 암호가 해시되면 되돌릴 수 없습니다. 이로 인해 암호를 잊어버린 경우 암호를 복구하기 어려울 수 있습니다.

bcrypt와 관련된 또 다른 잠재적 함정은 계산 비용이 많이 든다는 것입니다. 이로 인해 대규모 데이터 세트에서 bcrypt를 사용하기 어려울 수 있습니다.

## 외부 리소스

- [JSON 웹 토큰](https://jwt.io/)
- [Bcrypt](https://en.wikipedia.org/wiki/Bcrypt)
- [JWT(JSON 웹 토큰)를 사용하여 TypeScript 애플리케이션에서 사용자를 인증하는 방법](https://auth0.com/blog/how-to-use-jwts-to-authenticate-users-in-a-typescript- 애플리케이션/)
- [Bcrypt로 TypeScript 애플리케이션을 보호하는 방법](https://www.sitepoint.com/secure-typescript-application-bcrypt/)