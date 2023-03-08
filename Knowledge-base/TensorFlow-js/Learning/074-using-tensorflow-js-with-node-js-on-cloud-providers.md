---
title: 074: 클라우드 공급자에서 Node.js와 함께 TensorFlow.js 사용
description: 
published: true
date: 2023-02-03T00:04:39.646Z
tags: 
editor: markdown
dateCreated: 2023-02-03T00:04:37.992Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [074: Using TensorFlow.js with Node.js on Cloud Providers***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/074-using-tensorflow-js-with-node-js-on-cloud-providers)
{.links-list}


# 클라우드 공급자에서 Node.js와 함께 TensorFlow.js 사용

TensorFlow.js는 자바스크립트에서 기계 학습을 위한 강력한 도구입니다. AWS, Azure 및 Google Cloud Platform과 같은 클라우드 공급자의 Node.js 애플리케이션에서 사용할 수 있습니다.

이 게시물에서는 클라우드 공급자에서 Node.js 애플리케이션을 설정하고 TensorFlow.js를 사용하여 기계 학습 모델을 교육하는 방법을 다룹니다. 또한 학습된 모델을 웹 애플리케이션에서 사용할 수 있도록 클라우드 공급자에 배포합니다.

## 클라우드 공급자에 Node.js 애플리케이션 설정

먼저 클라우드 공급자에 Node.js 애플리케이션을 설정해야 합니다. Express 웹 프레임워크를 사용하여 기본 웹 애플리케이션을 설정합니다.

Express에 익숙하지 않다면 [시작 가이드](http://expressjs.com/en/starter/installing.html)를 확인하세요.

Express가 설치되면 다음 코드를 사용하여 `app.js`라는 파일을 만들 수 있습니다.

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello, world!');
});

app.listen(3000, () => {
  console.log('Example app listening on port 3000!');
});
```

이 코드는 "Hello, world!"로 HTTP 요청에 응답하는 기본 Express 애플리케이션을 생성합니다. 메시지.

다음으로 Node.js 애플리케이션을 클라우드 공급자에 배포해야 합니다. 이 예에서는 AWS를 사용하지만 프로세스는 다른 공급자와 유사합니다.

먼저 AWS 계정을 만들고 EC2에 액세스할 수 있는 새 IAM 사용자를 만듭니다. 이를 수행하는 방법에 대한 자세한 내용은 [AWS 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)를 참조하십시오.

IAM 사용자가 설정되면 새 EC2 인스턴스를 생성할 수 있습니다. 이 예에서는 t2.micro 인스턴스를 사용합니다.

인스턴스가 실행되면 SSH를 통해 인스턴스에 연결하고 Node.js 애플리케이션에 대한 종속성을 설치할 수 있습니다.

```
$ sudo npm install -g express
$ sudo npm install -g ejs
```

다음으로 `app.js` 파일을 EC2 인스턴스에 복사해야 합니다. scp 명령을 사용하여 이 작업을 수행할 수 있습니다.

```
$ scp -i <path-to-pem-file> app.js ec2-user@<ec2-instance-ip>:~/
```

파일이 복사되면 Node.js 애플리케이션을 시작할 수 있습니다.

```
$ node app.js
```

이제 Node.js 애플리케이션이 EC2 인스턴스에서 실행 중입니다!

## TensorFlow.js를 Node.js와 함께 사용

이제 Node.js 애플리케이션을 실행하고 있으므로 TensorFlow.js를 사용할 수 있습니다.

먼저 TensorFlow.js Node.js 패키지를 설치해야 합니다.

```
$ npm install @tensorflow/tfjs-node
```

다음으로 다음 코드를 사용하여 `train.js`라는 파일을 만듭니다.

```javascript
const tf = require('@tensorflow/tfjs-node');

// Define a model for linear regression.
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));

// Prepare the model for training: Specify the loss and the optimizer.
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

// Generate some synthetic data for training.
const xs = tf.tensor2d([1, 2, 3, 4], [4, 1]);
const ys = tf.tensor2d([1, 3, 5, 7], [4, 1]);

// Train the model using the data.
model.fit(xs, ys, {epochs: 10}).then(() => {
  // Use the model to do inference on a data point the model hasn't seen before:
  model.predict(tf.tensor2d([5], [1, 1])).print();
});
```

이 코드는 TensorFlow.js를 사용하여 간단한 선형 회귀 모델을 정의합니다. 그런 다음 일부 합성 데이터를 사용하여 모델을 교육합니다. 마지막으로 모델을 사용하여 새로운 데이터 포인트를 예측합니다.

이 코드를 실행하려면 `node` 명령을 사용할 수 있습니다.

```
$ node train.js
```

## TensorFlow.js 모델을 클라우드 제공업체에 배포

훈련된 TensorFlow.js 모델이 있으면 웹 애플리케이션에서 사용할 수 있도록 클라우드 공급자에 배포할 수 있습니다.

이 예에서는 AWS를 다시 사용하지만 프로세스는 다른 공급자와 비슷합니다.

먼저 모델 파일을 저장할 Amazon S3 버킷을 생성해야 합니다. 이를 수행하는 방법에 대한 자세한 내용은 [AWS 설명서](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html)를 참조하십시오.

다음으로 AWS CLI를 설치해야 합니다. 이를 수행하는 방법에 대한 자세한 내용은 [AWS 설명서](https://docs.aws.amazon.com/cli/latest/userguide/installing.html)를 참조하십시오.

AWS CLI가 설치되면 이를 사용하여 로컬 모델 파일을 S3 버킷에 동기화할 수 있습니다.

```
$ aws s3 sync . s3://<s3-bucket-name>
```

이제 TensorFlow.js 모델이 S3 버킷에 배포되었습니다!