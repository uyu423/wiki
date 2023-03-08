---
title: 099: TensorFlow.js 및 Node.js에서 강화 학습 에이전트 빌드
description: 
published: true
date: 2023-02-03T06:18:09.782Z
tags: 
editor: markdown
dateCreated: 2023-02-03T06:18:08.142Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [099: Building Reinforcement Learning Agents in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/099-building-reinforcement-learning-agents-in-tensorflow-js-and-node-js)
{.links-list}


## 099: TensorFlow.js 및 Node.js에서 강화 학습 에이전트 빌드

이 게시물에서는 TensorFlow.js 및 Node.js에서 강화 학습 에이전트를 빌드하는 방법을 알아봅니다. 강화 학습의 기본 사항을 간단히 다루는 것으로 시작하겠습니다. 그런 다음 TensorFlow.js 및 해당 종속 항목을 설치하는 방법을 살펴보겠습니다. 마지막으로 간단한 게임을 플레이하도록 강화 학습 에이전트를 훈련시키는 간단한 Node.js 스크립트를 작성합니다.

### 강화 학습이란 무엇입니까?

강화 학습은 에이전트가 환경에서 조치를 취하고 해당 조치에 대한 보상을 받음으로써 학습할 수 있도록 하는 기계 학습의 한 유형입니다. 강화 학습의 목표는 에이전트가 받는 총 보상을 최대화하는 것입니다.

강화 학습에는 두 가지 주요 유형이 있습니다.

- **이산 강화 학습**: 이 유형의 강화 학습에서 에이전트는 제한된 수의 작업만 수행할 수 있습니다.
- **지속적인 강화 학습**: 이 유형의 강화 학습에서는 에이전트가 무한한 수의 작업을 수행할 수 있습니다.

이 게시물에서는 이산 강화 학습에 중점을 둘 것입니다.

### TensorFlow.js 및 종속 항목 설정

강화 학습 에이전트 구축을 시작하기 전에 TensorFlow.js 및 해당 종속 항목을 설치해야 합니다.

먼저 Node.js를 설치해야 합니다. Node.js는 웹 브라우저 외부에서 JavaScript 코드를 실행할 수 있게 해주는 JavaScript 런타임입니다.

둘째, TensorFlow.js Node.js API를 설치해야 합니다. TensorFlow.js Node.js API를 사용하면 Node.js 환경에서 TensorFlow.js를 사용할 수 있습니다.

셋째, TensorFlow.js용 강화 학습 라이브러리를 설치해야 합니다. TensorFlow.js용 강화 학습 라이브러리를 사용하면 TensorFlow.js에서 강화 학습 에이전트를 구축할 수 있습니다.

넷째, 게임 엔진을 설치해야 합니다. 이 게시물에서는 Simple Game Engine을 사용합니다. Simple Game Engine은 강화 학습 에이전트를 쉽게 개발하고 테스트할 수 있는 경량 게임 엔진입니다.

마지막으로 텍스트 편집기를 설치해야 합니다. 이 게시물에서는 Visual Studio Code를 사용합니다. Visual Studio Code는 Microsoft의 무료 오픈 소스 텍스트 편집기입니다.

### 강화 학습 에이전트를 훈련시키는 Node.js 스크립트 작성

이제 TensorFlow.js와 해당 종속 항목이 설치되었으므로 강화 학습 에이전트를 교육하는 Node.js 스크립트를 작성할 수 있습니다.

먼저 설치한 종속성을 요구해야 합니다. TensorFlow.js Node.js API, TensorFlow.js용 강화 학습 라이브러리 및 Simple Game Engine이 필요합니다.

```javascript
const tf = require('@tensorflow/tfjs-node');
const rl = require('@tensorflow-models/rl');
const { SimpleGameEngine } = require('simple-game-engine');
```

다음으로 에이전트가 플레이할 게임을 정의해야 합니다. SimpleGameEngine 클래스의 새 인스턴스를 생성하여 이를 수행합니다.

```javascript
const game = new SimpleGameEngine();
```

SimpleGameEngine 클래스에는 게임을 정의하는 데 사용할 수 있는 여러 메서드가 있습니다. 이 예제에서는 addEntity() 메서드를 사용하여 플레이어를 게임에 추가합니다.

```javascript
game.addEntity({
  id: 'player',
  x: 0,
  y: 0,
  width: 10,
  height: 10
});
```

또한 addEntity() 메서드를 사용하여 게임에 장애물을 추가할 수 있습니다.

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

이제 게임을 정의했으므로 게임의 규칙을 정의해야 합니다. 이 예에서 게임의 목표는 장애물을 피하고 레벨의 끝에 도달하는 것입니다. 레벨은 폭이 50단위이고 플레이어는 레벨의 왼쪽에서 시작합니다. 플레이어는 왼쪽, 오른쪽, 위 또는 아래로 이동할 수 있습니다. 플레이어가 장애물과 충돌하면 게임이 종료됩니다. 플레이어가 레벨의 오른쪽에 도달하면 게임이 종료되고 플레이어는 100의 보상을 받습니다.

```javascript
game.setRules({
  win: ['atXPos', 'player', 50],
  lose: ['collides', 'player', ['obstacle1', 'obstacle2']],
  endOnWin: true
});
```

setRules() 메서드를 사용하여 게임에 대한 다른 규칙을 정의할 수도 있습니다. 예를 들어 setRules() 메서드를 사용하여 게임에 대한 시간 제한을 정의할 수 있습니다.

이제 게임을 정의했으므로 환경을 정의해야 합니다. 환경은 에이전트와 게임 간의 인터페이스입니다. 이 예에서는 TensorFlow.js용 강화 학습 라이브러리의 SimpleGameEngineEnvironment 클래스를 사용합니다.

```javascript
const environment = new rl.SimpleGameEngineEnvironment(game);
```

SimpleGameEngineEnvironment 클래스에는 환경과 상호 작용하는 데 사용할 수 있는 여러 메서드가 있습니다. 이 예제에서는 reset() 메서드를 사용하여 환경을 재설정하고 step() 메서드를 사용하여 환경에서 단계를 수행합니다.

```javascript
environment.reset();

while (!environment.isDone()) {
  const action = environment.actionSpace.sample();
  environment.step(action);
}
```

actionSpace 속성은 에이전트가 수행할 수 있는 모든 가능한 작업을 포함하는 공간입니다. 이 예제에서는 sample() 메서드를 사용하여 작업 공간에서 작업을 무작위로 샘플링합니다.

이제 환경을 정의했으므로 에이전트를 정의해야 합니다. 에이전트는 에이전트를 훈련하는 데 사용할 강화 학습 알고리즘입니다. 이 예에서는 TensorFlow.js용 강화 학습 라이브러리의 DQN() 메서드를 사용합니다.

```javascript
const agent = new rl.DQN({
  environment,
  numEpisodes: 100,
  trainInterval: 10
});
```

DQN() 메서드는 여러 옵션을 인수로 사용합니다. 이 예에서는 numEpisodes 옵션을 사용하여 에이전트가 훈련할 에피소드 수를 지정합니다. 또한 trainInterval 옵션을 사용하여 에이전트를 훈련시키려는 간격을 지정합니다.

이제 에이전트를 정의했으므로 에이전트를 교육해야 합니다. 에이전트에서 train() 메서드를 호출하여 이를 수행합니다.

```javascript
agent.train();
```

에이전트가 훈련되면 save() 메서드를 사용하여 훈련된 에이전트를 저장할 수 있습니다.

```javascript
agent.save('path/to/agent');
```

load() 메서드를 사용하여 훈련된 에이전트를 로드할 수도 있습니다.

```javascript
agent.load('path/to/agent');
```

### 결론

이 게시물에서는 TensorFlow.js 및 Node.js에서 강화 학습 에이전트를 빌드하는 방법을 배웠습니다. TensorFlow.js와 해당 종속 항목을 설치하는 방법을 살펴보았습니다. 간단한 게임을 플레이하도록 강화 학습 에이전트를 훈련시키는 간단한 Node.js 스크립트도 작성했습니다.