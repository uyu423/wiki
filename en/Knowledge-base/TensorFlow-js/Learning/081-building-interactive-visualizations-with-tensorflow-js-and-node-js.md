---
title: 081: Building Interactive Visualizations with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-03T01:44:05.592Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:44:00.875Z
---

- [081: Creación de visualizaciones interactivas con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/081-building-interactive-visualizations-with-tensorflow-js-and-node-js)
{.links-list}
- [081：使用 TensorFlow.js 和 Node.js 构建交互式可视化***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/081-building-interactive-visualizations-with-tensorflow-js-and-node-js)
{.links-list}
- [081: TensorFlow.js 및 Node.js로 대화형 시각화 구축***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/081-building-interactive-visualizations-with-tensorflow-js-and-node-js)
{.links-list}


# 081: Building Interactive Visualizations with TensorFlow.js and Node.js

In this post, we'll be looking at how to build interactive visualizations with TensorFlow.js and Node.js.

TensorFlow.js is a powerful JavaScript library for numerical computation that enables machine learning in the browser. Node.js is a JavaScript runtime that allows you to run JavaScript code outside of the browser.

Together, these two technologies can be used to build interactive visualizations that can be used to explore and analyze data.

## Getting Started

To get started, you'll need to install Node.js and TensorFlow.js.

Node.js can be downloaded and installed from the official website: https://nodejs.org/en/

TensorFlow.js can be installed using the Node.js package manager:

```
npm install @tensorflow/tfjs
```

## Hello World

Once you have Node.js and TensorFlow.js installed, you can create a simple "Hello World" program using the following code:

```javascript
// Load the TensorFlow.js library
const tf = require('@tensorflow/tfjs');

// Define a TensorFlow.js graph
tf.tensor([1, 2, 3, 4]).print();
```

Save the code above in a file named "hello.js" and run it using the Node.js runtime:

```
node hello.js
```

You should see the following output:

```
Tensor
    [[1, 2, 3, 4]]
```

 Congratulations! You've just run your first TensorFlow.js program.

## Building an Interactive Visualization

Now that we've seen how to get started with TensorFlow.js and Node.js, let's look at how to use these technologies to build an interactive visualization.

We'll be using the following libraries to build our visualization:

- TensorFlow.js: for numerical computation and machine learning
- Node.js: for running JavaScript code outside of the browser
- Express: for creating a web server
- Socket.IO: for real-time communication between the web server and the browser

Our visualization will be a simple line chart that updates in real-time.

### Defining the Data

First, let's define the data that we'll be visualizing. We'll use a TensorFlow.js graph to generate random data points.

```javascript
// Define a TensorFlow.js graph that generates random data
const data = tf.tensor(new Array(100).fill(0).map(() => Math.random()));
```

The code above defines a TensorFlow.js graph that generates 100 random data points.

### Creating the Web Server

Next, let's create a web server using Node.js and Express.

```javascript
// Load the Express.js library
const express = require('express');

// Create an Express.js app
const app = express();

// Define the port that the app will listen on
const port = 3000;

// Start the Express.js app
app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```

The code above creates an Express.js app that listens on port 3000.

### Serving the HTML Page

Now that we have our web server up and running, let's serve an HTML page that will be used to display our visualization.

```javascript
// Serve the HTML page
app.get('/', (req, res) => res.sendFile(__dirname + '/index.html'));
```

The code above defines a route that serves the HTML page when the root URL is accessed.

The HTML page should have the following contents:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>081: Building Interactive Visualizations with TensorFlow.js and Node.js</title>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.0/dist/tf.min.js"></script>
    <script src="https://cdn.socket.io/socket.io-1.4.5.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.7.3/Chart.min.js"></script>
  </head>
  <body>
    <canvas id="chart"></canvas>
    <script>
      // Your code here
    </script>
  </body>
</html>
```

The HTML page includes the following libraries:

- TensorFlow.js: for numerical computation and machine learning
- Socket.IO: for real-time communication between the web server and the browser
- Chart.js: for creating charts and graphs

The HTML page also includes a ```<canvas>``` element that will be used to display the line chart.

### Sending the Data to the Browser

Now that we have our web server up and running and we're serving the HTML page, let's send the data to the browser.

We'll use Socket.IO to establish a real-time connection between the web server and the browser.

```javascript
// Load the Socket.IO library
const io = require('socket.io')(server);

// Send the data to the browser
io.on('connection', socket => {
  setInterval(() => {
    socket.emit('data', data.toArray());
  }, 1000);
});
```

The code above uses Socket.IO to send the data to the browser every second.

### Receiving the Data in the Browser

Now that we're receiving the data in the browser, let's visualize it using Chart.js.

```javascript
// Connect to the socket.io server
const socket = io('http://localhost:3000');

// Receive the data from the server
socket.on('data', data => {
  // Visualize the data using Chart.js
  const chart = new Chart(document.getElementById('chart'), {
    type: 'line',
    data: {
      labels: data.map((_, i) => i),
      datasets: [{
        label: 'Random Data',
        data: data,
        borderColor: '#ff0000',
        fill: false
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false
    }
  });
});
```

The code above uses Chart.js to visualize the data as a line chart. The chart is updated in real-time as new data points are received.

## Conclusion

In this post, we've seen how to build interactive visualizations with TensorFlow.js and Node.js.

TensorFlow.js is a powerful JavaScript library for numerical computation that enables machine learning in the browser. Node.js is a JavaScript runtime that allows you to run JavaScript code outside of the browser.

Together, these two technologies can be used to build interactive visualizations that can be used to explore and analyze data.