---
title: AWS Transcribe: 클라우드에서 음성-텍스트 변환 자동화
description: 
published: true
date: 2023-02-19T03:32:30.303Z
tags: 
editor: markdown
dateCreated: 2023-02-19T03:32:22.713Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS Transcribe: Automating Speech-to-Text Transcription in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-transcribe-automating-speech-to-text-transcription-in-the-cloud)
{.links-list}


# AWS Transcribe: 클라우드에서 음성 텍스트 변환 자동화

오디오 및 비디오 파일을 기록하는 것은 시간이 많이 걸리고 오류가 발생하기 쉬운 작업이며 여러 명의 화자가 관련된 경우에만 복잡해집니다. AWS Transcribe는 거의 실시간으로 다양한 언어로 된 오디오 파일을 쉽게 전사할 수 있는 자동 음성 인식(ASR) 서비스입니다.

AWS Transcribe는 고객 서비스 통화, 인터뷰, 강의, 연설 등을 기록하는 데 사용할 수 있습니다. 이 서비스는 AWS Management Console, AWS 명령줄 인터페이스(CLI) 및 AWS SDK를 통해 액세스할 수 있습니다.

## AWS Transcribe 시작하기

AWS Transcribe를 시작하려면 계정을 만들고 [AWS Management Console](https://console.aws.amazon.com/)에 로그인합니다. 로그인한 후 **Transcribe** 서비스 페이지로 이동하여 **작업 만들기**를 클릭합니다.

![](https://i.imgur.com/pkzL0bj.png)

다음 페이지에서 기록할 입력 파일을 선택하라는 메시지가 표시됩니다. 파일은 Amazon Simple Storage Service(S3) 버킷에 저장해야 합니다. 또한 입력 파일의 언어와 화자 인식 활성화 여부를 지정할 수 있습니다.

![](https://i.imgur.com/sTm7rTz.png)

입력 파일을 선택했으면 **작업 만들기**를 클릭하여 전사 프로세스를 시작합니다. 작업 진행 상황은 **작업** 페이지에서 모니터링할 수 있습니다.

![](https://i.imgur.com/GpqoNcu.png)

기록 작업이 완료되면 일반 텍스트 또는 JSON 형식으로 기록을 다운로드할 수 있습니다.

![](https://i.imgur.com/Wql4Vfy.png)

## AWS Transcribe 요금

AWS Transcribe는 기록되는 오디오 파일의 길이에 따라 가격이 책정됩니다. 전사의 처음 60분은 무료이며 그 이후에는 분당 $0.006입니다. 예를 들어, 1시간 분량의 오디오 파일을 녹음하는 데 드는 비용은 $0.36입니다.

오디오 파일의 길이에 관계없이 각 필사 작업에 대해 $0.0001의 작업당 수수료가 부과됩니다.

## AWS Transcribe 제한

다음을 포함하여 AWS Transcribe 작업에 적용되는 몇 가지 제한이 있습니다.

- 입력 파일의 최대 크기는 160MB입니다.
- 입력 파일의 최대 길이는 2시간입니다.
- 대기할 수 있는 최대 작업 수는 1000개입니다.
- 동시에 실행할 수 있는 최대 작업 수는 100개입니다.

## AWS Transcribe 사용 모범 사례

다음은 AWS Transcribe를 사용할 때 염두에 두어야 할 몇 가지 모범 사례입니다.

- 전사의 오류를 최소화하기 위해 오디오 품질을 가능한 한 높게 유지하십시오.
- 오디오 파일이 MP3, WAV 또는 FLAC와 같은 지원되는 형식인지 확인하십시오.
- 전사 비용을 최소화하기 위해 짧은 오디오 파일(<10분)을 전사합니다.
- 화자 인식을 사용하여 대본에서 다른 화자에 레이블을 지정합니다.

## 결론

AWS Transcribe는 오디오 파일을 기록할 때 많은 시간과 노력을 절약할 수 있는 강력한 ASR 서비스입니다. 서비스를 최대한 활용하려면 이 문서에 설명된 모범 사례를 따르십시오.