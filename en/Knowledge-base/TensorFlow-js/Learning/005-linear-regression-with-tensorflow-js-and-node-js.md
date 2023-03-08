---
title: 005: Linear Regression with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T07:43:36.366Z
tags: 
editor: markdown
dateCreated: 2023-02-02T07:43:31.958Z
---

- [005: Regresión lineal con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/005-linear-regression-with-tensorflow-js-and-node-js)
{.links-list}
- [005：使用 TensorFlow.js 和 Node.js 进行线性回归***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/005-linear-regression-with-tensorflow-js-and-node-js)
{.links-list}
- [005: TensorFlow.js 및 Node.js를 사용한 선형 회귀***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/005-linear-regression-with-tensorflow-js-and-node-js)
{.links-list}


# Linear Regression with TensorFlow.js and Node.js

In this post, we'll learn how to perform linear regression using TensorFlow.js and Node.js. We'll start by briefly reviewing linear regression and then we'll see how to implement it using TensorFlow.js.

## What is Linear Regression?

Linear regression is a statistical technique that is used to model the relationship between a dependent variable and one or more independent variables. The dependent variable is the variable that is being predicted, while the independent variables are the variables that are used to predict the dependent variable.

In a linear regression model, the dependent variable is a linear function of the independent variables. That is, the dependent variable is a linear function of the independent variables.

## How to Perform Linear Regression using TensorFlow.js?

TensorFlow.js is a JavaScript library for training and deploying machine learning models. It is also used for numerical computation. In this section, we will see how to use TensorFlow.js for linear regression.

We will use the following data for our linear regression example:

| X | Y |
|---|---|
| 1 | 2 |
| 2 | 4 |
| 3 | 6 |

The first step is to import the TensorFlow.js library. We can do this using the require() function:

```javascript
const tf = require('@tensorflow/tfjs');
```

Next, we need to define the independent and dependent variables. We can do this using the tf.tensor() function:

```javascript
// Define the independent variable
const x = tf.tensor([1, 2, 3], [3, 1]);

// Define the dependent variable
const y = tf.tensor([2, 4, 6], [3, 1]);
```

Now that we have defined the independent and dependent variables, we can define the linear regression model. We can do this using the tf.layers.dense() function:

```javascript
// Define the linear regression model
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));
```

The next step is to compile the linear regression model. We can do this using the tf.model.compile() function:

```javascript
// Compile the linear regression model
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});
```

Finally, we can train the linear regression model. We can do this using the tf.model.fit() function:

```javascript
// Train the linear regression model
model.fit(x, y, {epochs: 100}).then(() => {
  // Use the model to predict the value of y for x = 4
  model.predict(tf.tensor([4], [1, 1])).print();
});
```

## Conclusion

In this post, we have seen how to perform linear regression using TensorFlow.js and Node.js. We have also seen how to use the linear regression model to predict the value of a dependent variable for a given independent variable.