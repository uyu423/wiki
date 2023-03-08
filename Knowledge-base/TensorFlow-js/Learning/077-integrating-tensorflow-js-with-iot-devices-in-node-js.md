---
title: 077: TensorFlow.js를 Node.js에서 IoT 장치와 통합
description: 
published: true
date: 2023-02-03T00:43:19.750Z
tags: 
editor: markdown
dateCreated: 2023-02-03T00:43:18.156Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [077: Integrating TensorFlow.js with IoT Devices in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/077-integrating-tensorflow-js-with-iot-devices-in-node-js)
{.links-list}


# TensorFlow.js를 Node.js에서 IoT 장치와 통합

TensorFlow.js는 브라우저에서 기계 학습 모델을 개발하고 교육하는 데 사용할 수 있는 오픈 소스 라이브러리입니다. IoT 장치에서 이러한 모델을 실행하는 데에도 사용할 수 있습니다. 이 게시물에서는 Node.js와 함께 TensorFlow.js를 사용하여 IoT 장치를 제어하는 데 사용할 수 있는 애플리케이션을 개발하는 방법을 보여줍니다.

## 전제 조건

시작하기 전에 필요한 몇 가지 사항이 있습니다.

- 자바스크립트에 대한 기본적인 이해
- 컴퓨터에 설치된 Node.js
- 텍스트 편집기([Visual Studio Code](https://code.visualstudio.com/) 권장)

## 시작하기

[TensorFlow.js](https://js.tensorflow.org/) 라이브러리를 사용하여 애플리케이션을 개발할 것입니다. 가장 먼저 해야 할 일은 프로젝트에 TensorFlow.js 라이브러리를 포함하는 것입니다. HTML 파일의 헤드에 다음 코드 줄을 추가하여 이를 수행할 수 있습니다.

```
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.0"> </script>
```

이제 프로젝트에 TensorFlow.js 라이브러리가 포함되었으므로 애플리케이션 개발을 시작할 수 있습니다.

## 애플리케이션 개발

우리의 응용 프로그램은 사전 훈련된 모델을 사용하여 IoT 장치를 제어하는 간단한 응용 프로그램입니다. 가장 먼저 해야 할 일은 모델을 로드하는 것입니다. tf.loadModel() 함수를 사용하여 이를 수행할 수 있습니다.

```javascript
const model = await tf.loadModel('https://my-model-url');
```

다음으로 모델의 입력과 출력을 정의해야 합니다. tf.layers.input() 및 tf.layers.dense() 함수를 사용하여 이를 수행할 수 있습니다.

```javascript
const input = tf.layers.input({shape: [1]});
const output = tf.layers.dense({units: 1, activation: 'sigmoid'}).apply(input);
```

이제 모델을 로드하고 입력과 출력을 정의했으므로 실제로 IoT 장치를 제어할 코드를 작성할 수 있습니다. 입력을 받고 모델을 사용하여 출력을 예측하는 함수를 생성하여 이를 수행합니다.

```javascript
async function predict(input) {
  const output = model.predict(input);
  return output;
}
```

마지막으로, predict() 함수를 호출하고 출력을 사용하여 IoT 장치를 제어하는 코드를 작성해야 합니다. Node.js [serialport](https://serialport.io/) 라이브러리를 사용하여 이를 수행합니다.

```javascript
const SerialPort = require('serialport');
const Readline = require('@serialport/parser-readline');

const port = new SerialPort('/dev/ttyACM0', {
  baudRate: 9600
});

const parser = port.pipe(new Readline({ delimiter: '\r\n' }));

parser.on('data', async line => {
  const input = parseFloat(line);
  const output = await predict(input);
  port.write(output);
});
```

## 결론

이 게시물에서는 Node.js와 함께 TensorFlow.js를 사용하여 IoT 장치를 제어하는 데 사용할 수 있는 애플리케이션을 개발하는 방법을 보여주었습니다. 우리는 TensorFlow.js와 IoT로 가능한 것의 표면을 긁어봤을 뿐이지만 이것이 가능한 것을 맛보고 더 깊이 탐구하도록 영감을 주셨기를 바랍니다.