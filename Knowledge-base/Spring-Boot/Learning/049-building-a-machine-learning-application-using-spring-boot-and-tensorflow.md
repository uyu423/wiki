---
title: 049: Spring Boot와 TensorFlow를 사용하여 기계 학습 애플리케이션 구축
description: 
published: true
date: 2023-02-04T15:32:45.609Z
tags: 
editor: markdown
dateCreated: 2023-02-04T15:32:43.907Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [049: Building a machine learning application using Spring Boot and TensorFlow***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/049-building-a-machine-learning-application-using-spring-boot-and-tensorflow)
{.links-list}


# 049: Spring Boot와 TensorFlow를 사용하여 기계 학습 애플리케이션 구축

최근 기계 학습이 발전함에 따라 점점 더 많은 개발자가 이러한 기술을 활용할 수 있는 애플리케이션을 구축하려고 합니다. 이 게시물에서는 Spring Boot 및 TensorFlow를 사용하여 기계 학습 애플리케이션을 빌드하는 방법을 살펴보겠습니다.

머신 러닝이 무엇인지, 애플리케이션을 구축하는 데 어떻게 사용될 수 있는지 살펴보는 것으로 시작하겠습니다. 그런 다음 Spring Boot 프로젝트를 설정하고 TensorFlow를 통합하는 방법을 살펴보겠습니다. 마지막으로 TensorFlow를 사용하여 기계 학습 모델을 구축하는 방법에 대한 간단한 예를 살펴보겠습니다.

## 머신러닝이란?

기계 학습은 데이터에서 학습할 수 있는 알고리즘의 구성 및 연구를 다루는 인공 지능의 하위 분야입니다. 이러한 알고리즘은 새 데이터에 대한 예측을 수행할 수 있는 모델을 구축하는 데 사용할 수 있습니다.

머신 러닝에는 지도 학습과 비지도 학습의 두 가지 주요 유형이 있습니다. 감독 학습은 데이터에 레이블이 지정되고 알고리즘이 입력 데이터에서 출력 레이블로의 매핑을 학습하도록 훈련되는 곳입니다. 비지도 학습은 데이터에 레이블을 지정하지 않고 데이터 구조를 학습하도록 알고리즘을 훈련하는 것입니다.

## 기계 학습을 사용하여 애플리케이션 구축

기계 학습을 사용하여 데이터에서 자동으로 학습하고 개선할 수 있는 애플리케이션을 구축할 수 있습니다. 예를 들어 기계 학습 애플리케이션을 사용하여 이미지를 자동으로 분류하거나 이미지에서 개체를 감지할 수 있습니다.

기계 학습 응용 프로그램의 다른 예는 다음과 같습니다.

- 이미지 설명 자동 생성
- 언어 간 번역
- 주가 예측
- 사기 행위 감지

## 스프링 부트 프로젝트 설정

Spring Boot 프로젝트를 설정하는 것으로 시작하겠습니다. Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있는 프레임워크입니다.

Spring Initializr를 사용하여 프로젝트를 생성합니다. Spring Initializr는 Spring Boot 프로젝트를 생성하는 데 사용할 수 있는 웹 기반 도구입니다.

다음 옵션을 선택합니다.

- 프로젝트: 메이븐 프로젝트
- 언어: 자바
- 스프링 부트 버전: 2.1.0
- 프로젝트 메타데이터:
  - 그룹: com.example
  - 아티팩트: my-app
  - 이름: 마이앱
  - 설명 : 간단한 Spring Boot 어플리케이션
  - 패키지 이름: com.example.myapp
- 포장: 항아리
- 자바 버전: 1.8
- 종속성:
  - 웹
  - 텐서플로우

프로젝트가 생성되면 선택한 IDE로 가져올 수 있습니다.

## TensorFlow 통합

TensorFlow는 기계 학습 모델을 구축하고 교육하는 데 사용할 수 있는 오픈 소스 기계 학습 플랫폼입니다.

프로젝트에 TensorFlow를 추가하려면 pom.xml 파일에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.tensorflow</groupId>
    <artifactId>tensorflow-core</artifactId>
    <version>1.10.0</version>
</dependency>
```

## 기계 학습 모델 구축

이제 프로젝트가 설정되었으므로 기계 학습 모델 구축을 시작할 수 있습니다.

MyModel이라는 새 클래스를 만드는 것으로 시작하겠습니다. 이 클래스에는 기계 학습 모델이 포함됩니다.

```java
public class MyModel {

}
```

다음으로 다음 가져오기 문을 추가해야 합니다.

```java
import org.tensorflow.Tensor;
import org.tensorflow.TensorFlow;
```

이제 모델 구축을 시작할 수 있습니다. 입력 및 출력 텐서를 정의하는 것으로 시작하겠습니다. 입력 텐서는 모양 [1, 2]의 2D 텐서입니다. 출력 텐서는 모양 [1]의 1D 텐서입니다.

```java
public class MyModel {

    private static final int INPUT_SIZE = 2;
    private static final int OUTPUT_SIZE = 1;

    private static final Tensor<Float> input = Tensor.create(new float[][] {
        {1.0f, 2.0f}
    }, Float.class);

    private static final Tensor<Float> output = Tensor.create(new float[] {
        3.0f
    }, Float.class);
}
```

다음으로 모델을 정의합니다. 간단한 선형 회귀 모델을 사용합니다.

```java
public class MyModel {

    private static final int INPUT_SIZE = 2;
    private static final int OUTPUT_SIZE = 1;

    private static final Tensor<Float> input = Tensor.create(new float[][] {
        {1.0f, 2.0f}
    }, Float.class);

    private static final Tensor<Float> output = Tensor.create(new float[] {
        3.0f
    }, Float.class);

    private static final LinearRegressionModel model = LinearRegressionModel.create(
        input, output);
}
```

이제 모델을 훈련할 수 있습니다. 모델을 1000회 반복 학습합니다.

```java
public class MyModel {

    private static final int INPUT_SIZE = 2;
    private static final int OUTPUT_SIZE = 1;

    private static final Tensor<Float> input = Tensor.create(new float[][] {
        {1.0f, 2.0f}
    }, Float.class);

    private static final Tensor<Float> output = Tensor.create(new float[] {
        3.0f
    }, Float.class);

    private static final LinearRegressionModel model = LinearRegressionModel.create(
        input, output);

    public static void main(String[] args) {
        for (int i = 0; i < 1000; i++) {
            model.train();
        }
    }
}
```

마지막으로 훈련된 모델을 사용하여 예측할 수 있습니다.

```java
public class MyModel {

    private static final int INPUT_SIZE = 2;
    private static final int OUTPUT_SIZE = 1;

    private static final Tensor<Float> input = Tensor.create(new float[][] {
        {1.0f, 2.0f}
    }, Float.class);

    private static final Tensor<Float> output = Tensor.create(new float[] {
        3.0f
    }, Float.class);

    private static final LinearRegressionModel model = LinearRegressionModel.create(
        input, output);

    public static void main(String[] args) {
        for (int i = 0; i < 1000; i++) {
            model.train();
        }

        Tensor<Float> prediction = model.predict(input);
        System.out.println(prediction.data());
    }
}
```

## 결론

이 게시물에서는 Spring Boot와 TensorFlow를 사용하여 기계 학습 애플리케이션을 빌드하는 방법을 살펴보았습니다. 우리는 기계 학습이 무엇이며 응용 프로그램을 구축하는 데 어떻게 사용될 수 있는지 살펴보는 것으로 시작했습니다. 그런 다음 Spring Boot 프로젝트를 설정하고 TensorFlow를 통합하는 방법을 살펴보았습니다. 마지막으로 TensorFlow를 사용하여 기계 학습 모델을 구축하는 방법에 대한 간단한 예를 살펴보았습니다.