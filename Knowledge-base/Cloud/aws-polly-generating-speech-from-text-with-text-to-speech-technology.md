---
title: AWS Polly: 텍스트 음성 변환 기술로 텍스트에서 음성 생성
description: 
published: true
date: 2023-02-05T19:17:34.870Z
tags: 
editor: markdown
dateCreated: 2023-02-05T19:17:33.180Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS Polly: Generating Speech from Text with Text-to-Speech Technology***English** document is available*](/en/Knowledge-base/Cloud/aws-polly-generating-speech-from-text-with-text-to-speech-technology)
{.links-list}


# AWS Polly: 텍스트 음성 변환 기술로 텍스트에서 음성 생성

TTS(텍스트 음성 변환) 기술은 텍스트를 자연스러운 음성으로 변환합니다. 텍스트를 읽는 데 도움이 되거나 게임이나 비디오에서 캐릭터의 생생한 음성을 생성하는 데 사용할 수 있습니다. TTS 기술은 또한 오디오 북을 만들거나 맹인 또는 시력이 낮은 사람들을 위해 이미지의 오디오 설명을 제공하는 데 사용되고 있습니다.

AWS Polly는 딥 러닝 알고리즘을 사용하여 텍스트를 생생한 음성으로 변환하는 TTS 서비스입니다. Polly는 여러 언어와 음성을 지원하므로 자신의 언어 또는 다른 언어로 음성을 생성할 수 있습니다.

폴리는 사용하기 쉽습니다. 음성으로 변환하려는 텍스트를 Polly API로 보내기만 하면 Polly가 이를 애플리케이션에서 다운로드하거나 재생할 수 있는 오디오 파일로 변환합니다.

Polly는 대용량 트래픽을 처리할 수 있는 확장 가능한 TTS 서비스입니다. 용량 계획이나 서버 인프라 관리에 대해 걱정할 필요 없이 Polly를 사용하여 규모에 맞게 음성을 생성할 수 있습니다.

## Polly는 어떻게 작동하나요?

Polly는 딥 러닝 알고리즘을 사용하여 텍스트를 음성으로 변환합니다. 이 알고리즘은 실제 사람의 음성 데이터 세트에서 학습되므로 사람의 음성 패턴을 모방하는 방법을 학습할 수 있습니다.

Polly는 여러 언어와 음성을 지원합니다. 각 음성에는 피치, 속도 및 억양과 같은 고유한 특성 세트가 있습니다. 애플리케이션에 적합한 음성을 선택할 수 있습니다.

Polly는 한 번에 한 단어씩 텍스트를 음성으로 변환합니다. 먼저 텍스트를 일련의 음소로 나눈 다음 음소를 선택한 음성의 해당 소리에 매핑합니다.

Polly는 실시간으로 텍스트에서 음성을 생성하거나 미리 녹음된 텍스트에서 음성을 생성할 수 있습니다.

## Polly를 사용하면 어떤 이점이 있나요?

Polly는 기존 TTS 시스템에 비해 여러 가지 이점이 있습니다.

- **자연스러운 음성:** Polly는 딥 러닝 알고리즘을 사용하여 자연스럽고 사람처럼 들리는 음성을 생성합니다.

- **다국어 및 음성 지원:** Polly는 다양한 언어와 음성을 지원하므로 자신의 언어 또는 다른 언어로 음성을 생성할 수 있습니다.

- **확장 가능:** Polly는 대용량 트래픽을 처리할 수 있는 확장 가능한 TTS 서비스입니다. 용량 계획이나 서버 인프라 관리에 대해 걱정할 필요 없이 Polly를 사용하여 규모에 맞게 음성을 생성할 수 있습니다.

## Polly를 사용하면 어떤 단점이 있나요?

폴리는 완벽하지 않습니다. 다음은 Polly 사용의 몇 가지 단점입니다.

- **정확도:** Polly는 100% 정확하지 않습니다. Polly가 음성을 생성하는 데 사용하는 딥 러닝 알고리즘은 완벽하지 않으며 때때로 실수를 합니다.

- **비용:** Polly는 종량제 서비스이므로 음성으로 변환하는 문자 수에 따라 요금이 부과됩니다.

- **대기 시간:** Polly는 음성을 생성하는 데 시간이 걸립니다. 걸리는 시간은 텍스트의 길이와 사용된 알고리즘의 복잡성에 따라 달라집니다.

## Polly 비용은 얼마인가요?

Polly는 종량제 서비스입니다. 음성으로 변환하는 문자 수에 따라 요금이 부과됩니다. 가격은 선택한 음성과 Polly를 사용하는 지역에 따라 다릅니다.

## Polly를 시작하려면 어떻게 해야 하나요?

Polly를 시작하려면 먼저 AWS 계정을 생성해야 합니다. 그런 다음 AWS Management Console을 사용하여 Polly 음성을 생성할 수 있습니다.

음성을 만든 후에는 Polly API를 사용하여 텍스트를 음성으로 변환할 수 있습니다. Polly API는 자체 애플리케이션에서 호출할 수 있는 웹 서비스입니다.

## Polly의 사용 사례에는 어떤 것이 있나요?

Polly는 다음을 포함하여 광범위한 애플리케이션에 사용할 수 있습니다.

- **텍스트 음성 변환:** Polly를 사용하여 텍스트를 음성으로 변환할 수 있습니다. 이것은 오디오 북을 만들거나 맹인 또는 시력이 낮은 사람들을 위해 이미지의 오디오 설명을 제공하는 데 사용할 수 있습니다.

- **Speech-to-text:** Polly를 사용하여 음성을 텍스트로 변환할 수 있습니다. 이것은 연설의 대본을 만들거나 비디오의 캡션을 만드는 데 사용할 수 있습니다.

- **몰입형 경험:** Polly를 사용하여 게임이나 비디오에서 캐릭터의 생생한 목소리를 만들 수 있습니다.