---
title: AWS SageMaker: 클라우드에서 기계 학습 모델 구축 및 배포
description: 
published: true
date: 2023-02-03T12:17:46.590Z
tags: 
editor: markdown
dateCreated: 2023-02-03T12:17:44.961Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS SageMaker: Building and Deploying Machine Learning Models in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-sagemaker-building-and-deploying-machine-learning-models-in-the-cloud)
{.links-list}


# AWS SageMaker: 클라우드에서 기계 학습 모델 구축 및 배포

기계 학습은 명시적으로 프로그래밍하지 않고도 컴퓨터가 데이터로부터 학습할 수 있도록 하는 컴퓨터 과학 분야에서 빠르게 성장하고 있는 분야입니다. 기계 학습은 이미 추천 시스템, 이미지 인식 및 사기 탐지와 같은 다양한 애플리케이션에서 사용되고 있습니다.

AWS SageMaker는 개발자와 데이터 과학자에게 클라우드에서 기계 학습 모델을 구축, 교육 및 배포할 수 있는 기능을 제공하는 완전관리형 서비스입니다. SageMaker는 기계 학습 프로세스의 각 단계에서 어려운 작업을 제거하여 고품질 모델을 더 쉽게 개발할 수 있도록 합니다.

## SageMaker 시작하기

SageMaker를 시작하려면 먼저 AWS 계정을 생성하고 SageMaker에 가입해야 합니다. 계정이 있으면 개발 환경으로 사용할 Amazon Elastic Compute Cloud(Amazon EC2) 인스턴스를 생성할 수 있습니다. SageMaker는 EC2 인스턴스를 시작하는 데 사용할 수 있는 사전 구성된 다양한 Amazon 머신 이미지(AMI)를 제공합니다.

EC2 인스턴스를 시작한 후에는 SSH를 사용하여 연결하고 SageMaker Python SDK를 설치할 수 있습니다. SDK는 SageMaker 작업을 보다 쉽게 해주는 여러 편의 기능을 제공합니다.

## SageMaker 모델 생성

SageMaker 모델을 생성하는 방법에는 두 가지가 있습니다.

- SageMaker Python SDK를 사용하여 Python 스크립트를 사용하여 모델을 정의합니다.
- SageMaker 웹 인터페이스를 사용하여 사전 훈련된 기계 학습 알고리즘을 사용하여 모델을 생성합니다.

### SageMaker Python SDK로 모델 생성

Python SDK를 사용하여 SageMaker 모델을 생성하려면 먼저 모델을 정의하는 Python 스크립트를 작성해야 합니다. 스크립트는 SageMaker Python SDK를 가져오고 SageMaker.Model 클래스의 하위 클래스를 정의해야 합니다.

모델 클래스는 다음 두 가지 메서드를 구현해야 합니다.

- ```train()```, 모델이 훈련 중일 때 호출됩니다. 여기서 훈련 알고리즘을 구현해야 합니다.
- ```predict()```, 모델이 배포될 때 호출되며 예측을 만드는 데 사용됩니다. 여기에서 예측 알고리즘을 구현해야 합니다.

모델 클래스를 정의하고 나면 이를 인스턴스화하고 ```fit()``` 메서드를 호출하여 모델을 훈련할 수 있습니다. ```fit()``` 메서드는 SageMaker.TrainingInstance 및 SageMaker.S3DataSource를 입력으로 사용합니다. TrainingInstance는 훈련 작업을 구성하는 데 사용되고 S3DataSource는 훈련 데이터의 위치를 지정하는 데 사용됩니다.

학습 작업이 완료되면 ```deploy()``` 메서드를 호출하여 학습된 모델을 배포할 수 있습니다. ```deploy()``` 메서드는 SageMaker.PredictorInstance 및 SageMaker.S3DataSource를 입력으로 사용합니다. PredictorInstance는 예측 엔드포인트를 구성하는 데 사용되고 S3DataSource는 모델 아티팩트의 위치를 지정하는 데 사용됩니다.

### SageMaker 웹 인터페이스로 모델 생성

웹 인터페이스를 사용하여 SageMaker 모델을 생성하려면 먼저 SageMaker 노트북 인스턴스를 시작해야 합니다. 노트북 인스턴스는 SageMaker Python SDK 및 Jupyter가 설치된 상태로 제공되는 Amazon EC2 인스턴스입니다.

노트북 인스턴스가 실행되면 Jupyter 노트북을 열고 새 SageMaker 모델을 생성할 수 있습니다. 이렇게 하려면 왼쪽 탐색 모음에서 "SageMaker 모델" 링크를 클릭한 다음 "모델 생성" 버튼을 클릭합니다.

"모델 만들기" 페이지에서 모델 이름을 지정하고 기계 학습 알고리즘을 선택해야 합니다. SageMaker는 사용할 수 있는 여러 가지 사전 훈련된 기계 학습 알고리즘을 제공합니다. 이 예에서는 XGBoost 알고리즘을 사용합니다.

다음으로 훈련 데이터의 위치를 지정해야 합니다. SageMaker는 Amazon S3에 저장된 데이터를 사용할 수 있으므로 Amazon S3 버킷을 생성하고 훈련 데이터를 해당 버킷에 업로드해야 합니다.

학습 데이터의 위치를 지정했으면 "모델 생성" 버튼을 클릭하여 모델을 생성할 수 있습니다.

## SageMaker 모델 교육

SageMaker 모델을 생성한 후에는 ```fit()``` 메서드를 사용하여 모델을 교육할 수 있습니다. ```fit()``` 메서드는 SageMaker.TrainingInstance 및 SageMaker.S3DataSource를 입력으로 사용합니다. TrainingInstance는 훈련 작업을 구성하는 데 사용되고 S3DataSource는 훈련 데이터의 위치를 지정하는 데 사용됩니다.

 학습 작업이 완료되면 ```deploy()``` 메서드를 호출하여 학습된 모델을 배포할 수 있습니다. ```deploy()``` 메서드는 SageMaker.PredictorInstance 및 SageMaker.S3DataSource를 입력으로 사용합니다. PredictorInstance는 예측 엔드포인트를 구성하는 데 사용되고 S3DataSource는 모델 아티팩트의 위치를 지정하는 데 사용됩니다.

## 결론

이 기사에서는 AWS SageMaker를 사용하여 클라우드에서 기계 학습 모델을 구축하고 배포하는 방법을 살펴보았습니다. SageMaker는 어려운 작업을 처리하는 완전 관리형 서비스를 제공하여 기계 학습 모델을 쉽게 교육하고 배포할 수 있도록 합니다.