---
title: 015: Error handling in Nest.js
description: 
published: true
date: 2023-02-11T01:17:32.298Z
tags: 
editor: markdown
dateCreated: 2023-02-11T01:17:25.633Z
---

- [015: manejo de errores en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/015-error-handling-in-nest-js)
{.links-list}
- [015: Nest.js 中的错误处理***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/015-error-handling-in-nest-js)
{.links-list}
- [015: Nest.js의 오류 처리***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/015-error-handling-in-nest-js)
{.links-list}


# Error handling in Nest.js

Developing web applications can be tricky - especially when it comes to error handling. There are many ways to handle errors in Nest.js, and in this post we'll explore some of the most common methods.

## Try/catch

The try/catch method is the most basic way to handle errors in Nest.js. To use this method, you simply wrap your code in a try block, and then add a catch block to handle any errors that may occur.

Here's a simple example:

```javascript
try {
  // do something that might throw an error
} catch (err) {
  // handle the error
}
```

If an error does occur, it will be caught by the catch block and can be dealt with accordingly.

## Asynchronous error handling

If you're using asynchronous code (i.e. code that uses Promises or async/await), you can still use the try/catch method. However, you need to be aware of the fact that errors thrown in asynchronous code are actually caught by the next tick of the event loop.

This means that if you have a try/catch block surrounding asynchronous code, the catch block will not be executed until the next tick of the event loop. This can be confusing, so let's take a look at an example:

```javascript
try {
  // do something that might throw an error
  setTimeout(() => {
    throw new Error('something went wrong');
  }, 1000);
} catch (err) {
  // this catch block will not be executed until 1000ms have passed
}
```

In the example above, the error will not be caught until 1000ms have passed. This is because the setTimeout function is asynchronous, and the error is only thrown on the next tick of the event loop.

To avoid this, you can use the Promise.catch method:

```javascript
try {
  // do something that might throw an error
  setTimeout(() => {
    throw new Error('something went wrong');
  }, 1000);
} catch (err) {
  // this catch block will not be executed until 1000ms have passed
}

Promise.catch((err) => {
  // this catch block will be executed immediately
});
```

## Error handling middleware

If you want to centralize your error handling, you can use Nest.js middleware. Middleware is a function that is executed before a request hits your controller code. This makes it the perfect place to put your error handling logic.

To create a middleware function, you need to use the @UseMiddleware decorator:

```javascript
import { UseMiddleware, Middleware } from '@nestjs/common';

@Middleware()
export class ErrorHandlerMiddleware implements NestMiddleware {
  // your middleware logic goes here
}
```

Then, to use the middleware, you need to register it in your Nest.js module:

```javascript
@Module({
  imports: [],
  controllers: [],
  providers: [],
  middleware: [ErrorHandlerMiddleware],
})
export class AppModule {}
```

Now, any errors that occur in your application will be handled by the middleware function.

## Conclusion

As you can see, there are many ways to handle errors in Nest.js. Which method you choose will depend on your specific needs. However, all of the methods described in this post should give you a good starting point for dealing with errors in your Nest.js applications.