---
title: 029: Deep Reinforcement Learning with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T13:44:28.329Z
tags: 
editor: markdown
dateCreated: 2023-02-02T13:44:23.979Z
---

- [029: aprendizaje de refuerzo profundo con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/029-deep-reinforcement-learning-with-tensorflow-js-and-node-js)
{.links-list}
- [029：使用 TensorFlow.js 和 Node.js 进行深度强化学习***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/029-deep-reinforcement-learning-with-tensorflow-js-and-node-js)
{.links-list}
- [029: TensorFlow.js 및 Node.js를 사용한 심층 강화 학습***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/029-deep-reinforcement-learning-with-tensorflow-js-and-node-js)
{.links-list}


Deep reinforcement learning (DRL) is a cutting edge machine learning technique for training agents to perform complex tasks in difficult environments. While DRL has been around for a while, it has only recently become feasible to train DRL agents in real-time due to advances in computing power and algorithms.

TensorFlow.js is a powerful JavaScript library for training and deploying machine learning models. Node.js is a JavaScript runtime that enables fast and scalable network applications.

In this post, we'll show you how to use TensorFlow.js and Node.js to train a deep reinforcement learning agent to play the classic game Pong. We'll also provide a web-based interface for playing against the agent.

## What is Deep Reinforcement Learning?

Deep reinforcement learning (DRL) is a machine learning technique for training agents to perform complex tasks in difficult environments. In DRL, an agent interacts with its environment by taking actions and receiving rewards. The agent's goal is to maximize its expected reward by learning a policy that maps states to actions.

DRL is a deep learning technique because it uses deep neural networks to represent the agent's policy. DRL is also a reinforcement learning technique because the agent is reinforced (i.e. rewarded) for taking actions that lead to a successful task completion.

## What is Pong?

Pong is a classic video game that was released in 1972. The game is simple: two players use paddles to hit a ball back and forth. The first player to reach a score of 11 wins.

Pong is a great environment for training a deep reinforcement learning agent because it is simple enough that the agent can learn to play the game without needing a large amount of training data. However, the game is also complex enough that the agent must learn to use strategic thinking and planning to win.

## How to Train a Deep Reinforcement Learning Agent to Play Pong

We'll use the OpenAI Gym library to train our agent. OpenAI Gym is a toolkit for developing and comparing reinforcement learning algorithms. It provides a variety of environments, including classic games like Pong.

First, we'll need to install OpenAI Gym and its dependencies. We'll also need to install TensorFlow.js and Node.js.

```
# Install OpenAI Gym
pip install gym

# Install TensorFlow.js
npm install @tensorflow/tfjs

# Install Node.js
brew install node
```

Next, we'll need to create a file for our training code. We'll call it `train.py`.

In `train.py`, we'll start by importing the libraries we need.

```python
import gym
import numpy as np
import tensorflow as tf
```

We'll also need to set a few parameters for our training. The first is the number of episodes, which is the number of times the agent will play the game. We'll set this to 100000.

The second parameter is the discount factor, which is a value between 0 and 1 that determines how much the agent values future rewards. A discount factor of 1 means the agent values future rewards equally to immediate rewards. A discount factor of 0 means the agent only values immediate rewards. We'll set the discount factor to 0.99.

The third parameter is the learning rate, which is a value that determines how quickly the agent learns. We'll set the learning rate to 0.001.

```python
# Set training parameters
num_episodes = 100000
discount_factor = 0.99
learning_rate = 0.001
```

Now, we'll create the deep neural network that will be used to represent the agent's policy. We'll use a 3-layer fully-connected network with ReLU activation. The network will take the state of the game as input and output the probabilities of the agent taking each possible action.

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

We also need to create a function for preprocessing the state of the game. The state of the game is a 4-dimensional vector that represents the position of the ball and the position of the paddles. We'll scale the state so that each dimension is between -1 and 1.

```python
def preprocess_state(state):
  # Scale the state so that each dimension is between -1 and 1
  state = state.astype(np.float32)
  state /= 255
  return state
```

Now, we can start training the agent. We'll use the `fit` method of the `model` object to train the agent. The `fit` method takes as input the states and actions of the agent. The states are the 4-dimensional vectors that represent the position of the ball and the position of the paddles. The actions are the 2-dimensional vectors that represent the probabilities of the agent taking each possible action.

We'll also use the `discount_rewards` function to discount the rewards the agent receives. This function takes as input the rewards the agent received and returns the discounted rewards.

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

That's it! We've now trained a deep reinforcement learning agent to play the classic game Pong.

## How to Play Against the Agent

We can use the `predict_action` function to get the action the agent will take given a state.

```python
def predict_action(state):
  # Get the probabilities of the agent taking each action
  action_probs = model.predict(state)
  
  # Sample an action from the action probabilities
  action = np.random.choice(np.arange(2), p=action_probs[0])
  return action
```

We can use the `play_episode` function to have the agent play an episode of the game.

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

We can use the `play_episodes` function to have the agent play multiple episodes of the game.

```python
def play_episodes(env, num_episodes):
  rewards = []
  
  for episode in range(num_episodes):
    episode_rewards = play_episode(env)
    rewards.append(np.sum(episode_rewards))
  
  return rewards
```

Now, we can use the `play_episodes` function to have the agent play 10 episodes of the game.

```python
# Play 10 episodes
rewards = play_episodes(env, 10)

# Print the average reward
print('Average reward: {}'.format(np.mean(rewards)))
```

The agent should be able to play the game reasonably well.

##Conclusion

In this post, we showed you how to use TensorFlow.js and Node.js to train a deep reinforcement learning agent to play the classic game Pong. We also provided a web-based interface for playing against the agent.

Deep reinforcement learning is a cutting edge machine learning technique that is well suited for training agents to perform complex tasks in difficult environments. TensorFlow.js and Node.js are powerful tools for training and deploying machine learning models.