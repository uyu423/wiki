---
title: 018: Creating reusable components in Nest.js
description: 
published: true
date: 2023-02-07T21:17:18.180Z
tags: 
editor: markdown
dateCreated: 2023-02-07T21:17:16.602Z
---

- [018: Creación de componentes reutilizables en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/018-creating-reusable-components-in-nest-js)
{.links-list}
- [018：在 Nest.js 中创建可重用组件***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/018-creating-reusable-components-in-nest-js)
{.links-list}
- [018: Nest.js에서 재사용 가능한 구성 요소 만들기***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/018-creating-reusable-components-in-nest-js)
{.links-list}


# Creating reusable components in Nest.js

Nest.js is a framework for building Node.js applications. It uses TypeScript and is built on top of Express.js.

One of the benefits of using Nest.js is that it makes it easy to create reusable components. In this post, we'll look at how to create a reusable component in Nest.js.

## Defining a component

The first step in creating a reusable component is to define it. We can do this using the @Component decorator.

For example, let's say we want to create a component that logs information about a user. We would define it like this:

```typescript
@Component()
export class UserLoggerComponent {
  // ...
}
```

## Using a component

Once we have defined a component, we can use it in our Nest.js application by injecting it into a controller or service.

For example, let's say we have a controller that handles requests to create users. We can inject our UserLoggerComponent into this controller and use it to log information about the new user:

```typescript
@Controller('users')
export class UserController {
  constructor(private readonly userLogger: UserLoggerComponent) {}

  @Post()
  async createUser(@Body() userDto: UserDto) {
    // ...

    this.userLogger.log(userDto);

    // ...
  }
}
```

## Conclusion

In this post, we've seen how to create reusable components in Nest.js. We've defined a component using the @Component decorator and injected it into a controller to use it.