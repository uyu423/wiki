---
title: Keras
description: 
published: true
date: 2023-02-16T03:55:55.747Z
tags: 
editor: markdown
dateCreated: 2023-02-16T03:55:53.560Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Keras***English** document is available*](/en/Knowledge-base/Dictionary/keras)
{.links-list}


# 개요
Keras는 Python으로 작성된 오픈 소스 신경망 라이브러리입니다. 모든 기술 수준의 사용자가 딥 러닝 모델을 만들고 배포할 수 있도록 간단하고 직관적으로 설계되었습니다. Keras는 TensorFlow, Theano 또는 CNTK 백엔드와 함께 사용할 수 있는 고급 API입니다.

# 설명
Keras는 데이터에서 학습하기 위해 신경망을 사용하는 머신 러닝 유형인 딥 러닝용 라이브러리입니다. Google 엔지니어인 François Chollet이 개발하여 2015년에 출시했습니다. Keras는 사용자 친화적이고 직관적으로 설계되었으며 신경망 구축 및 훈련을 위한 고급 API를 제공합니다.

Keras는 신경망 구축 및 훈련을 위한 저수준 라이브러리인 TensorFlow, Theano 또는 CNTK 위에 구축됩니다. 사용자가 모델을 만들고 훈련할 수 있는 더 간단하고 직관적인 인터페이스를 제공합니다. Keras는 또한 각각 이미지 및 텍스트 처리에 사용되는 컨벌루션 및 순환 신경망을 지원합니다.

Keras는 사용 편의성과 유연성으로 인해 딥 러닝에 널리 사용됩니다. 또한 컴퓨터 비전, 자연어 처리 및 자동 음성 인식을 포함한 많은 응용 프로그램에 사용됩니다.

# 특징
Keras는 딥 러닝 모델을 보다 쉽게 사용할 수 있도록 다양한 기능을 제공합니다. 여기에는 다음이 포함됩니다.

- **높은 수준의 API:** Keras는 신경망 구축 및 훈련을 위한 높은 수준의 API를 제공하므로 모든 기술 수준의 사용자가 모델을 쉽게 만들 수 있습니다.

- **호환성:** Keras는 TensorFlow, Theano 및 CNTK와 호환되므로 사용자가 필요에 가장 적합한 백엔드를 선택할 수 있습니다.

- **모듈식 설계:** Keras는 모듈식으로 설계되어 사용자가 다양한 계층과 모델을 쉽게 만들고 결합할 수 있습니다.

- **컨볼루션 및 반복 신경망 지원:** Keras는 각각 이미지 및 텍스트 처리에 사용되는 컨볼루션 및 반복 신경망을 지원합니다.

- **확장성:** Keras는 확장 가능하도록 설계되어 사용자가 맞춤형 레이어와 모델을 만들 수 있습니다.

# 예
다음 예제에서는 Keras를 사용하여 간단한 컨벌루션 신경망을 만드는 방법을 보여줍니다.

```python
from keras.layers import Conv2D, MaxPooling2D
from keras.models import Sequential

model = Sequential()
model.add(Conv2D(32, (3, 3), activation='relu', input_shape=(28, 28, 1)))
model.add(MaxPooling2D((2, 2)))
model.add(Conv2D(64, (3, 3), activation='relu'))
model.add(MaxPooling2D((2, 2)))
model.add(Conv2D(64, (3, 3), activation='relu'))

model.summary()
```

# 장점과 단점
Keras는 사용 편의성과 유연성으로 인해 딥 러닝에 널리 사용됩니다. 사용자 친화적이고 직관적으로 설계되었으며 신경망 구축 및 훈련을 위한 높은 수준의 API를 제공합니다.

그러나 Keras는 모든 애플리케이션에 적합하지 않습니다. TensorFlow 또는 Theano와 같은 저수준 라이브러리만큼 모델에 대한 제어 기능을 제공하지 않습니다. 또한 대규모 프로젝트에 중요할 수 있는 분산 컴퓨팅을 지원하지 않습니다.

# 관련 기술
Keras는 신경망 구축 및 훈련을 위한 저수준 라이브러리인 TensorFlow, Theano 및 CNTK 위에 구축되었습니다. Scikit-learn 및 PyTorch와 같은 다른 기계 학습 프레임워크와도 관련이 있습니다.