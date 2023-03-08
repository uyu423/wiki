---
title: 028：使用 TensorFlow.js 和 Node.js 进行强化学习
description: 
published: true
date: 2023-02-02T13:37:04.563Z
tags: 
editor: markdown
dateCreated: 2023-02-02T13:37:02.949Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [028: Reinforcement Learning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/028-reinforcement-learning-with-tensorflow-js-and-node-js)
{.links-list}


# 028：使用 TensorFlow.js 和 Node.js 进行强化学习

在本文中，我们将向您展示如何使用 TensorFlow.js 在 Node.js 中开始强化学习。我们将使用一个简单的示例来演示如何使用流行的 Q 学习算法构建和训练模型。

强化学习是一种机器学习，它允许代理通过在环境中采取行动并接收反馈来学习。它已被用于解决各种任务，例如玩视频游戏、控制机器人和管理数据中心的资源。

Q-learning 算法是强化学习任务的流行选择。它通过学习一个价值函数来工作，该价值函数估计在给定状态下采取给定行动的预期回报。该算法然后采取最大化预期回报的行动。

要开始在 TensorFlow.js 中使用 Q-learning，我们需要安装 @tensorflow/tfjs-node 包。这个包允许我们在服务器上或在无头环境（例如网络工作者）中运行 TensorFlow.js。

```
npm install @tensorflow/tfjs-node
```

接下来，我们需要为我们的代码创建一个文件。我们称之为 q-learning.js。

在 q-learning.js 中，我们将从导入所需的包开始。

```javascript
const tf = require('@tensorflow/tfjs-node');
const _ = require('lodash');
```

我们还需要创建一些辅助函数。我们将创建的第一个辅助函数是计算数组最大值的函数。此函数将用于查找具有最高预期回报的操作。

```javascript
function argmax(array) {
  return tf.tensor1d(array).argMax().dataSync()[0];
}
```

我们将创建的下一个辅助函数是一个函数，用于计算在给定状态下采取给定操作的预期回报。该函数将使用 Q-learning 算法来估计预期回报。

```javascript
function expectedReturn(state, action, reward, discount, nextState) {
  return reward + discount * _.max(Q(nextState).dataSync());
}
```

现在我们有了辅助函数，可以开始创建 Q-learning 模型了。我们将从定义我们的代理可以采取的状态和行动开始。在此示例中，我们的代理是一个可以在四个方向（上、下、左或右）上移动的机器人。我们将每个状态表示为一个二维数组。第一维表示机器人的 x 坐标，第二维表示机器人的 y 坐标。

```javascript
const states = [[0, 0], [0, 1], [0, 2], [1, 0], [1, 1], [1, 2], [2, 0], [2, 1], [2, 2]];
const actions = ['up', 'down', 'left', 'right'];
```

接下来，我们将为 Q 值创建一个 TensorFlow.js 张量。这个张量将是一个二维数组，与我们的状态数组具有相同的维度。张量中的值将表示在给定状态下采取给定动作的预期回报。

```javascript
const Q = tf.variable(tf.zeros([states.length, actions.length]));
```

现在我们已经定义了状态和动作，我们可以开始训练我们的模型了。我们将通过循环播放一系列剧集来做到这一点。在每一集中，我们的智能体都会在某个状态下采取行动并获得奖励。然后代理将使用 Q 学习算法更新它遇到的状态-动作对的 Q 值。

```javascript
for (let episode = 0; episode < 1000; episode++) {
  // Reset the environment at the start of each episode.
  let state = [0, 0];

  // Loop over each timestep in the episode.
  for (let timestep = 0; timestep < 10; timestep++) {
    // Choose an action at random.
    let action = _.sample(actions);

    // Take the action and observe the reward.
    let reward = 1;

    // Use the Q-learning algorithm to update the Q-values.
    let discount = 0.9;
    let nextState = [0, 0];
    Q.assign(tf.tensor2d(states).transpose(), expectedReturn(state, action, reward, discount, nextState));

    // Update the state.
    state = nextState;
  }
}
```

一旦我们的模型被训练好，我们就可以用它来进行预测。为此，我们首先需要定义一个将状态转换为张量的函数。此函数将用于将我们的代理状态转换为我们的模型可以使用的格式。

```javascript
function toTensor(state) {
  return tf.tensor2d([state]);
}
```

现在我们已经定义了 toTensor 函数，我们可以使用它将代理的状态转换为张量。然后我们可以使用我们的 Q 学习模型来预测在该状态下采取每个动作的预期回报。

```javascript
let state = [0, 0];
let tensor = toTensor(state);
let prediction = Q(tensor);

console.log(prediction.dataSync());
// [ 0.0, 0.0, 0.0, 0.0 ]
```

正如我们所见，我们的模型预测在该状态下采取每个动作的预期回报为 0.0。这是因为我们的模型尚未针对此状态-动作对进行训练。

为了让我们的模型做出更好的预测，我们需要在更多数据上对其进行训练。我们可以通过增加训练循环中的情节数来做到这一点。我们还可以为折扣因子尝试不同的值。该参数控制代理对未来奖励的重视程度。较高的折扣因子将导致代理对未来奖励的评价更高。

一旦我们的模型被训练好，我们就可以用它来找到最大化预期回报的行动。为此，我们将使用我们的 argmax 辅助函数。此函数将获取一个值数组并返回最大值的索引。

```javascript
let state = [0, 0];
let tensor = toTensor(state);
let prediction = Q(tensor);

let action = argmax(prediction.dataSync());

console.log(action);
// 0
```

如我们所见，我们的模型预测具有最高预期回报的动作为 0（向上）。

这是一个简单示例，说明如何使用 Q 学习算法在 Node.js 中使用 TensorFlow.js 训练强化学习代理。该算法可用于解决各种任务，例如玩视频游戏、控制机器人和管理数据中心的资源。