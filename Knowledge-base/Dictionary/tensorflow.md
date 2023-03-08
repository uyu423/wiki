---
title: TensorFlow
description: 
published: true
date: 2023-02-13T17:55:51.562Z
tags: 
editor: markdown
dateCreated: 2023-02-13T17:55:49.071Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [TensorFlow***English** document is available*](/en/Knowledge-base/Dictionary/tensorflow)
{.links-list}


# 개요
TensorFlow는 다양한 작업에서 데이터 흐름 프로그래밍을 위한 오픈 소스 소프트웨어 라이브러리입니다. 기호 수학 라이브러리이며 신경망과 같은 기계 학습 응용 프로그램에도 사용됩니다.

# 설명
TensorFlow는 원래 Google 내부용으로 Google Brain 팀에서 개발했습니다. 2015년 11월 9일 Apache 2.0 오픈 소스 라이선스로 출시되었습니다.

TensorFlow는 데이터 흐름 그래프를 사용한 수치 계산을 위한 라이브러리입니다. 데이터 흐름 그래프는 작업과 작업 간의 종속성을 그래픽으로 표현한 것입니다. 그래프의 노드는 수학적 연산을 나타내고 가장자리는 노드 사이를 흐르는 데이터 또는 텐서를 나타냅니다. 그래프는 신경망, 선형 대수, 최적화 알고리즘을 포함한 광범위한 수학적 연산을 나타내는 데 사용할 수 있습니다.

TensorFlow는 유연하고 확장 가능하도록 설계되었습니다. CPU, GPU 및 맞춤형 ASIC를 포함한 다양한 하드웨어 구성에서 사용할 수 있습니다. 또한 기계 학습 모델을 구축하고 배포하기 위한 다양한 도구와 라이브러리를 제공합니다.

# 역사
TensorFlow는 2011년 Google Brain 팀에서 만들었습니다. 처음에는 Google에서 내부용으로 개발되었지만 이후 2015년에 오픈 소스 라이브러리로 출시되었습니다. 이후 가장 인기 있고 널리 사용되는 기계 학습 중 하나가 되었습니다. 세계의 도서관.

# 특징
TensorFlow는 기계 학습 모델을 구축하고 교육하기 위한 다양한 기능을 제공합니다. 여기에는 다음이 포함됩니다.

- 데이터 흐름 그래프: TensorFlow를 사용하면 데이터 흐름 그래프를 만들어 수학적 연산을 나타낼 수 있습니다.
- 자동 차별화: TensorFlow는 작업을 자동으로 구분하여 기계 학습 모델을 효율적으로 교육할 수 있습니다.
- 높은 수준의 API: TensorFlow는 기계 학습 모델을 구축하고 교육하기 위한 높은 수준의 API를 제공합니다.
- 모델 배포: TensorFlow는 훈련된 모델을 프로덕션 환경에 배포하기 위한 도구를 제공합니다.

# 예
TensorFlow는 심층 신경망을 비롯한 다양한 기계 학습 모델을 구축하고 훈련하는 데 사용할 수 있습니다. 예를 들어 다음 코드는 손으로 쓴 숫자를 인식하기 위한 간단한 신경망을 만듭니다.

```python
import tensorflow as tf

# Create the model
model = tf.keras.models.Sequential([
    tf.keras.layers.Flatten(input_shape=(28, 28)),
    tf.keras.layers.Dense(128, activation='relu'),
    tf.keras.layers.Dense(10, activation='softmax')
])

# Compile the model
model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])

# Train the model
model.fit(x_train, y_train, epochs=5)
```

# 장점과 단점
TensorFlow에는 다음과 같은 많은 이점이 있습니다.

- 유연성: TensorFlow는 다양한 하드웨어 구성과 다양한 애플리케이션에 사용할 수 있습니다.
- 확장성: TensorFlow는 대규모 데이터 세트 및 복잡한 모델로 확장할 수 있습니다.
- 라이브러리 및 도구: TensorFlow는 기계 학습 모델을 구축하고 배포하기 위한 다양한 라이브러리와 도구를 제공합니다.

그러나 TensorFlow 사용에는 다음과 같은 몇 가지 단점도 있습니다.

- 복잡성: TensorFlow는 데이터 흐름 그래프 및 수치 계산에 대한 깊은 이해가 필요하기 때문에 초보자가 사용하기 어려울 수 있습니다.
- 성능: TensorFlow는 특히 CPU에서 모델 학습 속도가 느릴 수 있습니다.

# 관련 기술
TensorFlow는 Keras, PyTorch 및 Scikit-Learn과 같은 다른 기계 학습 라이브러리와 밀접한 관련이 있습니다. 구글의 딥러닝 플랫폼인 TFX(TensorFlow Extended)와도 관련이 있다.

# 기타
TensorFlow는 세계에서 가장 인기 있고 널리 사용되는 기계 학습 라이브러리 중 하나가 되었습니다. Google, Apple 및 Uber를 비롯한 많은 회사 및 조직에서 사용합니다.