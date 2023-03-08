---
title: 소프트웨어 개발 033: TensorFlow 및 Keras
description: 
published: true
date: 2023-02-28T13:32:16.451Z
tags: 
editor: markdown
dateCreated: 2023-02-28T13:32:15.082Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Software Development 033: TensorFlow and Keras***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-033-tensorflow-and-keras)
{.links-list}


# 소프트웨어 개발 033: TensorFlow 및 Keras

## TensorFlow란?

TensorFlow는 데이터 분석 및 기계 학습을 위한 강력한 오픈 소스 소프트웨어 라이브러리입니다. Keras는 TensorFlow 위에 구축된 고급 신경망 API입니다.

TensorFlow는 원래 Google 내부용으로 Google Brain 팀 구성원이 개발했습니다. 2015년 11월 Apache 2.0 오픈 소스 라이선스로 출시되었습니다.

Keras는 Google 엔지니어인 François Chollet이 개발했습니다. 2015년 3월에 MIT 오픈 소스 라이선스로 출시되었습니다.

## 설치

TensorFlow 웹사이트의 지침에 따라 자신의 컴퓨터에 TensorFlow 및 Keras를 설치할 수 있습니다.

## 안녕하세요, 세계!

"안녕하세요, 세상!" program은 "Hello, world!"를 출력하는 간단한 프로그램입니다. 화면에.

파이썬에서 "Hello, world!" 프로그램은 다음과 같습니다.

```python
print("Hello, world!")
```

TensorFlow에서 "Hello, world!" 프로그램은 다음과 같습니다.

```python
import tensorflow as tf

tf.print("Hello, world!")
```

Keras에서 "Hello, world!" 프로그램은 다음과 같습니다.

```python
from keras.models import Sequential
from keras.layers import Dense, Activation

model = Sequential()
model.add(Dense(1, input_dim=1))
model.add(Activation('sigmoid'))

model.compile(optimizer='rmsprop',
              loss='binary_crossentropy',
              metrics=['accuracy'])

model.fit(x, y, epochs=1000, batch_size=32)
```

## TensorFlow와 Keras 비교

TensorFlow는 Keras보다 낮은 수준의 라이브러리입니다. 즉, 더 유연하지만 시작하려면 더 많은 작업이 필요합니다.

딥 러닝을 이제 막 시작했다면 케라스를 사용해야 할 것입니다. 사용하기 쉽고 장기적으로 시간을 절약할 수 있습니다.

## 자원

- [TensorFlow 웹사이트](https://www.tensorflow.org/)
- [케라스 홈페이지](https://keras.io/)
- [TensorFlow 튜토리얼](https://www.tensorflow.org/tutorials/)
- [케라스 튜토리얼](https://keras.io/getting-started/sequential-model-guide/)