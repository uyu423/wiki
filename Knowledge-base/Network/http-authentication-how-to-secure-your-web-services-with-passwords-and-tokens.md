---
title: HTTP 인증: 비밀번호와 토큰으로 웹 서비스를 보호하는 방법
description: 
published: true
date: 2023-03-06T20:33:15.462Z
tags: 
editor: markdown
dateCreated: 2023-03-06T20:33:14.057Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [HTTP Authentication: How to Secure Your Web Services with Passwords and Tokens***English** document is available*](/en/Knowledge-base/Network/http-authentication-how-to-secure-your-web-services-with-passwords-and-tokens)
{.links-list}



HTTP 인증: 비밀번호와 토큰으로 웹 서비스를 보호하는 방법

웹 서비스와 API가 점점 보편화됨에 따라 보안 인증 메커니즘에 대한 필요성이 증가하고 있습니다. HTTP 인증은 개발자가 보호된 리소스에 대한 액세스를 허용하기 전에 사용자가 본인이 맞는지 확인할 수 있는 메커니즘 중 하나입니다. 이 기사에서는 다양한 유형의 HTTP 인증과 이를 웹 서비스에서 구현하는 방법을 살펴봅니다.

## HTTP 인증이란 무엇입니까?

HTTP 인증은 사용자가 웹 서버에 자신을 인증하는 방법을 제공하는 데 사용되는 메커니즘입니다. 이를 통해 웹 서비스는 제공된 자격 증명을 기반으로 보호된 리소스에 대한 액세스를 허용하거나 거부할 수 있습니다.

## HTTP 인증 유형

### 기본 인증

기본 인증은 HTTP 인증의 가장 단순한 형태입니다. 각 요청의 헤더에 사용자 이름과 암호를 보내야 합니다.

```
Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==
```

위의 예에서 사용자 이름은 "Aladdin"이고 암호는 "open sesame"입니다. 문자열 "QWxhZGRpbjpvcGVuIHNlc2FtZQ=="는 "Aladdin:open sesame"의 Base64 인코딩입니다.

### 다이제스트 인증

다이제스트 인증은 기본 인증보다 개선된 것입니다. 챌린지-응답 메커니즘을 사용하여 사용자를 인증하며 일반 텍스트로 암호를 보내는 것보다 더 안전합니다.

```
Authorization: Digest username="Aladdin",
                          realm="example.com",
                          nonce="dcd98b7102dd2f0e8b11d0f600bfb0c093",
                          uri="/dir/index.html",
                          qop=auth,
                          nc=00000001,
                          cnonce="0a4f113b",
                          response="6629fae49393a05397450978507c4ef1",
                          opaque="5ccc069c403ebaf9f0171e9517f40e41"
```

위의 예에서 "Aladdin"은 사용자 이름이고 "example.com"은 영역입니다. 서버는 고유한 문자열인 nonce를 생성하여 클라이언트로 다시 보냅니다. 그런 다음 클라이언트는 nonce를 사용하여 서버로 다시 전송되는 응답을 생성합니다. 응답에는 nonce 및 요청 URI와 같은 다른 값과 연결된 암호의 해시가 포함됩니다.

### 토큰 기반 인증

토큰 기반 인증은 HTTP 인증에 대한 대중적인 대안입니다. 클라이언트는 각 요청과 함께 사용자 이름과 암호를 보내는 대신 토큰을 보냅니다. 그런 다음 서버는 토큰을 확인하고 유효한 경우 액세스 권한을 부여합니다.

```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

위의 예에서 토큰은 ID 및 이름과 같은 사용자에 대한 정보를 포함하는 JWT(JSON Web Token)입니다. 토큰은 서버의 비밀 키로 서명되며 클라이언트는 각 요청의 헤더에 토큰을 포함합니다. 서버는 서명을 확인하고 토큰이 유효한 경우 액세스 권한을 부여합니다.

## HTTP 인증 구현

### 기본 인증

웹 서비스에서 기본 인증을 구현하려면 HTTP 서버 모듈 또는 미들웨어를 사용할 수 있습니다. Node.js에서는 [basic-auth](https://www.npmjs.com/package/basic-auth) 미들웨어를 사용할 수 있습니다.

```javascript
const auth = require('basic-auth');

function authenticate(req, res, next) {
  const user = auth(req);

  if (!user || user.name !== 'username' || user.pass !== 'password') {
    res.statusCode = 401;
    res.setHeader('WWW-Authenticate', 'Basic realm="Secure Area"');
    res.end('Unauthorized');
  } else {
    next();
  }
}

app.get('/protected-resource', authenticate, function(req, res) {
  res.send('Protected Resource');
});
```

위의 예에서는 요청 헤더에 전송된 사용자 이름과 비밀번호를 확인하는 `authenticate` 함수를 정의합니다. 자격 증명이 올바르지 않으면 'WWW-Authenticate' 헤더와 함께 401 응답을 보냅니다. 자격 증명이 정확하면 `next()` 미들웨어 함수를 호출하여 요청 처리를 계속합니다.

### 다이제스트 인증

다이제스트 인증을 구현하려면 HTTP 서버 모듈 또는 미들웨어를 사용할 수 있습니다. Node.js에서는 [digest-authentication](https://www.npmjs.com/package/digest-authentication) 미들웨어를 사용할 수 있습니다.

```javascript
const digest = require('digest-authentication');

function authenticate(req, res, next) {
  const realm = 'example.com';
  const users = {'Aladdin': 'open sesame'};
  const credentials = digest.parse(req.headers.authorization);

  if (!credentials) {
    digest.challenge(res, realm);
  } else if (!users[credentials.username] || users[credentials.username] !== credentials.password) {
    res.statusCode = 401;
    res.end('Unauthorized');
  } else {
    const ha1 = digest.generateHA1(credentials.username, realm, credentials.password);
    const ha2 = digest.generateHA2(req.method, credentials.uri);
    const response = digest.generateResponse(ha1, credentials.nonce, credentials.nc, credentials.cnonce, credentials.qop, ha2);
    const opaque = digest.generateOpaque();

    res.setHeader('Authentication-Info', `nextnonce="${digest.generateNonce()}", qop=${credentials.qop}, rspauth="${response}"`);
    res.setHeader('Opaque', opaque);
    res.end('Authorized');
  }
}

app.get('/protected-resource', authenticate, function(req, res) {
  res.send('Protected Resource');
});
```

위의 예에서는 요청 헤더에서 전송된 자격 증명을 확인하는 `authenticate` 함수를 정의합니다. 자격 증명이 올바르지 않으면 401 응답을 보냅니다. 자격 증명이 정확하면 `generateHA1`, `generateHA2` 및 `generateResponse` 기능을 사용하여 응답 문자열을 생성합니다. 그런 다음 `Authentication-Info` 및 `Opaque` 헤더를 설정하고 `next()` 미들웨어 함수를 호출하여 요청 처리를 계속합니다.

### 토큰 기반 인증

토큰 기반 인증을 구현하려면 JWT(JSON Web Token) 라이브러리를 사용할 수 있습니다. Node.js에서는 [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken) 라이브러리를 사용할 수 있습니다.

```javascript
const jwt = require('jsonwebtoken');

app.post('/login', function(req, res) {
  const { username, password } = req.body;

  if (username !== 'username' || password !== 'password') {
    res.statusCode = 401;
    res.end('Unauthorized');
  } else {
    const token = jwt.sign({ sub: '1234567890', name: 'John Doe' }, 'secretkey');
    res.json({ token });
  }
});

function authenticate(req, res, next) {
  const token = req.headers.authorization.split(' ')[1];

  jwt.verify(token, 'secretkey', function(err, decoded) {
    if (err) {
      res.statusCode = 401;
      res.end('Unauthorized');
    } else {
      req.user = decoded;
      next();
    }
  });
}

app.get('/protected-resource', authenticate, function(req, res) {
  res.send('Protected Resource');
});
```

위의 예에서는 요청 본문에 전송된 사용자 이름과 비밀번호를 확인하는 `/login` 경로를 정의합니다. 자격 증명이 정확하면 `sign` 함수를 사용하여 JWT를 생성하고 JSON 응답으로 클라이언트에 다시 보냅니다.

또한 요청 헤더에서 전송된 JWT를 확인하는 `authenticate` 함수를 정의합니다. JWT가 유효하지 않으면 401 응답을 보냅니다. JWT가 유효하면 `req.user` 객체를 디코딩된 JWT 페이로드로 설정하고 `next()` 미들웨어 함수를 호출하여 요청 처리를 계속합니다.

## 결론

HTTP 인증은 웹 서비스 및 API를 보호하기 위한 강력한 메커니즘입니다. 다양한 유형의 HTTP 인증과 이를 구현하는 방법을 이해함으로써 개발자는 사용자의 데이터를 안전하게 보호할 수 있습니다.

## 외부 리소스

- [MDN 웹 문서 - HTTP 인증](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication)
- [JWT.io - JSON 웹 토큰](https://jwt.io/)
- [npm - 기본 인증](https://www.npmjs.com/package/basic-auth)
- [npm - 다이제스트-인증](https://www.npmjs.com/package/digest-authentication)
- [npm - jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken)