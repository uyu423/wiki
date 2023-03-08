---
title: 013: Implementing authorization in Nest.js
description: 
published: true
date: 2023-02-14T23:32:26.637Z
tags: 
editor: markdown
dateCreated: 2023-02-14T23:32:18.986Z
---

- [013: Implementación de autorización en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/013-implementing-authorization-in-nest-js)
{.links-list}
- [013: 在 Nest.js 中实现授权***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/013-implementing-authorization-in-nest-js)
{.links-list}
- [013: Nest.js에서 인증 구현***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/013-implementing-authorization-in-nest-js)
{.links-list}


# Implementing authorization in Nest.js

Nest.js is a Node.js framework for building scalable server-side applications. It uses progressive JavaScript, is built with TypeScript (preserves compatibility with pure JavaScript) and combines elements of Object-Oriented Programming, Functional Programming, and Functional Reactive Programming.

In this post, we'll focus on how to implement authorization in a Nest.js application. We'll look at what authorization is and why it's important, before moving on to how to implement it in Nest.js.

## What is authorization?

Authorization is the process of determining whether a user is allowed to perform an action or access a resource. It usually involves checking that the user has the necessary permissions to perform the action.

In a web application, authorization is typically done by checking the user's identity and then comparing it to a list of authorized users. If the user is authorized, they are allowed to access the resource. If they are not authorized, they are not allowed to access the resource.

There are two main types of authorization:

- **Authentication**: This is the process of verifying that the user is who they say they are. In a web application, this is usually done by checking the user's credentials (e.g. username and password) against a database of users.

- **Authorization**: This is the process of verifying that the user has the necessary permissions to access a resource. In a web application, this is usually done by checking the user's identity against a list of authorized users. If the user is authorized, they are allowed to access the resource. If they are not authorized, they are not allowed to access the resource.

## Why is authorization important?

Authorization is important because it helps to keep your application secure. By only allowing authorized users to access resources, you can help to prevent unauthorized access to sensitive data.

## Implementing authorization in Nest.js

Nest.js provides a number of ways to implement authorization. In this section, we'll look at two of the most common ways: using the `@Authorized()` decorator and the `CanActivate` guards.

### Using the `@Authorized()` decorator

The `@Authorized()` decorator can be used to restrict access to a controller or action. It takes a single argument, which is the list of roles that are allowed to access the controller or action.

For example, the following controller would only be accessible to users with the `ADMIN` role:

```typescript
@Controller('/users')
@Authorized(['ADMIN'])
export class UserController {

}
```

If a user without the `ADMIN` role tried to access the `/users` endpoint, they would receive an ` unauthorized` error.

### Using the `CanActivate` guards

The `CanActivate` guards can be used to restrict access to a route. They take a single argument, which is the list of roles that are allowed to access the route.

For example, the following route would only be accessible to users with the `ADMIN` role:

```typescript
@Get('/users')
@CanActivate(['ADMIN'])
export class UserController {

}
```

If a user without the `ADMIN` role tried to access the `/users` endpoint, they would receive an ` unauthorized` error.

## Additional information

- Nest.js documentation: https://docs.nestjs.com/
- TypeScript documentation: https://www.typescriptlang.org/docs/handbook/basic-types.html