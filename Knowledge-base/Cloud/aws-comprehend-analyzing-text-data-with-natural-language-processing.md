---
title: AWS Comprehend: 자연어 처리로 텍스트 데이터 분석
description: 
published: true
date: 2023-02-14T21:17:26.018Z
tags: 
editor: markdown
dateCreated: 2023-02-14T21:17:18.354Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS Comprehend: Analyzing Text Data with Natural Language Processing***English** document is available*](/en/Knowledge-base/Cloud/aws-comprehend-analyzing-text-data-with-natural-language-processing)
{.links-list}



# AWS Comprehend: 자연어 처리로 텍스트 데이터 분석

텍스트 데이터는 어디에나 있습니다. 우리가 읽는 책, 소비하는 뉴스, 공유하는 소셜 미디어 게시물, 구매 결정을 내릴 때 의존하는 고객 리뷰에 있습니다. 이 데이터는 믿을 수 없을 정도로 가치가 있을 수 있지만 그 의미를 추출할 수 있는 경우에만 가능합니다.

자연어 처리(NLP)는 컴퓨터와 인간(자연) 언어 간의 상호 작용을 다루는 컴퓨터 과학 및 인공 지능 분야입니다. NLP는 텍스트 데이터에서 의미를 자동으로 해석하고 추출할 수 있는 애플리케이션을 구축하는 데 사용됩니다.

AWS Comprehend는 텍스트 데이터에서 의미를 쉽게 추출할 수 있게 해주는 완전 관리형 NLP 서비스입니다. 이 기사에서는 AWS Comprehend를 사용하여 텍스트 데이터를 분석하는 방법을 살펴보겠습니다.

## AWS Comprehend 시작하기

AWS Comprehend를 사용하기 전에 AWS 계정을 설정하고 서비스 액세스 권한이 있는 IAM 사용자를 생성해야 합니다.

AWS 계정이 있으면 다음 정책으로 IAM 사용자를 생성할 수 있습니다.

```{language} {code}
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "comprehend:*"
            ],
            "Resource": "*"
        }
    ]
}
```

IAM 사용자가 있으면 이제 AWS Comprehend 리소스를 생성할 수 있습니다. 이렇게 하려면 AWS Management Console에 로그인하고 AWS Comprehend 서비스로 이동해야 합니다.

AWS Comprehend 콘솔에 있으면 새 리소스를 생성할 수 있습니다. 리소스의 이름을 제공하고 리전을 선택한 다음 이전에 생성한 IAM 역할을 선택해야 합니다.

리소스가 생성되었으므로 이제 AWS Comprehend를 사용할 준비가 되었습니다.

## 텍스트 데이터 분석

AWS Comprehend는 텍스트 데이터를 분석하는 다양한 방법을 제공합니다. 이 섹션에서는 가장 일반적으로 사용되는 몇 가지 기능을 살펴보겠습니다.

### 감정 분석

감정 분석은 텍스트 조각에서 감정(긍정적, 부정적 또는 중립적)을 자동으로 추출하는 방법입니다. 이것은 고객 리뷰의 전반적인 감정을 결정하거나 소셜 미디어 게시물의 감정을 이해하는 것과 같은 다양한 애플리케이션에 유용할 수 있습니다.

AWS Comprehend로 감정 분석을 수행하려면 분석하려는 텍스트를 제공해야 합니다. 텍스트를 직접 입력하거나 텍스트가 있는 URL을 제공하여 이를 수행할 수 있습니다.

텍스트를 제공하면 AWS Comprehend가 텍스트를 분석하고 텍스트의 감정을 제공합니다.

### 핵심 구문 추출

핵심 구 추출은 텍스트에서 핵심 구를 자동으로 식별하는 방법입니다. 이것은 고객 리뷰의 주제를 식별하거나 소셜 미디어 게시물의 주제를 이해하는 것과 같은 다양한 애플리케이션에 유용할 수 있습니다.

AWS Comprehend로 핵심 구 추출을 수행하려면 분석하려는 텍스트를 제공해야 합니다. 텍스트를 직접 입력하거나 텍스트가 있는 URL을 제공하여 이를 수행할 수 있습니다.

텍스트를 제공하면 AWS Comprehend가 텍스트를 분석하고 추출한 핵심 문구를 제공합니다.

### 언어 감지

언어 감지는 텍스트 조각의 언어를 자동으로 식별하는 방법입니다. 이것은 고객 리뷰의 언어를 식별하거나 소셜 미디어 게시물의 언어를 이해하는 것과 같은 다양한 애플리케이션에 유용할 수 있습니다.

AWS Comprehend로 언어 감지를 수행하려면 분석하려는 텍스트를 제공해야 합니다. 텍스트를 직접 입력하거나 텍스트가 있는 URL을 제공하여 이를 수행할 수 있습니다.

텍스트를 제공하면 AWS Comprehend가 텍스트를 분석하고 감지한 언어를 제공합니다.

## 결론

이 기사에서는 AWS Comprehend를 사용하여 텍스트 데이터를 분석하는 방법을 살펴보았습니다. AWS Comprehend를 사용하여 감정 분석, 핵심 구 추출 및 언어 감지를 수행하는 방법을 살펴보았습니다.

AWS Comprehend로 가능한 것의 표면만 살펴봤지만 시작하기에 충분할 것입니다.