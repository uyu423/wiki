---
title: AWS Rekognition: Computer Vision으로 이미지 및 비디오 데이터 분석
description: 
published: true
date: 2023-02-05T17:55:21.860Z
tags: 
editor: markdown
dateCreated: 2023-02-05T17:55:20.298Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS Rekognition: Analyzing Image and Video Data with Computer Vision***English** document is available*](/en/Knowledge-base/Cloud/aws-rekognition-analyzing-image-and-video-data-with-computer-vision)
{.links-list}


# AWS Rekognition: 컴퓨터 비전으로 이미지 및 비디오 데이터 분석

AWS Rekognition은 애플리케이션에 강력한 시각적 분석을 쉽게 추가할 수 있는 클라우드 기반 서비스입니다. Rekognition을 사용하면 이미지와 동영상에서 물체, 장면, 얼굴을 감지하고 부적절한 콘텐츠를 식별할 수 있습니다. Rekognition은 또한 감정, 성별, 연령대 감지와 같은 매우 정확한 얼굴 인식 및 얼굴 분석을 제공합니다. 이러한 기능을 사용하여 콘텐츠를 자동으로 조정하고, 고객을 위한 경험을 개인화하고, 보안을 강화할 수 있는 더 스마트한 애플리케이션을 만들 수 있습니다.

Rekognition은 딥 러닝 알고리즘을 사용하여 이러한 기능을 제공합니다. 딥 러닝은 명시적으로 프로그래밍하지 않고 컴퓨터가 데이터로부터 학습하도록 가르치는 기계 학습의 한 유형입니다. 딥 러닝은 작업별 알고리즘과 달리 학습 데이터 표현을 기반으로 하는 광범위한 기계 학습 방법 계열의 일부입니다.

## Rekognition을 사용하는 이유

Rekognition을 사용하면 애플리케이션에 강력한 시각적 분석을 쉽게 추가할 수 있습니다. Rekognition을 사용하면 이미지와 비디오에서 물체, 얼굴, 장면을 감지하고 부적절한 콘텐츠를 식별할 수 있습니다. Rekognition은 또한 매우 정확한 안면 인식 및 안면 분석을 제공합니다. 이러한 기능을 사용하여 콘텐츠를 자동으로 조정하고, 고객을 위한 경험을 개인화하고, 보안을 강화할 수 있는 더 스마트한 애플리케이션을 만들 수 있습니다.

## Rekognition 시작하기

Rekognition을 시작하려면 먼저 AWS 계정을 만들고 서비스에 가입해야 합니다. 그런 다음 AWS Management Console에서 Rekognition 프로젝트를 생성할 수 있습니다. Rekognition 프로젝트는 Rekognition을 사용하는 데 필요한 모든 리소스의 논리적 컨테이너입니다. 프로젝트를 생성한 후 분석할 이미지와 동영상을 추가하고 분석 결과를 저장할 Amazon Simple Storage Service(Amazon S3) 버킷을 구성할 수 있습니다.

## 이미지 및 비디오 분석

Rekognition을 사용하면 물체, 얼굴, 장면 식별과 같은 다양한 사용 사례에 대해 이미지와 비디오를 쉽게 분석할 수 있습니다. 부적절한 콘텐츠 감지 유명인과 랜드마크를 인식합니다.

Rekognition은 이미지와 비디오를 분석하는 두 가지 주요 방법을 제공합니다.

* **DetectLabels**는 이미지에서 감지된 레이블(예: "개" 또는 "고양이") 목록을 반환합니다. 또한 각 레이블에는 레이블이 올바르게 식별되었다는 Rekognition의 신뢰도를 나타내는 신뢰도 점수가 포함됩니다.

* **DetectModerationLabels**는 이미지에서 안전하지 않거나 부적절한 콘텐츠를 식별하는 레이블 목록을 반환합니다. 예를 들어 "음란한" 또는 "폭력"과 같은 레이블은 이미지에 성인 콘텐츠가 포함되어 있음을 나타냅니다. 또한 각 레이블에는 레이블이 올바르게 식별되었다는 Rekognition의 신뢰도를 나타내는 신뢰도 점수가 포함됩니다.

또한 **AnalyzeFaces** 작업을 사용하여 이미지의 얼굴을 분석하고 감지된 감정, 얼굴의 예상 나이, 얼굴에 선글라스 착용 여부 등 얼굴에 대한 정보를 얻을 수 있습니다.

## 유명인과 랜드마크 인식하기

Rekognition은 이미지에서 유명인과 랜드마크를 인식할 수 있습니다. 예를 들어 **RecognizeCelebrities** 작업을 사용하여 이미지에서 유명인을 식별할 수 있습니다. **DetectLabels** 작업을 사용하여 이미지의 랜드마크를 식별할 수도 있습니다.

## 인식 구현

Rekognition은 AWS SDK를 사용하여 호출할 수 있는 웹 서비스입니다. AWS Management Console, AWS 명령줄 인터페이스를 사용하거나 AWS SDK 중 하나를 사용하여 프로그래밍 방식으로 Rekognition을 호출할 수 있습니다.

## 가격

Rekognition은 분석한 이미지 및 비디오 수와 저장한 얼굴 메타데이터에 대해 비용을 청구합니다. Rekognition은 저장한 이미지 및 비디오 수에 대해 비용을 청구하지 않습니다.

## 자원

* [AWS Rekognition](https://aws.amazon.com/rekognition/)
* [DetectLabels](https://docs.aws.amazon.com/rekognition/latest/dg/API_DetectLabels.html)
* [DetectModerationLabels](https://docs.aws.amazon.com/rekognition/latest/dg/API_DetectModerationLabels.html)
* [AnalyzeFaces](https://docs.aws.amazon.com/rekognition/latest/dg/API_AnalyzeFaces.html)
* [RecognizeCelebrities](https://docs.aws.amazon.com/rekognition/latest/dg/API_RecognizeCelebrities.html)
* [AWS SDK](https://aws.amazon.com/tools/)
* [요금](https://aws.amazon.com/rekognition/pricing/)