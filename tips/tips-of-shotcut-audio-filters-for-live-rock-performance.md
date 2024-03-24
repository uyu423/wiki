---
title: Shotcut 라이브 락 공연 Audio Filter 조절 수치 (개인적)
description: 단일 마이크로 촬영된 락 공연의 노이즈와 음향 최적화를 위한 개인적은 Audio Filters 설정
published: true
date: 2024-03-24T16:53:05.740Z
tags: shotcut
editor: markdown
dateCreated: 2024-03-24T13:45:15.839Z
---

> • 단일 마이크로 녹음된 라이브 락 공연의 Shotcut 오디오 필터 종류와 구체적인 수치입니다.
> • 당연히 영상의 음향과 상황에 따라 수치는 다르게 적용될 수 있어야합니다.
{.is-info}

## Shotcut Audio Filter 순서

- Noise Gate
- High Pass
- Low Pass
- Equalizer: 15-Band
- Normalize: One Pass
- Compressor
- Limiter
- Gain / Volume

## Noise Gate

### Key Filter: Low Frequency

- 40 Hz
- 이 값은 매우 낮은 주파수의 잡음을 필터링하는 데 도움이 됩니다. 

### Key Filter: High Frequency: 12000 Hz

- 고주파수 잡음을 줄이는 데 사용

### Threshold: -15.0 dB

- -20dB부터 시작해 조정. 
- 잡음과 음악 사이의 경계를 정의

### Attack: 50 ms

- 노이즈 리덕션 효과가 시작되기까지의 시간

### Hold: 200 ms
- 임계값 아래로 떨어진 후 노이즈 리덕션이 계속 적용되는 시간

### Decay: 150 ms
- 노이즈 리덕션이 소리에 더 이상 적용되지 않기 시작하는데까지 걸리는 시간

### Range: -6.0 dB

- 노이즈 리덕션의 최대 감소량
- 너무 큰 값을 설정하면 음악의 일부가 손실될 위험이 있음

## High Pass

- Cutoff Frequency: 80 Hz
-  Rolloff rate: 5
- Dry/Wet: 100%

## Low Filter

- Cutoff Frequency: 8,000 Hz ~ 15,000 Hz
  - 라이브 영상의 경우 8,000 Hz 가 넘는 부분이 있을 수 있어서 너무 낮으면 하이 부분이 뭉탱이로 잘려나가는 느낌이 있음
- Rolloff rate: 5
- Dry/Web: 100%

## Equalizer: 15-Band

![스크린샷_2024-03-24_22.26.17.png](/스크린샷_2024-03-24_22.26.17.png){.align-left}

### 보컬

- 2500 Hz (존재감)
- 3500 Hz (명료성)
- 5000 Hz (공간감, 기타와 겹침)

### 드럼

- 100 Hz (킥 베이스)
- 156 Hz (스네어 바디 밸런스)
- 5000 Hz (심벌, 하이햇)

### 베이스

- 100 Hz
- 311 Hz (베이스에서 발생할 수 있는 mud 제거)

### 일렉 기타

- 440 Hz (불필요한 중첩 감소)
- 2500 Hz (기타 솔로 및 리듬 파트 선명도)
- 5000 Hz (스트링 질감, 보컬과 겹침)

### 노이즈 및 톤

- 50 Hz (무대 진동, 저주파 잡음)
- 10000 Hz (과도한 심벌, 하이햇 소음 감소)
- 20000 Hz (고주파 잡음)

## Normalize: One Pass

### Target Loudness: 16.0 LUFS

- -23 LUFS (EBU R128 권장 값) 또는 -16 LUFS (스트리밍 플랫폼에 더 적합한 레벨) 중 선택

### Analysis Window: 5 s

- 3 sec ~ 5 sec

### Maximum Gain: 15.0 dB

- 너무 낮은 부분을 적절한 볼륨으로 끌어올릴 수 있게함

### Minimum Gain: -5.0 dB

- 이는 필요 이상으로 소리가 줄어드는 것을 방지

### Maximum Rate: 2.0 dB/s

- 이는 볼륨 변화가 너무 급격하게 발생하는 것을 방지

### Reset on discontinuity: off

- 일관된 오디오 스트림이면 체크 해제

## Compressor

### RMS: 50.0%

- RMS는 신호의 평균적인 볼륨을 측정하는 방법
- 평균 볼륨을 기준으로 압축을 시작하겠다는 의미

### Attack: 10 ms

- 컴프레셔가 작동하기 시작하는데 걸리는 시간
- 10 ms ~ 30 ms

### Release: 40 ms

- 컴프레셔가 작동을 멈추고 원래 상태로 돌아가는 데 걸리는 시간
- 음악의 리듬과 동적 변화를 자연스럽게 처리
- 40 ms ~ 100 ms

### Threshold: -10.0 dB

- 컴프레셔가 작동하기 시작하는 볼륨 레벨
- 20 dB ~ -10 dB

### Ratio: 1:4

- 압축 비율
- 1:4 ~ 1:8 
  - 신호가 임계값을 넘어서면, 신호의 4~8배만큼 압축되어 출력


### Knee radius: 6.0 dB

- 압축이 시작되는 지점의 부드러움
- 6 dB ~ 12 dB

### Makup gain: 3.0 dB

- 컴프레셔로 인해 감소된 볼륨을 보상
- 3 dB ~ 6 dB

## Limiter

### Input gain: 0 dB

- 신호의 초기 볼륨을 조정
- 0 부터 시작해서 너무 작으면 증가

### Limit: -0.1 dB

- 신호의 최대 레벨 (-1 dB ~ -0.1 dB 사이)

### Release: 0.05 s

- 리미터가 한번 작동한 후 다시 원래 대로 돌아오는데 걸리는 시간 (0.05 ~ 0.2)

## Gain / Volume

- 전체적인 평균 Audio Peek Meter가 -6 dB 에서 -3 dB 정도가 되도록 설정
- 유튜브 같은곳에 올린다면 어차피 인코딩 되면서 대충 볼륨 맞춰줌