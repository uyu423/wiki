---
title: HTTP Authentication: How to Secure Your Web Services with Passwords and Tokens
description: 
published: true
date: 2023-03-06T20:33:21.585Z
tags: 
editor: markdown
dateCreated: 2023-03-06T20:33:14.060Z
---

- [HTTP 인증: 비밀번호와 토큰으로 웹 서비스를 보호하는 방법***Korean** document is available*](/ko/Knowledge-base/Network/http-authentication-how-to-secure-your-web-services-with-passwords-and-tokens)
{.links-list}



HTTP Authentication: How to Secure Your Web Services with Passwords and Tokens

As web services and APIs become more common, the need for secure authentication mechanisms increases. HTTP Authentication is one such mechanism that allows developers to ensure that users are who they claim to be before allowing access to protected resources. In this article, we'll explore the different types of HTTP Authentication and how to implement them in your web services. 

## What is HTTP Authentication?

HTTP Authentication is a mechanism used to provide a way for users to authenticate themselves to web servers. It allows web services to grant or deny access to protected resources based on the provided credentials. 

## Types of HTTP Authentication

### Basic Authentication

Basic Authentication is the simplest form of HTTP Authentication. It requires a username and password to be sent in the header of each request. 

```
Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==
```

In the above example, the username is "Aladdin" and the password is "open sesame". The string "QWxhZGRpbjpvcGVuIHNlc2FtZQ==" is the Base64 encoding of "Aladdin:open sesame".

### Digest Authentication

Digest Authentication is an improvement over Basic Authentication. It uses a challenge-response mechanism to authenticate users, which is more secure than sending the password in plaintext. 

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

In the above example, "Aladdin" is the username and "example.com" is the realm. The server generates a nonce, which is a unique string, and sends it back to the client. The client then uses the nonce to create a response that is sent back to the server. The response includes a hash of the password concatenated with other values, such as the nonce and the request URI. 

### Token-Based Authentication

Token-Based Authentication is a popular alternative to HTTP Authentication. Instead of sending a username and password with each request, the client sends a token. The server then verifies the token and grants access if it is valid. 

```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

In the above example, the token is a JSON Web Token (JWT) that contains information about the user, such as their ID and name. The token is signed with a secret key on the server, and the client includes the token in the header of each request. The server verifies the signature and grants access if the token is valid. 

## Implementing HTTP Authentication

### Basic Authentication

To implement Basic Authentication in your web service, you can use an HTTP server module or middleware. In Node.js, you can use the [basic-auth](https://www.npmjs.com/package/basic-auth) middleware. 

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

In the above example, we define an `authenticate` function that checks the username and password sent in the request header. If the credentials are incorrect, we send a 401 response with a `WWW-Authenticate` header. If the credentials are correct, we call the `next()` middleware function to continue processing the request. 

### Digest Authentication

To implement Digest Authentication, you can use an HTTP server module or middleware. In Node.js, you can use the [digest-authentication](https://www.npmjs.com/package/digest-authentication) middleware. 

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

In the above example, we define an `authenticate` function that checks the credentials sent in the request header. If the credentials are incorrect, we send a 401 response. If the credentials are correct, we generate a response string using the `generateHA1`, `generateHA2`, and `generateResponse` functions. We then set the `Authentication-Info` and `Opaque` headers and call the `next()` middleware function to continue processing the request. 

### Token-Based Authentication

To implement Token-Based Authentication, you can use a JSON Web Token (JWT) library. In Node.js, you can use the [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken) library. 

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

In the above example, we define a `/login` route that checks the username and password sent in the request body. If the credentials are correct, we generate a JWT using the `sign` function and send it back to the client in a JSON response. 

We also define an `authenticate` function that checks the JWT sent in the request header. If the JWT is invalid, we send a 401 response. If the JWT is valid, we set the `req.user` object to the decoded JWT payload and call the `next()` middleware function to continue processing the request. 

## Conclusion

HTTP Authentication is a powerful mechanism for securing web services and APIs. By understanding the different types of HTTP Authentication and how to implement them, developers can ensure that their users' data is safe and secure. 

## External Resources

- [MDN Web Docs - HTTP authentication](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication)
- [JWT.io - JSON Web Tokens](https://jwt.io/)
- [npm - basic-auth](https://www.npmjs.com/package/basic-auth)
- [npm - digest-authentication](https://www.npmjs.com/package/digest-authentication)
- [npm - jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken)