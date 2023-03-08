---
title: TensorFlow 및 Keras를 사용한 기계 학습 소개
description: 
published: true
date: 2023-02-09T22:55:38.958Z
tags: 
editor: markdown
dateCreated: 2023-02-09T22:55:32.554Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Introduction to Machine Learning with TensorFlow and Keras***English** document is available*](/en/Knowledge-base/Common/introduction-to-machine-learning-with-tensorflow-and-keras)
{.links-list}


# TensorFlow 및 Keras를 사용한 기계 학습 소개

애플리케이션에 기계 학습을 추가하려는 개발자는 프레임워크 및 라이브러리와 관련하여 선택할 수 있는 많은 옵션이 있습니다. TensorFlow와 Keras는 딥 러닝을 위한 가장 인기 있는 두 가지 옵션이며, 이 기사에서는 두 가지 모두를 시작하는 방법을 살펴보겠습니다.

## 텐서플로

TensorFlow는 Google에서 개발한 인기 있는 기계 학습용 오픈 소스 플랫폼입니다. 개발자가 정교한 기계 학습 모델을 쉽게 만들 수 있도록 하는 다양한 도구, 라이브러리 및 커뮤니티 리소스를 제공합니다.

또한 TensorFlow는 프로덕션 배포에 중점을 두고 있으며 기계 학습 모델을 서비스 및 장치에 쉽게 배포할 수 있는 여러 기능을 제공합니다.

## 케라스

Keras는 사용 편의성과 빠른 개발에 중점을 두고 개발된 고급 딥 러닝 API입니다. TensorFlow 위에 구축되었으며 최소한의 코드로 정교한 기계 학습 모델을 만드는 데 사용할 수 있습니다.

Keras는 또한 딥 러닝 모델을 구축하고 실험할 수 있는 간단하고 효율적인 방법을 제공하기 때문에 프로토타이핑 및 연구에 널리 사용됩니다.

## 시작하기

이 섹션에서는 TensorFlow 및 Keras를 시작하는 방법을 살펴보겠습니다. 필요한 종속성을 설치하여 시작한 다음 몇 가지 기본 코드 예제를 살펴보겠습니다.

### 설치

TensorFlow 및 Keras를 사용하기 전에 필요한 종속 항목을 설치해야 합니다. TensorFlow는 pip를 사용하여 설치할 수 있습니다.

```
pip install tensorflow
```

Keras는 pip로도 설치할 수 있습니다.

```
pip install keras
```

### 안녕하세요, TensorFlow

이제 TensorFlow와 Keras가 설치되었으므로 간단한 예를 살펴보겠습니다. TensorFlow 라이브러리를 가져오는 것으로 시작하겠습니다.

```python
import tensorflow as tf
```

다음으로 TensorFlow 상수를 만듭니다.

```python
tf.constant('Hello, TensorFlow!')
```

이 코드는 "Hello, TensorFlow!"라는 문자열을 인쇄합니다. 콘솔에.

### 안녕, 케라스

이제 간단한 Keras 예제를 살펴보겠습니다. Keras 라이브러리를 가져오는 것으로 시작하겠습니다.

```python
import keras
```

다음으로 Keras Sequential 모델을 만듭니다.

```python
model = keras.Sequential()
```

이 코드는 간단한 Keras Sequential 모델을 생성합니다. 그런 다음 .add() 메서드를 사용하여 모델에 레이어를 추가할 수 있습니다.

```python
model.add(keras.layers.Dense(units=32, input_shape=(784,)))
model.add(keras.layers.Activation('relu'))
model.add(keras.layers.Dense(units=10))
model.add(keras.layers.Activation('softmax'))
```

이 코드는 32개의 뉴런이 있는 dense 레이어, 활성화 레이어, 10개의 뉴런이 있는 dense 레이어 및 활성화 레이어를 추가합니다.

그런 다음 .compile() 메서드를 사용하여 모델을 컴파일할 수 있습니다.

```python
model.compile(loss='categorical_crossentropy',
              optimizer='sgd',
              metrics=['accuracy'])
```

이 코드는 범주형 교차 엔트로피 손실 함수, 확률적 경사 하강 최적화 프로그램 및 정확도 메트릭을 사용하여 모델을 컴파일합니다.

그런 다음 .fit() 메서드를 사용하여 모델을 데이터에 맞출 수 있습니다.

```python
model.fit(x_train, y_train,
          batch_size=128, epochs=5,
          verbose=1,
          validation_data=(x_test, y_test))
```

이 코드는 모델을 5 에포크의 학습 데이터에 맞춥니다. 모델은 크기 128의 미니 배치를 사용하여 교육됩니다. .fit() 메서드는 교육 중에 모델을 평가하는 데 사용되는 validation_data 인수도 사용합니다.

그런 다음 .evaluate() 메서드를 사용하여 모델을 평가할 수 있습니다.

```python
score = model.evaluate(x_test, y_test, verbose=0)
```

이 코드는 테스트 데이터에서 모델을 평가하고 손실 및 정확도를 반환합니다.

## 결론

이 기사에서는 TensorFlow 및 Keras를 시작하는 방법을 살펴보았습니다. 필요한 종속성을 설치하고 몇 가지 기본 코드 예제를 살펴보았습니다.

TensorFlow 및 Keras에 대해 자세히 알아보려면 다음 리소스를 확인하는 것이 좋습니다.

- TensorFlow 웹사이트: https://www.tensorflow.org/
- 케라스 웹사이트: https://keras.io/
- TensorFlow 문서: https://www.tensorflow.org/docs/
- 케라스 문서: https://keras.io/docs/