---
title: 使用 JWT 和 Bcrypt 保护 TypeScript 应用程序
description: 
published: true
date: 2023-02-07T18:18:08.526Z
tags: 
editor: markdown
dateCreated: 2023-02-07T18:18:06.778Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Securing TypeScript Applications with JWT and Bcrypt***English** document is available*](/en/Knowledge-base/TypeScript/securing-typescript-applications-with-jwt-and-bcrypt)
{.links-list}


# 使用 JWT 和 Bcrypt 保护 TypeScript 应用程序

不能低估安全在 Web 应用程序中的重要性。在本文中，我们将探索两种流行的保护 TypeScript 应用程序的方法：JSON Web Tokens (JWT) 和 bcrypt。我们将看到如何使用这些技术中的每一种来保护 TypeScript 应用程序，我们还将了解与每种方法相关的一些潜在陷阱。

## 什么是 JSON Web 令牌 (JWT)？

JSON Web Token (JWT) 是一种在双方之间安全传输数据的流行方式。 JWT由三部分组成：

- **Header**：这包含用于生成 JWT 签名的算法，以及 JWT 的类型（通常为“JWT”）。
- **有效载荷**：这包含要传输的数据。此数据通常使用 Base64 编码。
- **签名**：用于验证有效负载中的数据未被篡改。签名是使用标头和有效负载以及密钥生成的。

JWT 的一个常见用例是在 Web 应用程序和后端服务器之间传输有关经过身份验证的用户的信息。例如，当用户登录Web应用程序时，可以使用JWT将有关用户的信息（例如用户的姓名和电子邮件地址）传输到后端服务器。然后后端服务器可以使用此信息生成为用户定制的响应。

JWT 的另一个常见用例是将有关用户会话的信息从 Web 应用程序传输到后端服务器。通常这样做是为了避免在 cookie 中存储敏感信息（例如用户的会话 ID）。当用户会话过期时，JWT 可用于在后端服务器上使用户会话失效。

## 什么是 bcrypt？

Bcrypt 是一种密码散列函数，其设计计算成本很高。这很重要，因为它使攻击者很难暴力破解密码。

Bcrypt 通常与盐一起使用。盐是随机生成的字符串，用于使密码哈希函数更难计算。盐通常与散列密码一起存储。

## 如何使用 JWT 来保护 TypeScript 应用程序？

在 TypeScript 应用程序中使用 JWT 的最常见方法是使用 [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken) 包。这个包提供了一组帮助函数，可以很容易地生成和验证 JWT。

要使用jsonwebtoken，我们首先需要安装它：

```
npm install jsonwebtoken
```

安装 jsonwebtoken 后，我们可以使用它来生成 JWT：

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

`jwt.sign()` 函数有两个参数：有效载荷和秘密。 payload是我们要在JWT中编码的数据，secret是用来生成JWT签名的。

生成 JWT 后，我们可以将其传输到后端服务器。然后后端服务器可以使用 `jwt.verify()` 函数来验证 JWT：

```javascript
const jwt = require('jsonwebtoken');

const token = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEyMywiZW1haWwiOiJ1c2VyQGV4YW1wbGUuY29tIiwibmFtZSI6IkpvaG4gRG9lIn0.S30gaSmqhzPZU6mxPiwm53cH-j2dhYfBYuYTR3LsyiE';

const secret = 'secret';

const payload = jwt.verify(token, secret);
```

`jwt.verify()` 函数有两个参数：token 和 secret。 token就是我们要验证的JWT，secret是用来验证JWT签名的。

如果 JWT 有效，`jwt.verify()` 函数将返回解码后的负载。如果 JWT 无效，`jwt.verify()` 函数将抛出错误。

## 如何使用 bcrypt 来保护 TypeScript 应用程序？

在 TypeScript 应用程序中使用 bcrypt 的最常见方法是使用 [bcryptjs](https://www.npmjs.com/package/bcryptjs) 包。这个包提供了一组帮助函数，可以很容易地生成和验证 bcrypt 哈希。

要使用 bcryptjs，我们首先需要安装它：

```
npm install bcryptjs
```

安装 bcryptjs 后，我们可以使用它来散列密码：

```javascript
const bcrypt = require('bcryptjs');

const password = 'secret';

const salt = bcrypt.genSaltSync(10);

const hash = bcrypt.hashSync(password, salt);
```

`bcrypt.hashSync()` 函数有两个参数：密码和盐。 password 是我们要散列的密码，salt 用于使密码散列函数更难计算。

生成哈希后，我们可以将其传输到后端服务器。然后后端服务器可以使用 bcrypt.compareSync() 函数将哈希值与密码进行比较：

```javascript
const bcrypt = require('bcryptjs');

const password = 'secret';

const hash = '$2a$10$2znyB6.qE1T.1S7X3C5NU.7bHJNz5KUzHJZzM6DQLN8tm4Gxe6Ay';

bcrypt.compareSync(password, hash); // true
```

`bcrypt.compareSync()` 函数有两个参数：密码和散列。密码是我们要比较的密码，哈希是我们要与之比较的 bcrypt 哈希。

如果密码有效，“bcrypt.compareSync()”函数将返回“true”。如果密码无效，“bcrypt.compareSync()”函数将返回“false”。

## 与 JWT 相关的潜在陷阱有哪些？

与 JWT 相关的一个潜在缺陷是负载中的数据未加密。这意味着如果攻击者设法获得 JWT，他们将能够查看有效负载中的数据。

与 JWT 相关的另一个潜在陷阱是用于生成 JWT 签名的秘密必须保密。如果机密被泄露，攻击者将能够使用他们选择的任何数据生成他们自己的 JWT。

## 与 bcrypt 相关的潜在陷阱有哪些？

与 bcrypt 相关的一个潜在缺陷是它是一种单向散列函数。这意味着一旦密码被散列，就无法逆转。如果忘记密码，这会使恢复密码变得困难。

与 bcrypt 相关的另一个潜在缺陷是它的计算成本很高。这会使在大型数据集上使用 bcrypt 变得困难。

## 外部资源

- [JSON 网络令牌](https://jwt.io/)
- [Bcrypt](https://en.wikipedia.org/wiki/Bcrypt)
- [如何使用 JSON Web 令牌 (JWT) 在 TypeScript 应用程序中对用户进行身份验证](https://auth0.com/blog/how-to-use-jwts-to-authenticate-users-in-a-typescript-应用/）
- [如何使用 Bcrypt 保护 TypeScript 应用程序](https://www.sitepoint.com/secure-typescript-application-bcrypt/)