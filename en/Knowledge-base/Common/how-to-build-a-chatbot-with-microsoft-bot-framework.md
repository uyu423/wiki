---
title: How to Build a Chatbot with Microsoft Bot Framework
description: 
published: true
date: 2023-02-12T09:17:37.424Z
tags: 
editor: markdown
dateCreated: 2023-02-12T09:17:30.478Z
---

- [Cómo construir un chatbot con Microsoft Bot Framework***Spanish** document is available*](/es/Knowledge-base/Common/how-to-build-a-chatbot-with-microsoft-bot-framework)
{.links-list}
- [如何使用 Microsoft Bot Framework 构建聊天机器人***Chinese Simplified** document is available*](/zh/Knowledge-base/Common/how-to-build-a-chatbot-with-microsoft-bot-framework)
{.links-list}
- [Microsoft Bot Framework로 챗봇을 구축하는 방법***Korean** document is available*](/ko/Knowledge-base/Common/how-to-build-a-chatbot-with-microsoft-bot-framework)
{.links-list}


# How to Build a Chatbot with Microsoft Bot Framework

Developing a chatbot can seem like a daunting task, but with the Microsoft Bot Framework it can be easy and fun! In this article, we'll go over everything you need to know to get started building your own chatbot.

## What is a chatbot?

A chatbot is a computer program that simulates human conversation. Chatbots are used in a variety of industries, including customer service, marketing, and even healthcare.

## Why build a chatbot?

Chatbots can be a great way to improve customer service or help people find information. They can also be used for marketing or even just for fun!

## What do I need to build a chatbot?

To build a chatbot, you'll need a computer with an internet connection and a text editor. You'll also need a Microsoft account. If you don't have one, you can create one for free.

## How do I build a chatbot?

There are two main ways to build a chatbot: using the Bot Framework tools or using the Azure Bot Service.

### Using the Bot Framework tools

The Bot Framework tools are a great way to get started building your chatbot. They include everything you need to get started, including a Bot Builder SDK and a CLI.

To get started, first create a new folder for your chatbot project. Then, open the folder in your text editor and create a file called `app.js`.

Next, you'll need to install the Bot Builder SDK. You can do this using npm:

```
npm install botbuilder
```

Once the SDK is installed, you can import it into your `app.js` file:

```js
const builder = require('botbuilder');
```

Now you're ready to start coding!

First, you'll need to create a bot adapter. This will be used to connect your chatbot to the Microsoft Bot Framework. You can do this with the following code:

```js
const adapter = new builder.BotFrameworkAdapter();
```

Next, you'll need to create a bot handler. This will be used to handle incoming messages from the user. You can do this with the following code:

```js
const bot = new builder.UniversalBot(adapter);
```

Now you're ready to start adding code to your bot handler!

The first thing you'll need to do is define a ` WelcomeMessage` dialog. This dialog will be used to greet the user and get started. You can do this with the following code:

```js
bot.dialog('WelcomeMessage', [
    (session) => {
        session.send("Hello! I'm a chatbot.");
        session.beginDialog('GetName');
    },
]);
```

As you can see, this dialog will send a message to the user and then start the `GetName` dialog.

The `GetName` dialog will be used to get the user's name. You can do this with the following code:

```js
bot.dialog('GetName', [
    (session) => {
        builder.Prompts.text(session, "What's your name?");
    },
    (session, results) => {
        session.endDialog(`Hello, ${results.response}!`);
    },
]);
```

As you can see, this dialog will prompt the user for their name and then store the response in a variable called `results.response`. It will then end the dialog and send a message to the user with their name.

Now you're ready to test your chatbot! To do this, you'll need to run the following command:

```
node app.js
```

This will start your chatbot and you can now talk to it! Try saying "Hello" or "What's your name?" and see what it does.

### Using the Azure Bot Service

The Azure Bot Service is a great way to build and deploy your chatbot. It includes everything you need to get started, including a Bot Builder SDK and a CLI.

To get started, first create a new folder for your chatbot project. Then, open the folder in your text editor and create a file called `app.js`.

Next, you'll need to install the Bot Builder SDK. You can do this using npm:

```
npm install botbuilder
```

Once the SDK is installed, you can import it into your `app.js` file:

```js
const builder = require('botbuilder');
```

Now you're ready to start coding!

First, you'll need to create a bot adapter. This will be used to connect your chatbot to the Microsoft Bot Framework. You can do this with the following code:

```js
const adapter = new builder.BotFrameworkAdapter();
```

Next, you'll need to create a bot handler. This will be used to handle incoming messages from the user. You can do this with the following code:

```js
const bot = new builder.UniversalBot(adapter);
```

Now you're ready to start adding code to your bot handler!

The first thing you'll need to do is define a ` WelcomeMessage` dialog. This dialog will be used to greet the user and get started. You can do this with the following code:

```js
bot.dialog('WelcomeMessage', [
    (session) => {
        session.send("Hello! I'm a chatbot.");
        session.beginDialog('GetName');
    },
]);
```

As you can see, this dialog will send a message to the user and then start the `GetName` dialog.

The `GetName` dialog will be used to get the user's name. You can do this with the following code:

```js
bot.dialog('GetName', [
    (session) => {
        builder.Prompts.text(session, "What's your name?");
    },
    (session, results) => {
        session.endDialog(`Hello, ${results.response}!`);
    },
]);
```

As you can see, this dialog will prompt the user for their name and then store the response in a variable called `results.response`. It will then end the dialog and send a message to the user with their name.

Now you're ready to test your chatbot! To do this, you'll need to run the following command:

```
node app.js
```

This will start your chatbot and you can now talk to it! Try saying "Hello" or "What's your name?" and see what it does.

## Resources

- [Microsoft Bot Framework](https://dev.botframework.com/)
- [Azure Bot Service](https://azure.microsoft.com/en-us/services/bot-service/)
- [Bot Builder SDK](https://docs.microsoft.com/en-us/javascript/api/botbuilder-core/botbuilder-core-sdk?view=botbuilder-js-stable)