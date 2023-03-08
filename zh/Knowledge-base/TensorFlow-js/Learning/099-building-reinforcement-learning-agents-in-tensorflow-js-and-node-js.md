---
title: 099：在 TensorFlow.js 和 Node.js 中构建强化学习代理
description: 
published: true
date: 2023-02-03T06:18:09.758Z
tags: 
editor: markdown
dateCreated: 2023-02-03T06:18:08.148Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [099: Building Reinforcement Learning Agents in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/099-building-reinforcement-learning-agents-in-tensorflow-js-and-node-js)
{.links-list}


## 099：在 TensorFlow.js 和 Node.js 中构建强化学习代理

在本文中，我们将学习如何在 TensorFlow.js 和 Node.js 中构建强化学习代理。我们将从简要介绍强化学习的基础知识开始。然后，我们将了解如何安装 TensorFlow.js 及其依赖项。最后，我们将编写一个简单的 Node.js 脚本来训练强化学习代理玩一个简单的游戏。

### 什么是强化学习？

强化学习是一种机器学习，它使代理能够通过在环境中采取行动并从他们的行动中获得奖励来学习。强化学习的目标是最大化代理收到的总奖励。

强化学习主要有两种类型：

- **离散强化学习**：在这种类型的强化学习中，代理只能采取有限数量的动作。
- **连续强化学习**：在这种类型的强化学习中，代理可以采取无限多的动作。

在这篇文章中，我们将重点关注离散强化学习。

### 设置 TensorFlow.js 及其依赖项

在开始构建强化学习代理之前，我们需要安装 TensorFlow.js 及其依赖项。

首先，我们需要安装 Node.js。 Node.js 是一个 JavaScript 运行时，它使我们能够在 Web 浏览器之外运行 JavaScript 代码。

其次，我们需要安装 TensorFlow.js Node.js API。 TensorFlow.js Node.js API 使我们能够在 Node.js 环境中使用 TensorFlow.js。

第三，我们需要为 TensorFlow.js 安装强化学习库。 TensorFlow.js 的强化学习库使我们能够在 TensorFlow.js 中构建强化学习代理。

第四，我们需要安装一个游戏引擎。在本文中，我们将使用 Simple Game Engine。 Simple Game Engine 是一种轻量级游戏引擎，可以轻松开发和测试强化学习代理。

最后，我们需要安装一个文本编辑器。在本文中，我们将使用 Visual Studio Code。 Visual Studio Code 是 Microsoft 的免费开源文本编辑器。

### 编写训练强化学习代理的 Node.js 脚本

现在我们已经安装了 TensorFlow.js 及其依赖项，我们可以编写一个 Node.js 脚本来训练强化学习代理。

首先，我们需要要求我们安装的依赖项。我们需要 TensorFlow.js Node.js API、TensorFlow.js 的强化学习库和简单游戏引擎。

```javascript
const tf = require('@tensorflow/tfjs-node');
const rl = require('@tensorflow-models/rl');
const { SimpleGameEngine } = require('simple-game-engine');
```

接下来，我们需要定义代理将玩的游戏。我们通过创建 SimpleGameEngine 类的新实例来完成此操作。

```javascript
const game = new SimpleGameEngine();
```

SimpleGameEngine 类有许多我们可以用来定义游戏的方法。在此示例中，我们将使用 addEntity() 方法将玩家添加到游戏中。

```javascript
game.addEntity({
  id: 'player',
  x: 0,
  y: 0,
  width: 10,
  height: 10
});
```

我们还可以使用 addEntity() 方法为游戏添加障碍。

```javascript
game.addEntity({
  id: 'obstacle1',
  x: 50,
  y: 50,
  width: 10,
  height: 10
});

game.addEntity({
  id: 'obstacle2',
  x: 100,
  y: 100,
  width: 10,
  height: 10
});
```

现在我们已经定义了游戏，我们需要定义游戏规则。在此示例中，游戏的目标是避开障碍物并到达关卡的尽头。关卡有 50 个单位宽，玩家从关卡的左侧开始。玩家可以向左、向右、向上或向下移动。如果玩家与障碍物发生碰撞，则游戏结束。如果玩家到达关卡的右侧，则游戏结束，玩家将获得 100 的奖励。

```javascript
game.setRules({
  win: ['atXPos', 'player', 50],
  lose: ['collides', 'player', ['obstacle1', 'obstacle2']],
  endOnWin: true
});
```

我们还可以使用 setRules() 方法为游戏定义其他规则。例如，我们可以使用 setRules() 方法来定义游戏的时间限制。

现在我们已经定义了游戏，我们需要定义环境。环境是代理和游戏之间的接口。在此示例中，我们将使用 TensorFlow.js 强化学习库中的 SimpleGameEngineEnvironment 类。

```javascript
const environment = new rl.SimpleGameEngineEnvironment(game);
```

SimpleGameEngineEnvironment 类有许多我们可以用来与环境交互的方法。在此示例中，我们将使用 reset() 方法重置环境，并使用 step() 方法在环境中采取步骤。

```javascript
environment.reset();

while (!environment.isDone()) {
  const action = environment.actionSpace.sample();
  environment.step(action);
}
```

actionSpace 属性是一个空间，其中包含代理可以采取的所有可能操作。在这个例子中，我们使用 sample() 方法从动作空间中随机抽取一个动作。

现在我们已经定义了环境，我们需要定义代理。代理是我们将用来训练代理的强化学习算法。在此示例中，我们将使用 TensorFlow.js 强化学习库中的 DQN() 方法。

```javascript
const agent = new rl.DQN({
  environment,
  numEpisodes: 100,
  trainInterval: 10
});
```

DQN() 方法采用多个选项作为参数。在此示例中，我们使用 numEpisodes 选项指定我们希望代理进行训练的剧集数。我们还使用 trainInterval 选项来指定我们希望代理训练的时间间隔。

现在我们已经定义了代理，我们需要训练代理。我们通过调用代理上的 train() 方法来完成此操作。

```javascript
agent.train();
```

代理经过训练后，我们可以使用 save() 方法保存经过训练的代理。

```javascript
agent.save('path/to/agent');
```

我们还可以使用 load() 方法来加载经过训练的代理。

```javascript
agent.load('path/to/agent');
```

### 结论

在本文中，我们学习了如何在 TensorFlow.js 和 Node.js 中构建强化学习代理。我们已经了解了如何安装 TensorFlow.js 及其依赖项。我们还编写了一个简单的 Node.js 脚本，用于训练强化学习代理玩一个简单的游戏。