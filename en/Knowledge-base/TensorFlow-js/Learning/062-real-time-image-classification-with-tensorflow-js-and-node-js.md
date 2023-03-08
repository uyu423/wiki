---
title: 062: Real-Time Image Classification with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T21:36:48.095Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:36:43.518Z
---

- [062: Clasificación de imágenes en tiempo real con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/062-real-time-image-classification-with-tensorflow-js-and-node-js)
{.links-list}
- [062：使用 TensorFlow.js 和 Node.js 进行实时图像分类***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/062-real-time-image-classification-with-tensorflow-js-and-node-js)
{.links-list}
- [062: TensorFlow.js 및 Node.js를 사용한 실시간 이미지 분류***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/062-real-time-image-classification-with-tensorflow-js-and-node-js)
{.links-list}


# Real-Time Image Classification with TensorFlow.js and Node.js

In this post, we'll be looking at how to build a real-time image classification app using TensorFlow.js and Node.js.

TensorFlow.js is a powerful tool for creating machine learning models in JavaScript. Node.js is a JavaScript runtime that allows you to run JavaScript on the server.

 Together, these two technologies can be used to build powerful real-time image classification applications.

## Installing TensorFlow.js

The first step is to install TensorFlow.js. You can do this using the Node Package Manager (NPM):

```
npm install @tensorflow/tfjs
```

## Installing Node.js

If you don't already have Node.js installed, you can do so by following the instructions on the Node.js website: https://nodejs.org/en/

## Building the Model

Now that we have TensorFlow.js and Node.js installed, we can start building our image classification model.

We'll be using theMobileNet model. MobileNet is a pre-trained model that has been trained on a large dataset of images.

To use the MobileNet model, we first need to load it into TensorFlow.js:

```javascript
const tf = require('@tensorflow/tfjs');

const mobilenet = require('@tensorflow-models/mobilenet');

async function loadModel() {
  const model = await mobilenet.load();
  return model;
}
```

Once the model is loaded, we can use it to classify images.

The classifyImage() function below takes an image as input and returns the top 5 predictions:

```javascript
async function classifyImage(image) {
  const model = await loadModel();
  const predictions = await model.classify(image);
  return predictions;
}
```

## Serving the Model

Now that we have our image classification model built, we need to serve it using Node.js.

We'll be using the Express web framework. Express is a popular web framework for Node.js.

To install Express, run the following command:

```
npm install express
```

Once Express is installed, we can create a file called server.js and add the following code:

```javascript
const express = require('express');
const app = express();

app.use(express.static('public'));

app.get('/classify', async (req, res) => {
  const image = req.query.image;
  const predictions = await classifyImage(image);
  res.json(predictions);
});

app.listen(3000, () => console.log('Server listening on port 3000!'));
```

The code above does the following:

- Serves static files from the public directory
- Creates an endpoint (/classify) that takes an image URL as a query parameter
- Uses the classifyImage() function to classify the image
- Returns the top 5 predictions as JSON

## Building the Front-end

Now that we have our Node.js server up and running, we can start building the front-end of our application.

We'll be using React. React is a popular JavaScript library for building user interfaces.

To install React, run the following command:

```
npm install react react-dom
```

Once React is installed, we can create a file called App.js and add the following code:

```javascript
import React, { useState, useEffect } from 'react';
import './App.css';

function App() {
  const [image, setImage] = useState(null);
  const [predictions, setPredictions] = useState([]);

  useEffect(() => {
    async function fetchPredictions() {
      const response = await fetch('/classify?image=' + image);
      const predictions = await response.json();
      setPredictions(predictions);
    }
    if (image) {
      fetchPredictions();
    }
  }, [image]);

  const onSelectFile = e => {
    if (e.target.files && e.target.files.length > 0) {
      const reader = new FileReader();
      reader.onload = () => setImage(reader.result);
      reader.readAsDataURL(e.target.files[0]);
    }
  };

  return (
    <div className="App">
      <h1>Real-Time Image Classification</h1>
      <p>
        Select an image to classify:
      </p>
      <input type="file" accept="image/*" onChange={onSelectFile} />
      {predictions.length > 0 && (
        <div className="predictions">
          <h2>Predictions</h2>
          {predictions.map((prediction, i) => (
            <div key={i}>
              <div className="prediction-label">{prediction.className}</div>
              <div className="prediction-confidence">{prediction.probability.toFixed(2)}</div>
            </div>
          ))}
        </div>
      )}
    </div>
  );
}

export default App;
```

The code above does the following:

- Renders a file input field that allows the user to select an image
- When an image is selected, the image is uploaded to the server and the predictions are fetched
- The predictions are then displayed on the page

## Running the App

Now that we have our front-end and back-end code complete, we can run the app.

First, start the Node.js server by running the following command:

```
node server.js
```

Then, open the following URL in your browser: http://localhost:3000

You should now see the image classification app up and running!