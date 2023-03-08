---
title: Working with Sessions and Cookies in TypeScript and Express.js
description: 
published: true
date: 2023-03-02T03:32:18.158Z
tags: 
editor: markdown
dateCreated: 2023-03-02T03:32:16.796Z
---

- [TypeScript 및 Express.js에서 세션 및 쿠키 작업***Korean** document is available*](/ko/Knowledge-base/TypeScript/working-with-sessions-and-cookies-in-typescript-and-express-js)
{.links-list}



# Working with Sessions and Cookies in TypeScript and Express.js

Sessions and cookies are an important part of web development. They allow us to store data about a user on the server and access it later. In this article, we'll learn how to work with sessions and cookies in TypeScript and Express.js.

## What are Sessions and Cookies?

Sessions and cookies are two different ways of storing data about a user on the server. Sessions are stored on the server, while cookies are stored on the user's computer.

Cookies are often used to store data such as a user's preferences or login information. Sessions are used to store data that we want to access later, such as a user's shopping cart.

## How to Create and Store a Cookie

To create and store a cookie, we can use the `cookie-parser` middleware. This middleware will parse the cookies from the request and make them available in the `req.cookies` object.

```javascript
var express = require('express');
var cookieParser = require('cookie-parser');

var app = express();
app.use(cookieParser());
```

Once we have the `cookie-parser` middleware set up, we can use the `res.cookie()` function to create a cookie. This function takes two arguments: the name of the cookie and the value of the cookie.

```javascript
res.cookie('name', 'value');
```

## How to Read a Cookie

Once we have set up the `cookie-parser` middleware, we can use the `req.cookies` object to read cookies. For example, if we have a cookie with the name `name`, we can read it like this:

```javascript
var name = req.cookies.name;
```

## How to Delete a Cookie

To delete a cookie, we can use the `res.clearCookie()` function. This function takes the name of the cookie as an argument.

```javascript
res.clearCookie('name');
```

## How to Create and Store a Session

To create and store a session, we can use the `express-session` middleware. This middleware will store the session data on the server.

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

Once we have the `express-session` middleware set up, we can use the `req.session` object to create a session. This object has a `.set()` function that we can use to set session data. The `.set()` function takes two arguments: the name of the session and the value of the session.

```javascript
req.session.set('name', 'value');
```

## How to Read a Session

To read a session, we can use the `req.session` object. This object has a `.get()` function that we can use to get session data. The `.get()` function takes the name of the session as an argument.

```javascript
var name = req.session.get('name');
```

## How to Delete a Session

To delete a session, we can use the `req.session.destroy()` function. This function will destroy the session and remove all session data.

```javascript
req.session.destroy();
```

## Conclusion

In this article, we've learned how to work with sessions and cookies in TypeScript and Express.js. We've seen how to create, read, and delete both cookies and sessions.