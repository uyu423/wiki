---
title: Implementing Role-Based Access Control in TypeScript Applications
description: 
published: true
date: 2023-02-01T08:05:48.410Z
tags: 
editor: markdown
dateCreated: 2023-02-01T08:05:46.873Z
---

- [TypeScript 애플리케이션에서 역할 기반 액세스 제어 구현***Korean** version of this document is available*](/ko/Knowledge-base/TypeScript/implementing-role-based-access-control-in-typescript-applications)
{.links-list}
- [在 TypeScript 应用程序中实现基于角色的访问控制***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/TypeScript/implementing-role-based-access-control-in-typescript-applications)
{.links-list}


  Implementing Role-Based Access Control in TypeScript Applications

Role-based access control (RBAC) is a model for permissions that is commonly used in applications. In RBAC, each user is assigned one or more roles, and each role has a set of permissions. This model is flexible and scalable, and it can be used to provide different levels of access to different parts of an application for different users.

In this article, we will show how to implement RBAC in a TypeScript application using the node-acl package. We will first create a simple application with two users and two roles. We will then add RBAC to the application and use it to restrict access to certain parts of the application based on the roles of the users.

## The Application

We will start by creating a simple TypeScript application with two users and two roles. The users and roles will be hard-coded in the application for simplicity. In a real application, you would likely store this information in a database.

The application will have two pages: a home page and a profile page. The home page will be accessible to all users, but the profile page will only be accessible to users who are logged in.

The home page will look like this:

![Home page](https://i.imgur.com/P0jrQbu.png)

The profile page will look like this:

![Profile page](https://i.imgur.com/TK7gNcu.png)

Users will be able to log in and out of the application using the login form on the home page. When a user logs in, their username will be displayed on the profile page.

To keep the focus on RBAC, we will not be implementing a full authentication system in this article. Instead, we will simply set a session variable when a user logs in. In a real application, you would want to use a more secure authentication method, such as JSON Web Tokens.

The code for the application is available in this [GitHub repository](https://github.com/ auth0-blog/typescript-rbac-app).

## Setting Up the Project

Before we start implementing RBAC, we need to set up the project. First, we need to create a new TypeScript project. We can do this using the [TypeScript template](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html) on the TypeScript website.

Once the project has been created, we need to install the dependencies that we will need for the project. In this case, we need the [Express](https://expressjs.com/) web framework and the [node-acl](https://www.npmjs.com/package/node-acl) package for implementing RBAC. We can install these dependencies using npm:

```
npm install express node-acl --save
```

We also need to install the [TypeScript](https://www.typescriptlang.org/) compiler and [Webpack](https://webpack.js.org/) module bundler. We can install these dependencies using npm as well:

```
npm install typescript webpack webpack-cli --save-dev
```

## Implementing RBAC

Now that we have our project set up, we can start implementing RBAC. We will start by creating a new file called `acl.ts` in the `src` directory. This file will contain the code for setting up and using the node-acl package.

First, we need to import the node-acl package and the Express Request and Response interfaces. We will also import the node-acl MemoryBackend, which we will use to store the ACL data in memory:

```typescript
import * as acl from 'acl';
import { Request, Response } from 'express';
import { MemoryBackend } from 'acl';
```

Next, we need to create a new instance of the node-acl MemoryBackend. We will also create a new instance of the node-acl acl class, which we will use to create and manage the ACL:

```typescript
const backend = new MemoryBackend();
const acl = new acl(backend);
```

Now that we have our backend and acl instances set up, we can start creating the roles and permissions for our application.

We will start by creating two roles: `user` and `admin`. The `user` role will have the `view` permission, which will allow users to view the home page. The `admin` role will have the `view` and `edit` permissions, which will allow admins to view and edit the profile page:

```typescript
acl.allow([
  {
    roles: ['user'],
    allows: [
      { resources: '/', permissions: 'view' }
    ]
  },
  {
    roles: ['admin'],
    allows: [
      { resources: '/', permissions: 'view' },
      { resources: '/profile', permissions: 'edit' }
    ]
  }
]);
```

We also need to create a `guest` role. This role will not have any permissions, which will prevent guests from accessing any part of the application:

```typescript
acl.addRoleParents('guest', []);
```

Now that we have our roles and permissions set up, we need to create a middleware function that will check the ACL to see if a user has the permission to access a certain resource.

First, we need to import the Express Request and Response interfaces. We will also import the node-acl acl class:

```typescript
import { Request, Response } from 'express';
import { acl } from 'acl';
```

Next, we will create a new middleware function called `checkPermission`:

```typescript
function checkPermission(resource: string, action: string) {
  return (req: Request, res: Response, next: Function) => {
    acl.isAllowed(req.session.user, resource, action, (err: Error, allowed: boolean) => {
      if (err) {
        next(err);
      } else if (allowed) {
        next();
      } else {
        res.status(403).send('Forbidden');
      }
    });
  };
}
```

This middleware function takes two arguments: the resource that the user is trying to access and the action that they are trying to perform on that resource. The `isAllowed` method of the acl instance is used to check if the user has the permission to access the resource. If the user does not have the permission, a status code of `403` is returned.

## Adding RBAC to the Application

Now that we have our middleware function set up, we can add it to our application.

First, we need to import the `express` and `body-parser` packages. We will also import the `./acl` file that we created in the previous section:

```typescript
import * as express from 'express';
import * as bodyParser from 'body-parser';
import * as acl from './acl';
```

Next, we will create a new Express application and configure it to use the `body-parser` middleware:

```typescript
const app = express();
app.use(bodyParser.json());
```

Now, we can start adding our routes.

The first route that we will add is the `GET /` route. This route will render the home page of the application:

```typescript
app.get('/', (req: Request, res: Response) => {
  res.send(`
    <html>
      <head>
        <title>Home</title>
      </head>
      <body>
        <h1>Home</h1>
        ${req.session.user ? `<p>Welcome, ${req.session.user}!</p>` : ''}
        <a href="/profile">Profile</a>
      </body>
    </html>
  `);
});
```

Next, we will add the `GET /profile` route. This route will render the profile page of the application:

```typescript
app.get('/profile', checkPermission('/profile', 'view'), (req: Request, res: Response) => {
  res.send(`
    <html>
      <head>
        <title>Profile</title>
      </head>
      <body>
        <h1>Profile</h1>
        <p>Welcome, ${req.session.user}!</p>
        <a href="/">Home</a>
      </body>
    </html>
  `);
});
```

Notice that we have added the `checkPermission` middleware function to this route. This will ensure that only users with the `view` permission will be able to access this route.

Finally, we will add the `POST /login` route. This route will be used to log users in and out of the application:

```typescript
app.post('/login', (req: Request, res: Response) => {
  const { user } = req.body;
  req.session.user = user;
  res.redirect('/');
});
```

This route will set the `user` property of the session object to the username that is passed in the request body.

## Testing the Application

Now that we have our application set up, we can test it to see if RBAC is working as expected.

First, we need to build the application. We can do this using the `webpack` command:

```
webpack
```

Next, we need to start the application. We can do this using the `node` command:

```
node ./dist/bundle.js
```

Now, we can open the application in a web browser and test it.

If we try to access the `/profile` route without logging in, we should see the following error message:

![Error message](https://i.imgur.com/vALDKd7.png)

This is the expected behavior, as we have not given the `guest` role the `view` permission for the `/profile` route.

If we log in as the `user` role, we should be able to access the home page, but we should not be able to access the profile page:

![Home page](https://i.imgur.com/P0jrQbu.png)

![Profile page](https://i.imgur.com/TK7gNcu.png)

This is the expected behavior, as we have only given the `user` role the `view` permission for the `/` route.

If we log in as the `admin` role, we should be able to access the home page and the profile page:

![Home page](https://i.imgur.com/P0jrQbu.png)

![Profile page](https://i.imgur.com/TK7gNcu.png)

This is the expected behavior, as we have given the `admin` role the `view` and `edit` permissions for the `/` and `/profile` routes.

## Conclusion

In this article, we have shown how to implement RBAC in a TypeScript application using the node-acl package. We have created a simple application with two users and two roles. We have then added RBAC to the application and used it to restrict access to certain parts of the application based on the roles of the users.

If you would like to learn more about RBAC, we recommend the following resources:

- [Role-Based Access Control](https://en.wikipedia.org/wiki/Role-based_access_control) on Wikipedia
- [node-acl Documentation](https://github.com/ OptimalBits/node-acl)
- [Express documentation](https://expressjs.com/en/guide/rbac.html)