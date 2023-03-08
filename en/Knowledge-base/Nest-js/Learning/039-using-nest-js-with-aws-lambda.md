---
title: 039: Using Nest.js with AWS Lambda
description: 
published: true
date: 2023-02-09T03:17:49.752Z
tags: 
editor: markdown
dateCreated: 2023-02-09T03:17:43.713Z
---

- [039: Uso de Nest.js con AWS Lambda***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/039-using-nest-js-with-aws-lambda)
{.links-list}
- [039：将 Nest.js 与 AWS Lambda 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/039-using-nest-js-with-aws-lambda)
{.links-list}
- [039: AWS Lambda와 함께 Nest.js 사용***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/039-using-nest-js-with-aws-lambda)
{.links-list}


# 039: Using Nest.js with AWS Lambda

AWS Lambda is a serverless computing platform that allows you to run code without provisioning or managing servers. Nest.js is a framework for building efficient, scalable Node.js server-side applications.

In this post, we'll show you how to use Nest.js with AWS Lambda. We'll create a simple Nest.js application and deploy it to AWS Lambda.

##Creating a Nest.js Application

First, we need to create a Nest.js application. We can use the Nest.js CLI to generate a new project.

```
$ nest new nest-lambda
```

This will create a new Nest.js project in a folder called `nest-lambda`.

Next, we need to install the `@nestjs/aws-lambda` package. This package provides a Nest.js adapter for AWS Lambda.

```
$ cd nest-lambda
$ npm install --save @nestjs/aws-lambda
```

Now that we have the `@nestjs/aws-lambda` package installed, we can create a new file called `main.ts` in the `src` folder. This file will contains our Nest.js application.

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

In this file, we imported the `NestFactory` and `AppModule` from Nest.js. We then used the `NestFactory` to create a new Nest.js application. We passed in our `AppModule` to the `NestFactory`. Finally, we called the `listen` method to start the Nest.js application on port 3000.

##Deploying to AWS Lambda

Now that we have a Nest.js application, we can deploy it to AWS Lambda. First, we need to create an AWS account. Once you have an account, you can create a new AWS Lambda function.

In the Lambda console, click the "Create Function" button.

![create-function](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-create-function.png)

On the "Create Function" page, select the "Author from scratch" option.

![author-from-scratch](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-author-from-scratch.png)

On the "Configure Function" page, enter a name for your function and select the "Node.js 12.x" runtime. Then, scroll down and click the "Create Function" button.

![configure-function](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-configure-function.png)

Once the function has been created, you should see the "Function code" editor. In this editor, we'll add our Nest.js application code.

First, we need to install the `@nestjs/aws-lambda` package. We can do this using the `npm` command.

```
$ npm install --save @nestjs/aws-lambda
```

Next, we'll add our `main.ts` file to the "Function code" editor.

![function-code](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-function-code.png)

Once we've added our code, we need to select the "Handler" for our function. The handler is the entry point for our Lambda function. In our case, the handler is `main.handler`.

![handler](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-handler.png)

Now that we've configured our function, we can scroll down and click the "Save" button.

![save](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-save.png)

Once the function has been saved, we can test it by clicking the "Test" button.

![test](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-test.png)

On the "Configure test event" page, we can create a new test event. In this event, we'll set the `httpMethod` to `GET` and the `path` to `/`. Then, we'll click the "Create" button.

![configure-test-event](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-configure-test-event.png)

Once the test event has been created, we can click the "Test" button to run our function.

![test-2](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-test-2.png)

If everything went well, you should see the "Execution result" section with a `200` status code.

![execution-result](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-execution-result.png)

##Conclusion

In this post, we've shown you how to use Nest.js with AWS Lambda. We've created a simple Nest.js application and deployed it to AWS Lambda.