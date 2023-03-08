---
title: Developing Chatbots with Microsoft Bot Framework
description: 
published: true
date: 2023-02-12T19:18:27.864Z
tags: 
editor: markdown
dateCreated: 2023-02-12T19:18:20.747Z
---

- [Desarrollo de chatbots con Microsoft Bot Framework***Spanish** document is available*](/es/Knowledge-base/Common/developing-chatbots-with-microsoft-bot-framework)
{.links-list}
- [使用 Microsoft Bot Framework 开发聊天机器人***Chinese Simplified** document is available*](/zh/Knowledge-base/Common/developing-chatbots-with-microsoft-bot-framework)
{.links-list}
- [Microsoft Bot Framework로 챗봇 개발***Korean** document is available*](/ko/Knowledge-base/Common/developing-chatbots-with-microsoft-bot-framework)
{.links-list}


# Developing Chatbots with Microsoft Bot Framework

Developing chatbots has become a hot topic in the IT industry as more businesses are seeking ways to automate customer interactions. Microsoft Bot Framework is one of the leading platforms for building chatbots, offering an easy-to-use set of tools and services that allow developers to create bots that can interact with users in a natural way.

In this article, we'll take a look at what it takes to develop chatbots using Microsoft Bot Framework. We'll start by looking at the different components of the framework and how they work together. Then we'll dive into some code examples to show you how to get started building your own chatbots.

## What is Microsoft Bot Framework?

Microsoft Bot Framework is a set of tools and services that help developers build chatbots for a variety of platforms, including Facebook Messenger, Skype, Slack, and more. The framework includes a Bot Builder SDK, which provides a set of APIs for building bots, and a set of tools and services for managing bot conversations.

The Bot Builder SDK allows developers to create bots that can understand natural language. The SDK includes a set of tools for building bots, including a dialog system, a set of natural language processing tools, and a set of tools for managing bot conversations.

The SDK also includes a set of APIs for integrating bots with a variety of services, including Facebook Messenger, Skype, Slack, and more.

## How Microsoft Bot Framework Works

Microsoft Bot Framework works by allowing developers to create bots that can understand natural language. The framework includes a set of tools for building bots, including a dialog system, a set of natural language processing tools, and a set of tools for managing bot conversations.

The framework also includes a set of APIs for integrating bots with a variety of services, including Facebook Messenger, Skype, Slack, and more.

## Getting Started with Microsoft Bot Framework

Now that we've looked at what Microsoft Bot Framework is and how it works, let's get started with some code examples.

The first thing you'll need to do is create a new Microsoft Bot Framework project. You can do this using the Microsoft Bot Framework Yeoman generator.

To install the generator, you'll need to have Node.js and Yeoman installed on your machine. To install Node.js, head over to the Node.js website and download the installer for your operating system.

Once Node.js is installed, you can install the Yeoman generator using the following command:

```
npm install -g yo generator-botframework
```

Once the generator is installed, you can create a new project using the following command:

```
yo botframework
```

You'll be prompted to enter a few details about your project, including the name, description, and version.

Once your project is generated, you'll need to install the dependencies. To do this, head over to the project directory and run the following command:

```
npm install
```

Once the dependencies are installed, you can start developing your chatbot.

## Developing Your Chatbot

Microsoft Bot Framework comes with a set of tools and services that make it easy to develop chatbots. In this section, we'll take a look at how to use the different components of the framework to develop your chatbot.

### The Bot Builder SDK

The Bot Builder SDK is a set of tools that allow you to build bots that can understand natural language. The SDK includes a dialog system, a set of natural language processing tools, and a set of tools for managing bot conversations.

To get started with the SDK, you'll need to create a new file in your project's root directory. The file should be named `bot.js`.

In the `bot.js` file, you'll need to require the `botbuilder` module and create a new `BotBuilder` instance.

```javascript
var builder = require('botbuilder');

var bot = new builder.BotBuilder();
```

### The Dialog System

The dialog system is the heart of the Bot Builder SDK. It allows you to define the flow of conversation between the user and the chatbot.

The dialog system is based on the concept of dialogs. A dialog is a unit of conversation between the user and the chatbot. Dialogs can be nested, meaning that a dialog can contain other dialogs.

To create a dialog, you'll need to create a new file in your project's `/dialogs` directory. The file should be named `{dialog_name}.js`.

In the `{dialog_name}.js` file, you'll need to require the `botbuilder` module and create a new `Dialog` instance.

```javascript
var builder = require('botbuilder');

var dialog = new builder.Dialog();
```

Once you have a `Dialog` instance, you can define the flow of conversation by adding dialogs to the `stack` property.

```javascript
dialog.stack(
    // First dialog in the stack
    function (session, args, next) {
        // Do something here
    },
    // Second dialog in the stack
    function (session, args, next) {
        // Do something here
    }
);
```

You can also add dialogs to the `stack` property using the `addDialog` method.

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
});
```

The `addDialog` method accepts an `onSelector` function, which allows you to specify when the dialog should be executed. The `onSelector` function should return `true` when the dialog should be executed and `false` when it should not.

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
}, function (session, args) {
    // Return true when the dialog should be executed
    return true;
});
```

The `addDialog` method also accepts an `onReject` function, which allows you to specify what should happen if the dialog is not executed. The `onReject` function should return a `Promise` that resolves with the value that should be passed to the next dialog in the stack.

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
}, function (session, args) {
    // Return false when the dialog should not be executed
    return false;
}, function (session, args) {
    // Return a Promise that resolves with the value that should be passed to the next dialog
    return Promise.resolve('some-value');
});
```

The `addDialog` method also accepts an `onPost` function, which allows you to specify what should happen after the dialog has been executed. The `onPost` function should return a `Promise` that resolves with the value that should be passed to the next dialog in the stack.

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
}, function (session, args) {
    // Return true when the dialog should be executed
    return true;
}, function (session, args) {
    // Return a Promise that resolves with the value that should be passed to the next dialog
    return Promise.resolve('some-value');
});
```

### The Natural Language Processing Tools

The Bot Builder SDK includes a set of tools for processing natural language. These tools can be used to understand the user's intent, extract entities from the user's input, and more.

The natural language processing tools are based on the `LuisRecognizer` and `QnAMakerRecognizer` classes.

To use the natural language processing tools, you'll need to create a new file in your project's `/recognizers` directory. The file should be named `{recognizer_name}.js`.

In the `{recognizer_name}.js` file, you'll need to require the `botbuilder` module and create a new `LuisRecognizer` or `QnAMakerRecognizer` instance.

```javascript
var builder = require('botbuilder');

var recognizer = new builder.LuisRecognizer();
```

Once you have a `LuisRecognizer` or `QnAMakerRecognizer` instance, you can use the `recognize` method to process the user's input.

```javascript
recognizer.recognize('What is your name?', function (err, result) {
    // Handle the result here
});
```

The `recognize` method accepts a `callback` function, which is called with the results of the recognition. The `callback` function is passed two arguments: `err` and `result`.

The `err` argument is an error object that is passed if an error occurred during recognition.

The `result` argument is an object that contains the results of the recognition. The object has the following properties:

- `intent`: The name of the intent that was recognized.
- `score`: A confidence score between 0 and 1.
- `entities`: An object containing the entities that were extracted from the user's input.

### The Tools for Managing Bot Conversations

The Bot Builder SDK includes a set of tools for managing bot conversations. These tools can be used to send messages to the user, end the conversation, and more.

To use the tools for managing bot conversations, you'll need to require the `botbuilder` module and create a new `ConversationBot` instance.

```javascript
var builder = require('botbuilder');

var bot = new builder.ConversationBot();
```

Once you have a `ConversationBot` instance, you can use the `message` method to send a message to the user.

```javascript
bot.message('Hello, world!');
```

The `message` method accepts a `text` argument, which is the message that should be sent to the user, and a `callback` function, which is called when the message has been sent.

You can also use the `endConversation` method to end the conversation.

```javascript
bot.endConversation();
```

The `endConversation` method does not accept any arguments.

## Deploying Your Chatbot

Once you've developed your chatbot, you'll need to deploy it to a server so that it can be used by users.

Microsoft Bot Framework comes with a set of tools and services for deploying chatbots. The framework includes a Bot Connector service, which allows you to connect your chatbot to a variety of chat platforms, including Facebook Messenger, Skype, Slack, and more.

To deploy your chatbot, you'll first need to create a new file in your project's root directory. The file should be named `.env`.

In the `.env` file, you'll need to add the following environment variables:

- `PORT`: The port on which your chatbot will be running.
- `MICROSOFT_APP_ID`: Your Microsoft App ID.
- `MICROSOFT_APP_PASSWORD`: Your Microsoft App Password.

Once you've added the environment variables to the `.env` file, you can start the chatbot using the following command:

```
npm start
```

Your chatbot will now be running on the port specified in the `PORT` environment variable.

## Conclusion

In this article, we've looked at what it takes to develop chatbots using Microsoft Bot Framework. We've looked at the different components of the framework and how they work together. We've also seen some code examples of how to get started building your own chatbots.