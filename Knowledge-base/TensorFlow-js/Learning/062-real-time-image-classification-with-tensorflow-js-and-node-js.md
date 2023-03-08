---
title: 062: TensorFlow.js 및 Node.js를 사용한 실시간 이미지 분류
description: 
published: true
date: 2023-02-02T21:36:45.205Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:36:43.516Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [062: Real-Time Image Classification with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/062-real-time-image-classification-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 실시간 이미지 분류

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 실시간 이미지 분류 앱을 빌드하는 방법을 살펴보겠습니다.

TensorFlow.js는 자바스크립트로 기계 학습 모델을 만들기 위한 강력한 도구입니다. Node.js는 서버에서 JavaScript를 실행할 수 있게 해주는 JavaScript 런타임입니다.

 이 두 가지 기술을 함께 사용하여 강력한 실시간 이미지 분류 애플리케이션을 구축할 수 있습니다.

## TensorFlow.js 설치하기

첫 번째 단계는 TensorFlow.js를 설치하는 것입니다. NPM(노드 패키지 관리자)을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

## Node.js 설치하기

Node.js를 아직 설치하지 않은 경우 Node.js 웹 사이트(https://nodejs.org/en/)의 지침에 따라 설치할 수 있습니다.

## 모델 구축

이제 TensorFlow.js 및 Node.js가 설치되었으므로 이미지 분류 모델 구축을 시작할 수 있습니다.

우리는 MobileNet 모델을 사용할 것입니다. MobileNet은 대규모 이미지 데이터 세트에 대해 훈련된 사전 훈련된 모델입니다.

MobileNet 모델을 사용하려면 먼저 TensorFlow.js에 로드해야 합니다.

```javascript
const tf = require('@tensorflow/tfjs');

const mobilenet = require('@tensorflow-models/mobilenet');

async function loadModel() {
  const model = await mobilenet.load();
  return model;
}
```

모델이 로드되면 이를 사용하여 이미지를 분류할 수 있습니다.

아래의 classifyImage() 함수는 이미지를 입력으로 사용하고 상위 5개의 예측을 반환합니다.

```javascript
async function classifyImage(image) {
  const model = await loadModel();
  const predictions = await model.classify(image);
  return predictions;
}
```

## 모델 제공

이제 이미지 분류 모델이 구축되었으므로 Node.js를 사용하여 제공해야 합니다.

우리는 Express 웹 프레임워크를 사용할 것입니다. Express는 Node.js용으로 널리 사용되는 웹 프레임워크입니다.

Express를 설치하려면 다음 명령을 실행합니다.

```
npm install express
```

Express가 설치되면 server.js라는 파일을 만들고 다음 코드를 추가할 수 있습니다.

```javascript
const express = require('express');
const app = express();

app.use(express.static('public'));

app.get('/classify', async (req, res) => {
  const image = req.query.image;
  const predictions = await classifyImage(image);
  res.json(predictions);
});

app.listen(3000, () => console.log('Server listening on port 3000!'));
```

위의 코드는 다음을 수행합니다.

- 공개 디렉토리에서 정적 파일 제공
- 이미지 URL을 쿼리 매개변수로 사용하는 엔드포인트(/classify) 생성
- classifyImage() 함수를 사용하여 이미지를 분류합니다.
- 상위 5개 예측을 JSON으로 반환

## 프론트엔드 구축

이제 Node.js 서버를 가동하고 실행 중이므로 애플리케이션의 프런트 엔드 구축을 시작할 수 있습니다.

우리는 React를 사용할 것입니다. React는 사용자 인터페이스 구축에 널리 사용되는 JavaScript 라이브러리입니다.

React를 설치하려면 다음 명령을 실행합니다.

```
npm install react react-dom
```

React가 설치되면 App.js라는 파일을 만들고 다음 코드를 추가할 수 있습니다.

```javascript
import React, { useState, useEffect } from 'react';
import './App.css';

function App() {
  const [image, setImage] = useState(null);
  const [predictions, setPredictions] = useState([]);

  useEffect(() => {
    async function fetchPredictions() {
      const response = await fetch('/classify?image=' + image);
      const predictions = await response.json();
      setPredictions(predictions);
    }
    if (image) {
      fetchPredictions();
    }
  }, [image]);

  const onSelectFile = e => {
    if (e.target.files && e.target.files.length > 0) {
      const reader = new FileReader();
      reader.onload = () => setImage(reader.result);
      reader.readAsDataURL(e.target.files[0]);
    }
  };

  return (
    <div className="App">
      <h1>Real-Time Image Classification</h1>
      <p>
        Select an image to classify:
      </p>
      <input type="file" accept="image/*" onChange={onSelectFile} />
      {predictions.length > 0 && (
        <div className="predictions">
          <h2>Predictions</h2>
          {predictions.map((prediction, i) => (
            <div key={i}>
              <div className="prediction-label">{prediction.className}</div>
              <div className="prediction-confidence">{prediction.probability.toFixed(2)}</div>
            </div>
          ))}
        </div>
      )}
    </div>
  );
}

export default App;
```

위의 코드는 다음을 수행합니다.

- 사용자가 이미지를 선택할 수 있는 파일 입력 필드를 렌더링합니다.
- 이미지를 선택하면 이미지가 서버에 업로드되고 예측이 가져옵니다.
- 그런 다음 예측이 페이지에 표시됩니다.

## 앱 실행

이제 프런트엔드 및 백엔드 코드가 완성되었으므로 앱을 실행할 수 있습니다.

먼저 다음 명령을 실행하여 Node.js 서버를 시작합니다.

```
node server.js
```

그런 다음 브라우저에서 다음 URL을 엽니다. http://localhost:3000

이제 이미지 분류 앱이 실행되고 있는 것을 볼 수 있습니다!