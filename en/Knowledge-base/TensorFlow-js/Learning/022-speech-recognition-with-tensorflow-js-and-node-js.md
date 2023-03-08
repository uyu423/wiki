---
title: 022: Speech Recognition with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T12:04:39.108Z
tags: 
editor: markdown
dateCreated: 2023-02-02T12:04:34.685Z
---

- [022: Reconocimiento de voz con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/022-speech-recognition-with-tensorflow-js-and-node-js)
{.links-list}
- [022：使用 TensorFlow.js 和 Node.js 进行语音识别***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/022-speech-recognition-with-tensorflow-js-and-node-js)
{.links-list}
- [022: TensorFlow.js 및 Node.js를 사용한 음성 인식***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/022-speech-recognition-with-tensorflow-js-and-node-js)
{.links-list}


# 022: Speech Recognition with TensorFlow.js and Node.js

In this post, we'll be looking at how to use TensorFlow.js and Node.js to build a speech recognition system.

We'll start by looking at how to setup the environment, then we'll get into the code.

## Setting up the environment

The first thing we need to do is install TensorFlow.js. We can do that with the following command:

```
npm install @tensorflow/tfjs
```

Once that's done, we need to install the Node.js bindings for TensorFlow.js. We can do that with the following command:

```
npm install @tensorflow/tfjs-node
```

With that out of the way, we can now move on to the code.

## The code

We'll start by loading the TensorFlow.js library and the Node.js bindings. We can do that with the following code:

```javascript
const tf = require('@tensorflow/tfjs');
require('@tensorflow/tfjs-node');
```

Next, we'll need to load the speech recognition library. We can do that with the following code:

```javascript
const speech = require('@tensorflow-models/speech-commands');
```

With that out of the way, we can now move on to the fun part: the code.

We'll start by creating a new speech recognition model. We can do that with the following code:

```javascript
const model = speech.createModel();
```

Next, we'll need to train the model. We can do that with the following code:

```javascript
model.train({
  fileNames: [
    'file1.wav',
    'file2.wav',
    'file3.wav',
  ],
  labels: [
    'label1',
    'label2',
    'label3',
  ]
});
```

Once the model is trained, we can now use it to recognize speech. We can do that with the following code:

```javascript
model.recognize(audio, (err, result) => {
  if (err) {
    console.error(err);
  } else {
    console.log(result);
  }
});
```

And that's it! You now have a working speech recognition system.

## Conclusion

In this post, we've seen how to use TensorFlow.js and Node.js to build a speech recognition system. We've started by looking at how to setup the environment, then we've gotten into the code.

If you're interested in learning more, I recommend checking out the following resources:

- The official TensorFlow.js documentation: https://js.tensorflow.org/
- The official Node.js bindings for TensorFlow.js documentation: https://js.tensorflow.org/tfjs-node/
- The official speech recognition library documentation: https://js.tensorflow.org/speech-commands/