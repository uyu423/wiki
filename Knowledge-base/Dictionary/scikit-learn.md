---
title: Scikit-learn
description: 
published: true
date: 2023-02-26T22:32:33.461Z
tags: 
editor: markdown
dateCreated: 2023-02-26T22:32:32.108Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Scikit-learn***English** document is available*](/en/Knowledge-base/Dictionary/scikit-learn)
{.links-list}


# 개요
Scikit-learn은 Python용 무료 오픈 소스 기계 학습 라이브러리입니다. 데이터 마이닝 및 데이터 분석을 위한 강력하고 효율적인 도구를 제공하도록 설계되었습니다. Scikit-learn은 광범위한 지도 및 비지도 학습 알고리즘을 제공하며 NumPy, SciPy 및 matplotlib와 같은 다른 인기 있는 Python 라이브러리 위에 구축됩니다.

# 설명
Scikit-learn은 Python에서 기계 학습을 위한 강력하고 효율적인 라이브러리입니다. 광범위한 감독 및 비지도 학습 알고리즘과 데이터 마이닝 및 데이터 분석 도구를 제공하도록 설계되었습니다. NumPy, SciPy 및 matplotlib와 같은 다른 인기 있는 Python 라이브러리 위에 구축됩니다.

Scikit-learn은 분류, 회귀, 클러스터링 및 차원 축소를 포함하여 다양한 지도 및 비지도 학습 알고리즘을 제공합니다. 이러한 알고리즘은 이미지 인식, 텍스트 분류 및 시계열 예측을 비롯한 다양한 작업에 사용할 수 있습니다.

라이브러리는 일관된 인터페이스와 명확한 설명 및 예제 제공에 중점을 두고 사용하기 쉽게 설계되었습니다. 또한 교차 검증 및 하이퍼파라미터 튜닝과 같은 모델 평가 및 선택을 위한 다양한 도구가 포함되어 있습니다.

# 역사
Scikit-learn은 원래 2007년 Google Summer of Code 프로젝트로 David Cournapeau에 의해 개발되었습니다. 나중에 2010년에 오픈 소스 프로젝트로 출시되었으며 이후 가장 인기 있는 Python용 기계 학습 라이브러리 중 하나가 되었습니다.

# 특징
Scikit-learn은 다음과 같은 다양한 지도 및 비지도 학습 알고리즘을 제공합니다.
- 로지스틱 회귀, 서포트 벡터 머신 및 나이브 베이즈와 같은 분류 알고리즘.
- 선형 회귀, 지원 벡터 머신 및 의사 결정 트리와 같은 회귀 알고리즘.
- k-평균 및 계층적 클러스터링과 같은 클러스터링 알고리즘.
- 주성분 분석 및 선형 판별 분석과 같은 차원 감소 알고리즘.

또한 교차 검증 및 하이퍼파라미터 튜닝과 같은 모델 평가 및 선택을 위한 다양한 도구가 포함되어 있습니다.

# 예
Scikit-learn은 이미지 인식, 텍스트 분류 및 시계열 예측과 같은 다양한 작업에 사용할 수 있습니다. 예를 들어 다음 예와 같이 손으로 쓴 숫자의 이미지를 분류하는 데 사용할 수 있습니다.

```python
from sklearn import datasets
from sklearn import svm

# Load the digits dataset
digits = datasets.load_digits()

# Create a Support Vector Classifier
clf = svm.SVC(gamma=0.001, C=100.)

# Train the classifier
clf.fit(digits.data[:-1], digits.target[:-1])

# Predict the label of the last image
predicted = clf.predict(digits.data[-1:])

# Print the predicted label
print(predicted)
```

# 장점과 단점
Scikit-learn은 Python에서 기계 학습을 위한 강력하고 효율적인 라이브러리입니다. 일관된 인터페이스와 명확한 설명 및 예를 제공하는 데 중점을 두고 사용하기 쉽게 설계되었습니다.

그러나 Scikit-learn은 딥러닝 알고리즘을 제공하지 않으며, 자연어 처리와 같은 복잡한 작업에 사용하기 어려울 수 있습니다.

# 관련 기술
Scikit-learn은 NumPy, SciPy 및 matplotlib와 같은 다른 인기 있는 Python 라이브러리 위에 구축됩니다. TensorFlow 및 Keras와 같은 Python용 다른 기계 학습 라이브러리와도 관련이 있습니다.