---
title: 050: Advanced Nest.js features and techniques
description: 
published: true
date: 2023-02-15T18:33:09.769Z
tags: 
editor: markdown
dateCreated: 2023-02-15T18:33:00.857Z
---

- [050: funciones y técnicas avanzadas de Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/050-advanced-nest-js-features-and-techniques)
{.links-list}
- [050：高级 Nest.js 特性和技术***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/050-advanced-nest-js-features-and-techniques)
{.links-list}
- [050: 고급 Nest.js 기능 및 기술***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/050-advanced-nest-js-features-and-techniques)
{.links-list}


050: Advanced Nest.js features and techniques

Nest.js is a powerful web framework for Node.js. It is built on top of Express.js and makes use of TypeScript, which makes it easy to develop and deploy enterprise-grade applications.

In this post, we will take a look at some of the advanced features and techniques that Nest.js offers.

We will cover the following topics:

- Routing
- Authentication and authorization
- Database access
- Testing

## Routing

In Nest.js, routes are defined using the @Controller() decorator. For example:

```typescript
@Controller('/users')
export class UserController {

  @Get('/')
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

As you can see, the @Controller() decorator defines the base path for all the routes defined within the controller. The @Get(), @Post(), @Put(), and @Delete() decorators are used to define the HTTP methods for each route.

## Authentication and authorization

Nest.js provides out-of-the-box support for authentication and authorization.

To authenticate a user, Nest.js provides the @Authenticate() decorator. This decorator can be used on a controller or method level.

For example, to authenticate all the routes defined in the UserController, we can use the @Authenticate() decorator on the controller:

```typescript
@Controller('/users')
@Authenticate()
export class UserController {
  // ...
}
```

To authenticate only certain routes, we can use the @Authenticate() decorator on the methods:

```typescript
@Controller('/users')
export class UserController {

  @Get('/')
  @Authenticate()
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

Nest.js also provides the @Authorize() decorator for authorization. This decorator can be used on a controller or method level.

For example, to authorize all the routes defined in the UserController, we can use the @Authorize() decorator on the controller:

```typescript
@Controller('/users')
@Authorize()
export class UserController {
  // ...
}
```

To authorize only certain routes, we can use the @Authorize() decorator on the methods:

```typescript
@Controller('/users')
export class UserController {

  @Get('/')
  @Authorize()
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

## Database access

Nest.js provides several ways to access databases.

The most common way is to use the @Inject() decorator to inject a database client into your controller or service.

For example, to inject a MongoDB client into your controller, you can use the following code:

```typescript
@Controller('/users')
export class UserController {

  constructor(
    @Inject('MONGODB_CLIENT') private mongodb: MongoClient,
  ) {}

  // ...

}
```

Another way to access databases is to use the @UseDatabases() decorator. This decorator can be used on a controller or service level.

For example, to use MongoDB and PostgreSQL in your controller, you can use the following code:

```typescript
@Controller('/users')
@UseDatabases(['MONGODB', 'POSTGRESQL'])
export class UserController {

  // ...

}
```

## Testing

Nest.js provides several ways to test your applications.

The most common way is to use the @Test() decorator. This decorator can be used on a controller or service level.

For example, to test the UserController, you can use the following code:

```typescript
@Test()
export class UserController {

  @Get('/')
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

Another way to test your application is to use the @TestModule() decorator. This decorator can be used on a module level.

For example, to test the UserModule, you can use the following code:

```typescript
@TestModule()
export class UserModule {}
```

## Conclusion

In this post, we have covered some of the advanced features and techniques that Nest.js offers.

We have seen how to define routes, how to authenticate and authorize users, how to access databases, and how to test Nest.js applications.

If you want to learn more about Nest.js, I recommend checking out the official documentation.