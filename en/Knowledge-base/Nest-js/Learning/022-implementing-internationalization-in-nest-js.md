---
title: 022: Implementing internationalization in Nest.js
description: 
published: true
date: 2023-02-15T03:32:38.351Z
tags: 
editor: markdown
dateCreated: 2023-02-15T03:32:36.017Z
---

- [022: Implementando la internacionalización en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/022-implementing-internationalization-in-nest-js)
{.links-list}
- [022: 在 Nest.js 中实现国际化***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/022-implementing-internationalization-in-nest-js)
{.links-list}
- [022: Nest.js에서 국제화 구현***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/022-implementing-internationalization-in-nest-js)
{.links-list}


# Implementing internationalization in Nest.js

Nest.js is a Node.js framework for building scalable server-side applications. It uses TypeScript, a superset of JavaScript, and combines elements of Object-Oriented Programming, Functional Programming, and Functional Reactive Programming.

In this post, we'll be looking at how to implement internationalization in Nest.js. Internationalization is the process of designing and developing a product, application, or website for multiple markets. Nest.js provides a built-in module for i18n that makes it easy to add internationalization to your Nest.js applications.

## Getting started

Before we get started, let's make sure we have everything we need. First, we need to install the @nestjs/i18n module. We can do this with the following command:

```
npm install @nestjs/i18n
```

Once the module is installed, we need to create a configuration file for i18n. We'll call this file i18n.options.ts and it will go in the src directory of our Nest.js project. The file should look like this:

```typescript
import {
  I18nModuleOptions,
  I18nCoreModule,
} from '@nestjs/i18n';

const i18nModuleOptions: I18nModuleOptions = {
  fallbacks: {
    'en-US': 'en',
  },
  defaultLocale: 'en',
  path: __dirname,
};

export { i18nModuleOptions };
```

In this file, we're configuring the i18n module to use English as the default language. We're also telling the module to look for language files in the src directory.

## Creating language files

Now that we have our i18n configuration file set up, we need to create our language files. For this example, we'll be creating two language files: one for English and one for Spanish. We'll call these files en.json and es.json, respectively.

The en.json file should look like this:

```json
{
  "hello": "Hello, world!"
}
```

And the es.json file should look like this:

```json
{
  "hello": "¡Hola, mundo!"
}
```

These files contain our translations for the "hello" key. Notice that the structure of the files is the same, regardless of the language. This is because the i18n module uses the CommonJS module format.

## Using language files in our Nest.js application

Now that we have our language files set up, we can start using them in our Nest.js application.

First, we need to import the I18nModule in our application module. We can do this with the following code:

```typescript
import { Module } from '@nestjs/common';
import { I18nModule } from '@nestjs/i18n';

@Module({
  imports: [
    I18nModule.forRoot(),
  ],
})
export class ApplicationModule {}
```

Next, we need to create a service that will be responsible for handling our translations. We'll call this service I18nService. The service should look like this:

```typescript
import { Injectable } from '@nestjs/common';
import { I18nService as I18n } from '@nestjs/i18n';

@Injectable()
export class I18nService {
  constructor(private readonly i18n: I18n) {}

  translate(key: string, params?: any) {
    return this.i18n.translate(key, params);
  }
}
```

In this service, we're injecting the I18nService from the @nestjs/i18n module. We're also creating a translate() method that will be responsible for handling our translations.

Now that we have our service set up, we can use it in our controllers. For this example, we'll create a simple controller that returns a greeting in the user's preferred language. The controller should look like this:

```typescript
import { Controller, Get, Res } from '@nestjs/common';
import { Response } from 'express';
import { I18nService } from './i18n.service';

@Controller()
export class AppController {
  constructor(private readonly i18nService: I18nService) {}

  @Get()
  getHello(@Res() res: Response) {
    const message = this.i18nService.translate('hello');
    res.send(message);
  }
}
```

In this controller, we're injecting our I18nService. We're also creating a getHello() method that returns a greeting in the user's preferred language.

## Testing our Nest.js application

Now that we have our Nest.js application set up, let's test it to make sure everything is working as expected. We can do this with the following command:

```
npm test
```

If everything is working as expected, you should see the following output:

```
> nestjs-i18n@0.0.1 test /Users/username/projects/nestjs-i18n
> jest

 PASS  src/app.controller.spec.ts
  AppController
    GET /
      ✓ should return "Hello, world!" (5ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.548s
Ran all test suites.
```

## Conclusion

In this post, we've looked at how to implement internationalization in Nest.js. We've created language files and a service to handle our translations. We've also created a controller that returns a greeting in the user's preferred language.