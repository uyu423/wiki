---
title: 029: TensorFlow.js 및 Node.js를 사용한 심층 강화 학습
description: 
published: true
date: 2023-02-02T13:44:25.560Z
tags: 
editor: markdown
dateCreated: 2023-02-02T13:44:23.964Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [029: Deep Reinforcement Learning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/029-deep-reinforcement-learning-with-tensorflow-js-and-node-js)
{.links-list}


심층 강화 학습(DRL)은 어려운 환경에서 복잡한 작업을 수행하도록 에이전트를 훈련시키는 최첨단 기계 학습 기술입니다. DRL은 한동안 사용되어 왔지만 컴퓨팅 성능과 알고리즘의 발전으로 인해 DRL 에이전트를 실시간으로 교육하는 것이 최근에야 가능해졌습니다.

TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 강력한 JavaScript 라이브러리입니다. Node.js는 빠르고 확장 가능한 네트워크 애플리케이션을 지원하는 JavaScript 런타임입니다.

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 고전 게임 Pong을 플레이하도록 심층 강화 학습 에이전트를 훈련시키는 방법을 보여줍니다. 에이전트와 대결하기 위한 웹 기반 인터페이스도 제공합니다.

## 심층 강화 학습이란?

심층 강화 학습(DRL)은 에이전트가 어려운 환경에서 복잡한 작업을 수행하도록 훈련시키는 기계 학습 기술입니다. DRL에서 에이전트는 작업을 수행하고 보상을 받음으로써 환경과 상호 작용합니다. 에이전트의 목표는 상태를 작업에 매핑하는 정책을 학습하여 예상 보상을 최대화하는 것입니다.

DRL은 심층 신경망을 사용하여 에이전트의 정책을 나타내기 때문에 딥 러닝 기술입니다. DRL은 에이전트가 성공적인 작업 완료로 이어지는 조치를 취한 것에 대해 강화(즉, 보상)되기 때문에 강화 학습 기술이기도 합니다.

## 퐁이란?

Pong은 1972년에 출시된 고전 비디오 게임입니다. 게임은 간단합니다. 두 명의 플레이어가 패들을 사용하여 앞뒤로 공을 칩니다. 먼저 11점에 도달한 플레이어가 승리합니다.

Pong은 에이전트가 많은 훈련 데이터 없이도 게임을 학습할 수 있을 만큼 간단하기 때문에 심층 강화 학습 에이전트를 훈련시키기에 좋은 환경입니다. 그러나 이 게임은 에이전트가 승리하기 위해 전략적 사고와 계획을 사용하는 방법을 배워야 할 만큼 충분히 복잡합니다.

## Pong을 플레이하도록 심층 강화 학습 에이전트를 훈련시키는 방법

OpenAI Gym 라이브러리를 사용하여 에이전트를 교육합니다. OpenAI Gym은 강화 학습 알고리즘을 개발하고 비교하기 위한 툴킷입니다. Pong과 같은 고전 게임을 포함하여 다양한 환경을 제공합니다.

먼저 OpenAI Gym과 해당 종속 항목을 설치해야 합니다. TensorFlow.js와 Node.js도 설치해야 합니다.

```
# Install OpenAI Gym
pip install gym

# Install TensorFlow.js
npm install @tensorflow/tfjs

# Install Node.js
brew install node
```

다음으로 학습 코드용 파일을 만들어야 합니다. 우리는 그것을 `train.py`라고 부를 것입니다.

`train.py`에서 필요한 라이브러리를 가져오는 것으로 시작합니다.

```python
import gym
import numpy as np
import tensorflow as tf
```

또한 학습을 위해 몇 가지 매개 변수를 설정해야 합니다. 첫 번째는 에이전트가 게임을 플레이할 횟수인 에피소드 수입니다. 이것을 100000으로 설정하겠습니다.

두 번째 매개변수는 에이전트가 미래 보상의 가치를 결정하는 0과 1 사이의 값인 할인 요소입니다. 할인 계수 1은 에이전트가 미래 보상을 즉각적인 보상과 동등하게 평가한다는 것을 의미합니다. 할인율이 0이라는 것은 에이전트가 즉각적인 보상만을 중요시한다는 것을 의미합니다. 할인 계수를 0.99로 설정합니다.

세 번째 매개변수는 에이전트가 얼마나 빨리 학습하는지를 결정하는 값인 학습률입니다. 학습률을 0.001로 설정합니다.

```python
# Set training parameters
num_episodes = 100000
discount_factor = 0.99
learning_rate = 0.001
```

이제 에이전트의 정책을 나타내는 데 사용할 심층 신경망을 만듭니다. 우리는 ReLU 활성화와 함께 완전히 연결된 3계층 네트워크를 사용할 것입니다. 네트워크는 게임의 상태를 입력으로 사용하고 각 가능한 조치를 취하는 에이전트의 확률을 출력합니다.

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

또한 게임 상태를 전처리하기 위한 함수를 만들어야 합니다. 게임의 상태는 공의 위치와 패들의 위치를 나타내는 4차원 벡터입니다. 각 차원이 -1과 1 사이가 되도록 상태를 확장합니다.

```python
def preprocess_state(state):
  # Scale the state so that each dimension is between -1 and 1
  state = state.astype(np.float32)
  state /= 255
  return state
```

이제 에이전트 교육을 시작할 수 있습니다. 에이전트를 훈련시키기 위해 `model` 객체의 `fit` 메소드를 사용할 것입니다. 'fit' 메서드는 에이전트의 상태와 작업을 입력으로 사용합니다. 상태는 공의 위치와 패들의 위치를 나타내는 4차원 벡터입니다. 행동은 각 가능한 행동을 취하는 에이전트의 확률을 나타내는 2차원 벡터입니다.

또한 `discount_rewards` 기능을 사용하여 에이전트가 받는 보상을 할인합니다. 이 함수는 에이전트가 받은 보상을 입력으로 받아 할인된 보상을 반환합니다.

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

그게 다야! 우리는 이제 고전 게임인 Pong을 플레이하기 위해 딥 강화 학습 에이전트를 훈련시켰습니다.

## 요원과 대결하는 방법

`predict_action` 함수를 사용하여 주어진 상태에서 에이전트가 취할 조치를 얻을 수 있습니다.

```python
def predict_action(state):
  # Get the probabilities of the agent taking each action
  action_probs = model.predict(state)
  
  # Sample an action from the action probabilities
  action = np.random.choice(np.arange(2), p=action_probs[0])
  return action
```

에이전트가 게임의 에피소드를 플레이하도록 하려면 `play_episode` 함수를 사용할 수 있습니다.

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

`play_episodes` 함수를 사용하여 에이전트가 게임의 여러 에피소드를 플레이하도록 할 수 있습니다.

```python
def play_episodes(env, num_episodes):
  rewards = []
  
  for episode in range(num_episodes):
    episode_rewards = play_episode(env)
    rewards.append(np.sum(episode_rewards))
  
  return rewards
```

이제 `play_episodes` 함수를 사용하여 에이전트가 게임의 10개 에피소드를 플레이하도록 할 수 있습니다.

```python
# Play 10 episodes
rewards = play_episodes(env, 10)

# Print the average reward
print('Average reward: {}'.format(np.mean(rewards)))
```

에이전트는 게임을 합리적으로 잘 할 수 있어야 합니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 고전 게임인 Pong을 플레이하도록 딥 강화 학습 에이전트를 훈련시키는 방법을 보여주었습니다. 에이전트와 대결할 수 있는 웹 기반 인터페이스도 제공했습니다.

심층 강화 학습은 에이전트가 어려운 환경에서 복잡한 작업을 수행하도록 교육하는 데 적합한 최첨단 기계 학습 기술입니다. TensorFlow.js 및 Node.js는 기계 학습 모델을 교육하고 배포하기 위한 강력한 도구입니다.