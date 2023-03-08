---
title: 028: TensorFlow.js 및 Node.js를 사용한 강화 학습
description: 
published: true
date: 2023-02-02T13:37:04.506Z
tags: 
editor: markdown
dateCreated: 2023-02-02T13:37:02.948Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [028: Reinforcement Learning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/028-reinforcement-learning-with-tensorflow-js-and-node-js)
{.links-list}


# 028: TensorFlow.js 및 Node.js를 사용한 강화 학습

이 게시물에서는 TensorFlow.js를 사용하여 Node.js에서 강화 학습을 시작하는 방법을 보여줍니다. 인기 있는 Q-러닝 알고리즘을 사용하여 모델을 구축하고 교육하는 방법을 보여주기 위해 간단한 예를 사용할 것입니다.

강화 학습은 에이전트가 환경에서 조치를 취하고 피드백을 받아 학습할 수 있도록 하는 기계 학습의 한 유형입니다. 비디오 게임, 로봇 제어, 데이터 센터의 리소스 관리와 같은 다양한 작업을 해결하는 데 사용되었습니다.

Q-러닝 알고리즘은 강화 학습 작업에 널리 사용되는 선택입니다. 주어진 상태에서 주어진 행동을 취할 때 기대되는 수익을 추정하는 가치 함수를 학습함으로써 작동합니다. 그런 다음 알고리즘은 예상 수익을 최대화하는 조치를 취합니다.

TensorFlow.js에서 Q-러닝을 시작하려면 @tensorflow/tfjs-node 패키지를 설치해야 합니다. 이 패키지를 사용하면 서버 또는 웹 작업자와 같은 헤드리스 환경에서 TensorFlow.js를 실행할 수 있습니다.

```
npm install @tensorflow/tfjs-node
```

다음으로 코드용 파일을 만들어야 합니다. 우리는 그것을 q-learning.js라고 부를 것입니다.

q-learning.js에서 필요한 패키지를 가져오는 것으로 시작하겠습니다.

```javascript
const tf = require('@tensorflow/tfjs-node');
const _ = require('lodash');
```

또한 몇 가지 도우미 함수를 만들어야 합니다. 우리가 만들 첫 번째 도우미 함수는 배열의 최대값을 계산하는 함수입니다. 이 함수는 예상 수익이 가장 높은 작업을 찾는 데 사용됩니다.

```javascript
function argmax(array) {
  return tf.tensor1d(array).argMax().dataSync()[0];
}
```

우리가 만들 다음 헬퍼 함수는 주어진 상태에서 주어진 행동을 취할 때 예상되는 수익을 계산하는 함수입니다. 이 기능은 Q-러닝 알고리즘을 사용하여 예상 수익을 추정합니다.

```javascript
function expectedReturn(state, action, reward, discount, nextState) {
  return reward + discount * _.max(Q(nextState).dataSync());
}
```

도우미 기능이 있으므로 이제 Q-러닝 모델을 만들 수 있습니다. 에이전트가 취할 수 있는 상태와 조치를 정의하는 것으로 시작하겠습니다. 이 예에서 에이전트는 네 방향(위, 아래, 왼쪽 또는 오른쪽)으로 이동할 수 있는 로봇입니다. 우리는 각 상태를 2차원 배열로 나타낼 것입니다. 첫 번째 차원은 로봇의 x 좌표를 나타내고 두 번째 차원은 로봇의 y 좌표를 나타냅니다.

```javascript
const states = [[0, 0], [0, 1], [0, 2], [1, 0], [1, 1], [1, 2], [2, 0], [2, 1], [2, 2]];
const actions = ['up', 'down', 'left', 'right'];
```

다음으로 Q-값에 대한 TensorFlow.js 텐서를 생성합니다. 이 텐서는 상태 배열과 같은 차원의 2차원 배열이 됩니다. 텐서의 값은 주어진 상태에서 주어진 행동을 취할 때 예상되는 수익을 나타냅니다.

```javascript
const Q = tf.variable(tf.zeros([states.length, actions.length]));
```

이제 상태와 작업이 정의되었으므로 모델 학습을 시작할 수 있습니다. 일련의 에피소드를 반복하여 이 작업을 수행합니다. 각 에피소드에서 에이전트는 상태에서 조치를 취하고 보상을 받습니다. 그런 다음 에이전트는 Q-학습 알고리즘을 사용하여 만난 상태-행동 쌍에 대한 Q-값을 업데이트합니다.

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

모델이 학습되면 모델을 사용하여 예측할 수 있습니다. 이렇게 하려면 먼저 상태를 텐서로 변환하는 함수를 정의해야 합니다. 이 함수는 에이전트의 상태를 모델에서 사용할 수 있는 형식으로 변환하는 데 사용됩니다.

```javascript
function toTensor(state) {
  return tf.tensor2d([state]);
}
```

이제 toTensor 함수를 정의했으므로 이를 사용하여 에이전트의 상태를 텐서로 변환할 수 있습니다. 그런 다음 Q-러닝 모델을 사용하여 상태에서 각 작업을 수행할 때 예상되는 수익을 예측할 수 있습니다.

```javascript
let state = [0, 0];
let tensor = toTensor(state);
let prediction = Q(tensor);

console.log(prediction.dataSync());
// [ 0.0, 0.0, 0.0, 0.0 ]
```

우리가 볼 수 있듯이 우리 모델은 상태에서 각 행동을 취할 때 기대되는 수익이 0.0이라고 예측하고 있습니다. 이는 모델이 아직 이 상태-행동 쌍에 대해 훈련되지 않았기 때문입니다.

모델이 더 나은 예측을 하도록 하려면 더 많은 데이터로 모델을 훈련해야 합니다. 훈련 루프의 에피소드 수를 늘려서 이를 수행할 수 있습니다. 할인 요인에 대해 다른 값을 시도할 수도 있습니다. 이 매개변수는 에이전트가 미래 보상을 평가하는 정도를 제어합니다. 할인 계수가 높을수록 에이전트는 미래 보상의 가치를 더 높이 평가하게 됩니다.

모델이 학습되면 모델을 사용하여 기대 수익을 최대화하는 작업을 찾을 수 있습니다. 이를 위해 argmax 헬퍼 함수를 사용합니다. 이 함수는 값의 배열을 취하고 최대값의 인덱스를 반환합니다.

```javascript
let state = [0, 0];
let tensor = toTensor(state);
let prediction = Q(tensor);

let action = argmax(prediction.dataSync());

console.log(action);
// 0
```

보시다시피, 우리 모델은 가장 높은 기대 수익을 가진 행동이 0(위)이라고 예측하고 있습니다.

TensorFlow.js를 사용하여 Node.js에서 강화 학습 에이전트를 교육하기 위해 Q-러닝 알고리즘을 사용하는 방법에 대한 간단한 예입니다. 이 알고리즘은 비디오 게임, 로봇 제어, 데이터 센터의 리소스 관리와 같은 다양한 작업을 해결하는 데 사용할 수 있습니다.