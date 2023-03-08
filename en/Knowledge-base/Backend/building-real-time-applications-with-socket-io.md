---
title: Building Real-time Applications with Socket.io
description: 
published: true
date: 2023-02-17T18:00:56.698Z
tags: 
editor: markdown
dateCreated: 2023-01-29T21:21:07.676Z
---

- [Socket.io로 실시간 애플리케이션 구축***Korean** version of this document is available*](/ko/Knowledge-base/Backend/building-real-time-applications-with-socket-io)
{.links-list}


# Building Real-time Applications with Socket.io

In this article, we'll be looking at how to build real-time applications with Socket.io. Socket.io is a JavaScript library that allows us to easily create real-time, two-way communication applications.

We'll be building a simple chat application. Our chat application will have two parts: a front-end web interface that we'll build using HTML, CSS, and JavaScript, and a back-end server that we'll build using Node.js and Socket.io.

## Setting up our development environment

Before we start writing any code, we need to set up our development environment. We'll need to install Node.js and the Socket.io library.

### Installing Node.js

Node.js is a JavaScript runtime that lets us run JavaScript code on our computer, outside of a web browser. Node.js is required for our Socket.io chat application to work.

There are a few ways to install Node.js. The easiest way is to download the Node.js installer from the [Node.js website](https://nodejs.org/en/). Run the installer, and follow the instructions.

Once Node.js is installed, open a terminal or command prompt, and type `node -v`. This will print the version of Node.js that you have installed. You should see something like `v10.16.0`.

### Installing Socket.io

Now that we have Node.js installed, we can install Socket.io. Socket.io is a JavaScript library that makes it easy to create real-time, two-way communication applications.

There are two ways to install Socket.io. The first way is to use the [Socket.io website](https://socket.io/). The second way is to use the [npm](https://www.npmjs.com/) package manager, which is included with Node.js.

We'll be using the npm package manager to install Socket.io. To install Socket.io, open a terminal or command prompt, and type `npm install socket.io`. This will install the Socket.io library into your project.

## Creating our chat application

Now that we have our development environment set up, we can start writing code.

We'll start by creating a file named `index.html`. This will be the HTML file that our front-end web interface will be built in.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Socket.io Chat</title>
  </head>
  <body>
    <h1>Socket.io Chat</h1>
    
    <form id="message-form">
      <input type="text" id="message-input" placeholder="Enter a message...">
      <button type="submit">Send</button>
    </form>
    
    <ul id="message-list"></ul>
    
    <script src="/socket.io/socket.io.js"></script>
    <script src="https://code.jquery.com/jquery-3.4.1.min.js"></script>
    <script src="/js/index.js"></script>
  </body>
</html>
```

In our `index.html` file, we've included the Socket.io JavaScript library, and the jQuery library. We've also included our own `index.js` file, which we'll create in a moment.

Next, we'll create our `index.js` file. This is where our JavaScript code will go.

```js
$(function() {
  var socket = io();
  
  $('#message-form').submit(function(e) {
    e.preventDefault();
    
    var message = $('#message-input').val();
    
    socket.emit('message', message);
    
    $('#message-input').val('');
    
    return false;
  });
  
  socket.on('message', function(message) {
    $('#message-list').append($('<li>').text(message));
  });
});
```

In our `index.js` file, we've created a connection to our Socket.io server. We've also set up an event handler that will be called when the user submits the message form.

When the message form is submitted, we'll get the message from the message input, and emit it to our Socket.io server. We'll also clear the message input, so that the user can enter another message.

Finally, we've set up an event handler that will be called when our Socket.io server emits a message. When this happens, we'll append the message to our message list.

Now that we have our front-end web interface set up, we can start working on our back-end server.

We'll start by creating a file named `server.js`. This is where our Node.js code will go.

```js
var app = require('express')();
var http = require('http').Server(app);
var io = require('socket.io')(http);

app.get('/', function(req, res) {
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', function(socket) {
  socket.on('message', function(message) {
    io.emit('message', message);
  });
});

http.listen(3000, function() {
  console.log('listening on *:3000');
});
```

In our `server.js` file, we've required the `express` and `socket.io` libraries. We've also created an HTTP server, and a Socket.io server.

We've set up an event handler that will be called when our Socket.io server receives a message. When this happens, we'll emit the message to all connected clients.

Finally, we've set up our HTTP server to listen on port 3000.

## Running our chat application

Now that we have our chat application written, we can run it.

To run our chat application, open a terminal or command prompt, and navigate to the directory that our `server.js` file is in. Then, type `node server.js`. This will start our Node.js server.

Open a web browser, and navigate to `http://localhost:3000`. You should see our chat application. Try sending a message. You should see the message appear in your browser window.

## Conclusion

In this article, we've looked at how to build real-time applications with Socket.io. We've built a simple chat application that allows us to send and receive messages in real-time.