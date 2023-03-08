---
title: 095: Spring Boot 및 TensorFlow를 사용하여 기계 학습 시스템 구축
description: 
published: true
date: 2023-02-06T00:32:33.309Z
tags: 
editor: markdown
dateCreated: 2023-02-06T00:32:31.736Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [095: Building a Machine Learning System with Spring Boot and TensorFlow***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/095-building-a-machine-learning-system-with-spring-boot-and-tensorflow)
{.links-list}


# 095: Spring Boot와 TensorFlow로 기계 학습 시스템 구축하기

이번 포스팅에서는 Spring Boot와 TensorFlow를 이용하여 머신러닝 시스템을 구축하는 방법에 대해 알아보겠습니다. 개발 환경을 설정하고, 모델을 훈련하고, 훈련된 모델을 웹 애플리케이션에 배포하는 과정을 살펴보겠습니다.

## 개발 환경 설정

가장 먼저 해야 할 일은 개발 환경을 설정하는 것입니다. 다음 소프트웨어를 설치해야 합니다.

- 자바 8
- 메이븐
- 텐서플로우

즐겨 사용하는 패키지 관리자를 사용하여 Java 8 및 Maven을 설치할 수 있습니다. TensorFlow의 경우 [TensorFlow 웹사이트](https://www.tensorflow.org/)에서 바이너리를 다운로드해야 합니다. 모든 것이 설치되면 새 Maven 프로젝트를 만들고 `pom.xml` 파일에 다음 종속성을 추가할 수 있습니다.

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.tensorflow</groupId>
        <artifactId>tensorflow-core</artifactId>
        <version>1.15.0</version>
    </dependency>
</dependencies>
```

## 모델 교육

이제 개발 환경이 설정되었으므로 기계 학습 모델 교육을 시작할 수 있습니다. 이 예에서는 [MNIST](https://en.wikipedia.org/wiki/MNIST_database) 데이터세트를 사용합니다. MNIST 데이터 세트는 이미지 인식 모델 교육에 일반적으로 사용되는 필기 숫자 모음입니다.

`MnistClassifier.java`라는 새로운 Java 클래스를 생성하는 것으로 시작하겠습니다. 이 수업에서는 TensorFlow를 사용하여 MNIST 숫자를 분류하는 간단한 신경망을 훈련합니다. [Keras](https://keras.io/) API를 사용하여 신경망 개발을 단순화하겠습니다.

먼저 다음 패키지를 가져와야 합니다.

```java
import org.tensorflow.keras.datasets.mnist.MnistDataset;
import org.tensorflow.keras.models.Sequential;
import org.tensorflow.keras.layers.Dense;
import org.tensorflow.keras.optimizers.SGD;
```

다음으로 MNIST 데이터 세트를 로드합니다.

```java
MnistDataset dataset = MnistDataset.create();
```

이제 신경망을 만들 수 있습니다.

```java
Sequential model = new Sequential();
model.add(new Dense(128, activation="relu", inputShape=(784,)));
model.add(new Dense(10, activation="softmax"));
```

이제 모델을 컴파일하고 훈련할 수 있습니다.

```java
model.compile(
    optimizer=new SGD(0.001),
    loss="categorical_crossentropy",
    metrics=["accuracy"]
);
model.fit(
    dataset.getTrainImages(), dataset.getTrainLabels(),
    epochs=10, batchSize=128
);
```

## 학습된 모델 배포

훈련된 모델이 있으므로 이제 웹 애플리케이션에 배포할 수 있습니다. 웹 애플리케이션 개발을 단순화하기 위해 Spring Boot를 사용할 것입니다.

먼저 `MnistController.java`라는 새로운 자바 클래스를 생성해야 합니다. 이 클래스에서는 `/classify` 엔드포인트를 노출하는 REST 컨트롤러를 생성합니다. 이 끝점은 손으로 쓴 숫자의 이미지를 가져와 예측된 숫자를 반환합니다.

다음 패키지를 가져오는 것으로 시작하겠습니다.

```java
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;
```

다음으로 `MnistController` 클래스를 만들고 `@RestController`로 주석을 추가합니다.

```java
@RestController
public class MnistController {

}
```

이제 `/classify` 엔드포인트를 만들 수 있습니다.

```java
@PostMapping("/classify")
public String classify(@RequestParam("image") String image) {
    // TODO: Classify the image and return the predicted digit
}
```

`classify` 메서드에서 이미지를 분류하고 예측된 숫자를 반환해야 합니다. 훈련된 `MnistClassifier` 클래스를 사용하여 이를 수행할 수 있습니다.

```java
MnistClassifier classifier = new MnistClassifier();
String predictedDigit = classifier.classify(image);
return predictedDigit;
```

## 결론

이번 포스팅에서는 Spring Boot와 TensorFlow를 이용하여 머신러닝 시스템을 구축하는 방법에 대해 알아보았습니다. 개발 환경을 설정하고, 모델을 훈련하고, 훈련된 모델을 웹 애플리케이션에 배포하는 과정을 거쳤습니다.