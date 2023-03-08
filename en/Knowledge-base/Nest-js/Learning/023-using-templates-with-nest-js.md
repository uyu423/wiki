---
title: 023: Using templates with Nest.js
description: 
published: true
date: 2023-02-15T04:32:38.773Z
tags: 
editor: markdown
dateCreated: 2023-02-15T04:32:31.164Z
---

- [023: Uso de plantillas con Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/023-using-templates-with-nest-js)
{.links-list}
- [023: 在 Nest.js 中使用模板***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/023-using-templates-with-nest-js)
{.links-list}
- [023: Nest.js에서 템플릿 사용하기***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/023-using-templates-with-nest-js)
{.links-list}


## Introduction

Nest.js is a Node.js framework for building scalable server-side applications. It uses TypeScript, a language that provides static type-checking and powerful tooling for large-scale development. 

Nest.js applications are built using a modular approach, which allows developers to break up their code into smaller pieces that can be reused across the application. Nest.js comes with a built-in dependency injection system that makes it easy to inject services and other dependencies into components.

One of the most powerful features of Nest.js is its use of templates. Nest.js templates are based on the popular AngularJS template system, and they provide a way to modularize your HTML and reduce the amount of code you have to write. 

In this post, we'll take a look at how to use templates with Nest.js. We'll start by creating a simple Nest.js application and then we'll add a template to it. Finally, we'll learn how to use the template to render data from a database.

##Creating a Nest.js Application

Let's start by creating a new Nest.js application. We'll use the Nest.js CLI to generate a new application. First, make sure you have the Nest.js CLI installed. If you don't have it installed, you can install it using npm:

```
npm install -g @nestjs/cli
```

Once the Nest.js CLI is installed, we can use it to generate a new application. We'll call our application "template-app":

```
nest new template-app
```

This will create a new directory called "template-app" and generate the files needed for a basic Nest.js application.

## Adding a Template

Now that we have a basic Nest.js application, let's add a template to it. Nest.js comes with a built-in template engine called Nest.js View. Nest.js View is based on the popular AngularJS template engine, and it provides a way to modularize your HTML and reduce the amount of code you have to write. 

To add a template to our Nest.js application, we need to create a new file called "template.html" in the "src/views" directory. The "src/views" directory is where Nest.js looks for templates. 

In our "template.html" file, we'll add a simple HTML template:

```html
<html>
  <head>
    <title>Template App</title>
  </head>
  <body>
    <h1>Hello, World!</h1>
  </body>
</html>
```

Now that we have our template, let's use it in our Nest.js application.

## Using the Template

To use our template, we need to tell Nest.js where to find it. We can do this by adding a "template" property to the "view" object in the "src/main.ts" file:

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.setViewEngine({
    type: 'html',
    template: './src/views/template.html',
  });

  await app.listen(3000);
}
bootstrap();
```

The "template" property tells Nest.js where to find our template file. In this case, we're telling Nest.js to look for the "template.html" file in the "src/views" directory. 

Now that we've told Nest.js where to find our template, we can use it to render data.

## Rendering Data

To render data in our template, we need to use the "render" function. The "render" function takes two arguments: a data object and a response object. The data object contains the data that we want to render, and the response object is used to send the rendered HTML to the client. 

Let's take a look at an example. In this example, we'll render a list of users in our template:

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.setViewEngine({
    type: 'html',
    template: './src/views/template.html',
  });

  app.get('/users', (req, res) => {
    const users = [
      {
        name: 'John Doe',
        age: 30,
      },
      {
        name: 'Jane Doe',
        age: 31,
      },
    ];

    res.render('users', { users });
  });

  await app.listen(3000);
}
bootstrap();
```

In this example, we've added a new route to our Nest.js application that renders a list of users. We're using the "render" function to render the "users" template and pass in a data object containing a list of users. 

Now that we've seen how to render data in a Nest.js template, let's take a look at how to access the data in our template.

## Accessing Data in the Template

To access data in the template, we use the "render" function's "data" argument. The "data" argument is an object that contains the data that we want to render. 

In our "template.html" file, we can access the data that we passed in using the "render" function like this:

```html
<html>
  <head>
    <title>Template App</title>
  </head>
  <body>
    <h1>Users</h1>
    <ul>
      <li>
        {{ users[0].name }} - {{ users[0].age }}
      </li>
      <li>
        {{ users[1].name }} - {{ users[1].age }}
      </li>
    </ul>
  </body>
</html>
```

In this example, we're using the "render" function's "data" argument to access the list of users that we passed in. We're then looping over the list of users and rendering their name and age. 

Now that we've seen how to use templates with Nest.js, let's take a look at some resources for further reading.

## Resources for Further Reading

- [Nest.js View](https://docs.nestjs.com/v/6/view)
- [AngularJS](https://angularjs.org/)
- [Handlebars](https://handlebarsjs.com/)