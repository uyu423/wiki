---
title: ffmpeg 성능 최적화 with Java
description: Java 환경에서 ffmpeg를 사용할 때의 소소한 꿀팁들
published: true
date: 2023-02-17T18:00:45.724Z
tags: java, ffmpeg
editor: markdown
dateCreated: 2023-01-25T10:23:02.739Z
---

- [Optimizing ffmpeg performance with Java***English** version of this document is available*](/en/dev/Java/ffmpeg-optimization-with-java)
{.links-list}

## ffmpeg 결과물 품질 최적화

- CRF(Constant Rate Factor)와 Audio Quality Scale로 결과물의 품질을 최적화 시켜줄 수 있다.
- 적당히 원본 퀄리티를 크게 손상하지 않도록 `-crf 18`, `-qscale:a 6` 정도로 사용하고 있다.

### with Java

- Java에서 `net.bramp.ffmpeg` 패키지를 사용한다면 다음과 같이 CRF와 Audio Quality Sacle을 적용할 수 있다.

```java
FFmpegOutputBuilder output = new FFmpegOutputBuilder()
    .setConstantRateFactor(18)
    .setAudioQuality(6)
    .setFilename(extractedFile.getPath());
```

### CRF 테스트

- 1080p 영상 기준으로 CRF 수치를 변경하면 테스트한 결과 다음과 같은 결과 값을 얻었다.


#### 원본 파일
- filesize: 31.4MB
```
ffprobe test_origin.mp4

  Duration: 00:02:00.04, start: 0.000000, bitrate: 2091 kb/s
  Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 192 kb/s (default)
```

#### No CRF (CRF Default 23)
- `-crf` 옵션을 주지 않았을 때의 기본 
- filesize: 26.7MB
```
  Duration: 00:02:00.00, start: 0.000000, bitrate: 1781 kb/s
  Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 128 kb/s (default)
```

#### CRF 22
- filesize: 29.3MB
```
  Duration: 00:02:00.00, start: 0.000000, bitrate: 1956 kb/s
  Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 128 kb/s (default)
```

#### CRF 21
- filesize: 32.2MB
```
  Duration: 00:02:00.00, start: 0.000000, bitrate: 2143 kb/s
  Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 128 kb/s (default)
```

#### CRF 20
- filesize: 35.2MB
```
  Duration: 00:02:00.00, start: 0.000000, bitrate: 2345 kb/s
  Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 128 kb/s (default)
```

#### CRF 18
- filesize: 42.4MB
```
  Duration: 00:02:00.00, start: 0.000000, bitrate: 2829 kb/s
  Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 128 kb/s (default)
```

#### CRF 0 (무손실)
- filesize: 495.1MB
```
  Duration: 00:02:00.00, start: 0.000000, bitrate: 33004 kb/s
  Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 128 kb/s (default)
```

## CPU 사용량 제한

- 인프라 환경에서 `ffmpeg`가 CPU 리소스를 100% 다 잡아먹으면 별의 별 문제가 생길 수 있다.
- `ffmpeg`에서 직접적으로 제공하는 CPU 사용량 제한 옵션은 없지만 `-threads` 옵션을 통해 간접적으로 제어를 할 수 있다.

### -threads 옵션을 사용하지 않는 경우

```bash
ffmpeg -y -v error -ss 01:10:30 -t 120 \
  -i /Users/user/Movies/a6fd876f-72db-11ec-9990-246e963a41ed.mp4 \
  -crf 18 -qscale:a 6 \
  /var/folders/9w/wbdl0s1s67vc1rv789307n9h0000gn/T/video-11194128045073791782/shortclip-4230-4350_a6fd876f-72db-11ec-9990-246e963a41ed.mp4
```

- 소요시간: 15sec 464ms

![c5ba17d3-ae4e-4257-a681-29811a064d92.png](/c5ba17d3-ae4e-4257-a681-29811a064d92.png)

### -threads 옵션을 사용하는 경우

```bash
ffmpeg -y -v error -ss 01:10:30 -t 120 \
  -i /Users/user/Movies/a6fd876f-72db-11ec-9990-246e963a41ed.mp4 \
  -crf 18 -qscale:a 6 -threads 7 \
  /var/folders/9w/wbdl0s1s67vc1rv789307n9h0000gn/T/video-14701788610086880799/shortclip-4230-4350_a6fd876f-72db-11ec-9990-246e963a41ed.mp4
```

- 쇼오시간: 23sec 172ms

![74df05b8-7638-4eb7-a95b-f8098d897163.png](/74df05b8-7638-4eb7-a95b-f8098d897163.png)

### with Java

- Java에서 `net.bramp.ffmpeg` 패키지를 사용한다면 다음과 같이 threads를 계산해서 적용해볼 수 있다.
- 아래 코드는 대충 CPU 코어의 70% 갯수의 스레드를 사용한다고 옵션을 주었다.

```java
int cores = Runtime.getRuntime().availableProcessors();

FFmpegOutputBuilder output = new FFmpegOutputBuilder()
    .setConstantRateFactor(FFMPEG_OUTPUT_CRF)
    .setAudioQuality(FFMPEG_AUDIO_QUALITY_SCALE)
    .addExtraArgs("-threads", String.valueOf((int)Math.floor(cores * 0.7)))
    .setFilename(extractedFile.getPath());
```

> `-threads` 옵션이 추가되는 순서가 문제가 될수 있다.
> 예를 들어 `ffmpeg -i input.mp4 -threads 4 output.mp4` 는 `-threads` 옵션이 동작하지만
> `ffmpeg -threads 4 -i input.mp4 output.mp4` 는 `-threads` 옵션이 제대로 동작하지 않는다.
{.is-warning}