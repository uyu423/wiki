---
title: 011: Implementing authentication in Nest.js
description: 
published: true
date: 2023-02-14T21:32:48.365Z
tags: 
editor: markdown
dateCreated: 2023-02-14T21:32:46.280Z
---

- [011: Implementando autenticación en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/011-implementing-authentication-in-nest-js)
{.links-list}
- [011: 在 Nest.js 中实现身份验证***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/011-implementing-authentication-in-nest-js)
{.links-list}
- [011: Nest.js에서 인증 구현***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/011-implementing-authentication-in-nest-js)
{.links-list}


# Implementing authentication in Nest.js

Nest.js is a framework for building Node.js applications. It uses TypeScript and is influenced by Angular. Nest.js provides a way to structure code that is easy to use and maintain.

Authentication is a process of verifying the identity of a user. Nest.js provides a way to implement authentication in applications. In this post, we will learn how to implement authentication in a Nest.js application.

## What is authentication?

Authentication is the process of verifying the identity of a user. It is used to protect resources from unauthorized access. Authentication is usually done by asking the user to provide a username and password. The username and password are then verified against a database of authorized users.

## What is Nest.js?

Nest.js is a framework for building Node.js applications. It uses TypeScript and is influenced by Angular. Nest.js provides a way to structure code that is easy to use and maintain.

## What are the benefits of using Nest.js?

There are many benefits of using Nest.js, some of which are:

- Nest.js provides a way to structure code that is easy to use and maintain.
- Nest.js is easy to learn and use.
- Nest.js is based on TypeScript, which is a superset of JavaScript. This means that Nest.js code is easier to read and understand.
- Nest.js is influenced by Angular. This means that Nest.js code is easy to read and understand for those who are familiar with Angular.

## What is TypeScript?

TypeScript is a superset of JavaScript. This means that TypeScript code is easier to read and understand. TypeScript is also typed, which means that it can catch errors at compile time. This makes TypeScript code more reliable.

## What is the difference between JavaScript and TypeScript?

The difference between JavaScript and TypeScript is that TypeScript is typed and JavaScript is not. This means that TypeScript can catch errors at compile time. This makes TypeScript code more reliable.

## What is the difference between Node.js and Nest.js?

The difference between Node.js and Nest.js is that Nest.js is built on top of Node.js. Nest.js provides a way to structure code that is easy to use and maintain.

## How do I install Nest.js?

Nest.js can be installed using the Node.js Package Manager (npm). To install Nest.js, open a terminal and run the following command:

```
npm install -g @nestjs/cli
```

## How do I create a Nest.js project?

To create a Nest.js project, open a terminal and run the following command:

```
nest new project-name
```

Replace project-name with the name of your project. This will create a new Nest.js project with the name project-name.

## How do I run a Nest.js project?

To run a Nest.js project, open a terminal and navigate to the project directory. Then, run the following command:

```
nest start
```

This will start the Nest.js server. The server will be accessible at http://localhost:3000.

## What are the steps to implement authentication in Nest.js?

There are many ways to implement authentication in Nest.js. In this post, we will use the Passport.js library to implement authentication. Passport.js is a popular authentication library for Node.js.

The steps to implement authentication in Nest.js are:

1. Install the Passport.js library.
2. Configure Passport.js.
3. Create a login page.
4. Create a logout page.
5. Protect resources with authentication.

## Step 1: Install the Passport.js library

The first step is to install the Passport.js library. Passport.js is a popular authentication library for Node.js. To install the Passport.js library, open a terminal and run the following command:

```
npm install passport
```

## Step 2: Configure Passport.js

The next step is to configure Passport.js. Passport.js needs to know how to verify the identity of a user. This is done by providing a strategy. There are many strategies that can be used with Passport.js. In this post, we will use the LocalStrategy.

The LocalStrategy is a strategy that uses a username and password to verify the identity of a user. To use the LocalStrategy, we need to provide a callback function. This callback function will be called when Passport.js needs to verify the identity of a user.

The LocalStrategy callback function has the following signature:

```
function(username, password, done) {

}
```

The username and password arguments are the username and password that the user has provided. The done callback is a function that is used to return the result of the verification. The done callback has the following signature:

```
function(error, user, info) {

}
```

If the verification was successful, the user argument will contain the user object. If the verification was unsuccessful, the error and info arguments will contain information about the error.

To configure the LocalStrategy, we need to create a file called passport.js in the project root directory. The passport.js file should look like this:

```javascript
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;

passport.use(new LocalStrategy(
  function(username, password, done) {
    //Verify the username and password here
  }
));
```

Replace the //Verify the username and password here comment with the code to verify the username and password.

## Step 3: Create a login page

The next step is to create a login page. The login page will be a HTML page that contains a form. The form will have fields for the username and password. The form will be submitted to the /login route.

To create the login page, create a file called login.html in the project root directory. The login.html file should look like this:

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

## Step 4: Create a logout page

The next step is to create a logout page. The logout page will be a HTML page that contains a form. The form will have a field for the username. The form will be submitted to the /logout route.

To create the logout page, create a file called logout.html in the project root directory. The logout.html file should look like this:

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

## Step 5: Protect resources with authentication

The final step is to protect resources with authentication. To do this, we need to create a middleware function that checks if the user is authenticated. If the user is not authenticated, the middleware function will redirect the user to the login page.

To create the middleware function, create a file called auth.js in the project root directory. The auth.js file should look like this:

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

The isAuthenticated() function is the middleware function. The function checks if the user is authenticated. If the user is not authenticated, the function redirects the user to the /login page.

The middleware function can be used to protect any route. For example, to protect the /admin route, we can use the following code:

```javascript
app.get('/admin', auth.isAuthenticated, (req, res) => {
  // The authenticated user can access this route
});
```

## Conclusion

In this post, we learned how to implement authentication in a Nest.js application. We installed the Passport.js library and configured it to use the LocalStrategy. We also created a login page and a logout page. Finally, we protected resources with authentication.