---
title: 047: Building and deploying scalable and performant applications with Nest.js
description: 
published: true
date: 2023-02-15T17:32:59.640Z
tags: 
editor: markdown
dateCreated: 2023-02-15T17:32:52.157Z
---

- [047: Creación e implementación de aplicaciones escalables y de alto rendimiento con Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/047-building-and-deploying-scalable-and-performant-applications-with-nest-js)
{.links-list}
- [047：使用 Nest.js 构建和部署可扩展的高性能应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/047-building-and-deploying-scalable-and-performant-applications-with-nest-js)
{.links-list}
- [047: Nest.js로 확장 가능하고 성능이 뛰어난 애플리케이션 구축 및 배포***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/047-building-and-deploying-scalable-and-performant-applications-with-nest-js)
{.links-list}


# Nest.js

Nest.js is a framework for building scalable and performant applications with Node.js. It is inspired by Angular and provides a powerful set of tools for creating server-side applications. In this post, we'll take a look at how to get started with Nest.js and how to build and deploy a scalable and performant application with it.

## Getting Started

To get started with Nest.js, you'll need to install the Nest.js CLI. You can do this with npm:

```
npm install -g @nestjs/cli
```

Once you have the Nest.js CLI installed, you can create a new Nest.js project with the following command:

```
nest new my-project
```

This will create a new directory called ```my-project``` with the basic Nest.js project structure inside.

## project structure

A Nest.js project has the following basic structure:

```
my-project
├── src
│   ├── app.controller.ts
│   ├── app.module.ts
│   ├── app.service.ts
│   ├── main.ts
│   └── ...
├── test
│   ├── app.controller.spec.ts
│   ├── app.service.spec.ts
│   └── ...
├── .gitignore
├── nest-cli.json
├── package-lock.json
└── package.json
```

The ```src``` directory contains the source code for your application. The ```app.controller.ts``` file contains the controller for your application. The ```app.module.ts``` file contains the module definition for your application. The ```app.service.ts``` file contains the service for your application. The ```main.ts``` file is the entry point for your application.

The ```test``` directory contains the unit tests for your application. The ```app.controller.spec.ts``` file contains the unit tests for the controller. The ```app.service.spec.ts``` file contains the unit tests for the service.

The ```.gitignore``` file contains the patterns for files that should be ignored by Git.

The ```nest-cli.json``` file contains the configuration for the Nest.js CLI.

The ```package-lock.json``` file contains the dependency versions for your project.

The ```package.json``` file contains the metadata for your project.

## Writing code

Now that you have a basic understanding of the project structure, let's take a look at how to write code in Nest.js.

### Controllers

Controllers are responsible for handling incoming HTTP requests and returning responses. In Nest.js, controllers are defined using the ```@Controller()``` decorator.

Here's an example controller that handles GET requests to the ```/hello``` route:

```javascript
@Controller('hello')
export class HelloController {

  @Get()
  hello() {
    return 'Hello, world!';
  }

}
```

In this example, the ```@Controller('hello')``` decorator defines the controller with the name ```hello```. The ```@Get()``` decorator defines a handler for GET requests. The ```hello()``` method is the handler function that returns the string ```Hello, world!```.

### Services

Services are singletons that are responsible for encapsulating business logic. In Nest.js, services are defined using the ```@Injectable()``` decorator.

Here's an example service that has a method for generating a greeting:

```javascript
@Injectable()
export class HelloService {

  generateGreeting(name: string) {
    return `Hello, ${name}!`;
  }

}
```

In this example, the ```@Injectable()``` decorator defines the service as being injectable. The ```generateGreeting()``` method takes a ```name``` parameter and returns a greeting string.

### Modules

Modules are used to organize related functionality in Nest.js. In Nest.js, modules are defined using the ```@Module()``` decorator.

Here's an example module that defines a controller and a service:

```javascript
@Module({
  controllers: [HelloController],
  providers: [HelloService],
})
export class HelloModule {}
```

In this example, the ```@Module()``` decorator defines the module with the ```HelloController``` and ```HelloService```.

## Building and deploying

Now that you've seen how to write code in Nest.js, let's take a look at how to build and deploy a Nest.js application.

### Building

To build a Nest.js application, you'll need to use the Nest.js CLI. The Nest.js CLI provides a ```build``` command that can be used to build a Nest.js application.

To build a Nest.js application, you'll need to run the following command:

```
nest build
```

This will build the Nest.js application and output the compiled files to the ```dist``` directory.

### Deploying

To deploy a Nest.js application, you'll need to use a Node.js hosting provider. There are many Node.js hosting providers to choose from, but we recommend using [Heroku](https://www.heroku.com/).

Heroku offers a free tier that you can use to deploy your Nest.js application. To deploy your application to Heroku, you'll need to create a ```Procfile``` in the root of your project. The ```Procfile``` is used to tell Heroku how to run your application.

Here's an example ```Procfile``` for a Nest.js application:

```
web: nest start
```

In this example, the ```web``` process type is used to tell Heroku that this is a web application. The ```nest start``` command is used to start the Nest.js application.

Once you have created the ```Procfile```, you can deploy your Nest.js application to Heroku with the following command:

```
git push heroku master
```

This will push your code to Heroku and trigger a new deployment.

## Conclusion

In this post, we've taken a look at how to get started with Nest.js and how to build and deploy a scalable and performant application with it. Nest.js is a powerful framework for building server-side applications and we hope this post has given you a good introduction to it.