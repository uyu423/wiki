---
title: 029：使用 TensorFlow.js 和 Node.js 进行深度强化学习
description: 
published: true
date: 2023-02-02T13:44:25.589Z
tags: 
editor: markdown
dateCreated: 2023-02-02T13:44:23.965Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [029: Deep Reinforcement Learning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/029-deep-reinforcement-learning-with-tensorflow-js-and-node-js)
{.links-list}


深度强化学习 (DRL) 是一种前沿的机器学习技术，用于训练代理在困难环境中执行复杂任务。虽然 DRL 已经存在了一段时间，但由于计算能力和算法的进步，实时训练 DRL 代理直到最近才变得可行。

TensorFlow.js 是一个强大的 JavaScript 库，用于训练和部署机器学习模型。 Node.js 是一种 JavaScript 运行时，可实现快速且可扩展的网络应用程序。

在本文中，我们将向您展示如何使用 TensorFlow.js 和 Node.js 训练深度强化学习代理来玩经典游戏 Pong。我们还将提供一个基于 Web 的界面，用于与代理对战。

## 什么是深度强化学习？

深度强化学习 (DRL) 是一种机器学习技术，用于训练代理在困难环境中执行复杂任务。在 DRL 中，代理通过采取行动和接收奖励与其环境进行交互。代理的目标是通过学习将状态映射到动作的策略来最大化其预期奖励。

DRL 是一种深度学习技术，因为它使用深度神经网络来表示代理的策略。 DRL 也是一种强化学习技术，因为代理会因采取导致成功完成任务的行动而得到强化（即奖励）。

## 什么是傍？

Pong 是一款经典的视频游戏，于 1972 年发布。游戏很简单：两名玩家使用球拍来回击球。第一个达到 11 分的玩家获胜。

Pong 是训练深度强化学习代理的绝佳环境，因为它非常简单，代理无需大量训练数据即可学会玩游戏。然而，游戏也足够复杂，智能体必须学会运用战略思维和规划来取胜。

## 如何训练深度强化学习代理打乒乓球

我们将使用 OpenAI Gym 库来训练我们的代理。 OpenAI Gym 是一个用于开发和比较强化学习算法的工具包。它提供了多种环境，包括 Pong 等经典游戏。

首先，我们需要安装 OpenAI Gym 及其依赖项。我们还需要安装 TensorFlow.js 和 Node.js。

```
# Install OpenAI Gym
pip install gym

# Install TensorFlow.js
npm install @tensorflow/tfjs

# Install Node.js
brew install node
```

接下来，我们需要为我们的训练代码创建一个文件。我们将其称为“train.py”。

在 train.py 中，我们将从导入所需的库开始。

```python
import gym
import numpy as np
import tensorflow as tf
```

我们还需要为我们的训练设置一些参数。第一个是集数，也就是代理人玩游戏的次数。我们将其设置为 100000。

第二个参数是折扣因子，它是一个介于 0 和 1 之间的值，决定了代理对未来奖励的重视程度。折扣因子为 1 表示代理人对未来奖励的评价与即时奖励相同。折扣因子为 0 意味着代理只重视即时奖励。我们将折扣系数设置为 0.99。

第三个参数是学习率，它是一个决定代理学习速度的值。我们将学习率设置为 0.001。

```python
# Set training parameters
num_episodes = 100000
discount_factor = 0.99
learning_rate = 0.001
```

现在，我们将创建用于表示代理策略的深度神经网络。我们将使用具有 ReLU 激活功能的 3 层全连接网络。网络将把游戏状态作为输入，并输出智能体采取每个可能行动的概率。

```python
# Create the policy network
model = tf.keras.models.Sequential([
  tf.keras.layers.Dense(16, activation='relu', input_shape=(4,)),
  tf.keras.layers.Dense(16, activation='relu'),
  tf.keras.layers.Dense(2, activation='softmax')
])

# Compile the model
model.compile(loss='categorical_crossentropy',
              optimizer=tf.keras.optimizers.Adam(learning_rate),
              metrics=['accuracy'])
```

我们还需要创建一个函数来预处理游戏状态。游戏的状态是一个 4 维向量，表示球的位置和球拍的位置。我们将缩放状态，使每个维度都在 -1 和 1 之间。

```python
def preprocess_state(state):
  # Scale the state so that each dimension is between -1 and 1
  state = state.astype(np.float32)
  state /= 255
  return state
```

现在，我们可以开始训练代理了。我们将使用 `model` 对象的 `fit` 方法来训练代理。 `fit` 方法将代理的状态和动作作为输入。状态是表示球的位置和桨的位置的 4 维向量。动作是二维向量，表示代理采取每个可能动作的概率。

我们还将使用 `discount_rewards` 函数对代理收到的奖励进行折扣。该函数将代理收到的奖励作为输入并返回折扣后的奖励。

```python
# Train the agent
for episode in range(num_episodes):
  # Reset the environment
  state = env.reset()
  state = preprocess_state(state)
  done = False
  rewards = []
  
  while not done:
    # Get the probabilities of the agent taking each action
    action_probs = model.predict(state)
    
    # Sample an action from the action probabilities
    action = np.random.choice(np.arange(2), p=action_probs[0])
    
    # Take the action and get the next state and reward
    next_state, reward, done, _ = env.step(action)
    next_state = preprocess_state(next_state)
    
    # Store the reward
    rewards.append(reward)
    
    # Update the state
    state = next_state
  
  # Discount the rewards
  discounted_rewards = discount_rewards(rewards, discount_factor)
  
  # Get the loss and accuracy
  loss, accuracy = model.evaluate(state, action, verbose=0)
  
  # Print the episode number, loss, and accuracy
  print('Episode: {}, Loss: {}, Accuracy: {}'.format(episode, loss, accuracy))
```

就是这样！我们现在已经训练了一个深度强化学习代理来玩经典游戏 Pong。

## 如何对抗代理

我们可以使用 `predict_action` 函数来获取代理在给定状态下将采取的操作。

```python
def predict_action(state):
  # Get the probabilities of the agent taking each action
  action_probs = model.predict(state)
  
  # Sample an action from the action probabilities
  action = np.random.choice(np.arange(2), p=action_probs[0])
  return action
```

我们可以使用 `play_episode` 函数让代理播放游戏的一集。

```python
def play_episode(env):
  # Reset the environment
  state = env.reset()
  state = preprocess_state(state)
  done = False
  rewards = []
  
  while not done:
    # Get the action the agent will take
    action = predict_action(state)
    
    # Take the action and get the next state and reward
    next_state, reward, done, _ = env.step(action)
    next_state = preprocess_state(next_state)
    
    # Store the reward
    rewards.append(reward)
    
    # Update the state
    state = next_state
  
  return rewards
```

我们可以使用 `play_episodes` 函数让代理播放游戏的多集。

```python
def play_episodes(env, num_episodes):
  rewards = []
  
  for episode in range(num_episodes):
    episode_rewards = play_episode(env)
    rewards.append(np.sum(episode_rewards))
  
  return rewards
```

现在，我们可以使用 `play_episodes` 函数让代理播放 10 集游戏。

```python
# Play 10 episodes
rewards = play_episodes(env, 10)

# Print the average reward
print('Average reward: {}'.format(np.mean(rewards)))
```

代理人应该能够相当好地玩游戏。

## 结论

在本文中，我们向您展示了如何使用 TensorFlow.js 和 Node.js 训练深度强化学习代理来玩经典游戏 Pong。我们还提供了一个基于 Web 的界面，用于与代理对战。

深度强化学习是一种尖端的机器学习技术，非常适合训练代理在困难的环境中执行复杂的任务。 TensorFlow.js 和 Node.js 是用于训练和部署机器学习模型的强大工具。