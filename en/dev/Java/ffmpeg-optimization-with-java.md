---
title: Optimizing ffmpeg performance with Java
description: Small tips for using ffmpeg in Java environment
published: true
date: 2023-02-17T18:00:47.081Z
tags: english, ffmpeg, java
editor: markdown
dateCreated: 2023-01-25T13:29:26.894Z
---

- [ffmpeg 성능 최적화 with Java***Korean** version of this document is available*](/ko/dev/Java/ffmpeg-optimization-with-java)
{.links-list}

## Optimize output quality of ffmpeg

- The quality of the result can be optimized with CRF (Constant Rate Factor) and Audio Quality Scale.
- We use `-crf 18` and `-qscale:a 6` so as not to greatly damage the original quality.

### with Java

- If you use the `net.bramp.ffmpeg` package in Java, you can apply CRF and Audio Quality Sacle as follows.

```java
FFmpegOutputBuilder output = new FFmpegOutputBuilder()
    .setConstantRateFactor(18)
    .setAudioQuality(6)
    .setFilename(extractedFile.getPath());
```

### CRF test

- When the CRF value was changed based on 1080p video, the following results were obtained as a result of the test.


#### original file
-filesize: 31.4MB

```
ffprobe test_origin.mp4

  Duration: 00:02:00.04, start: 0.000000, bitrate: 2091 kb/s
  Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 192 kb/s (default)
```

#### No CRF (CRF Default 23)
- Default when `-crf` option is not given
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

#### CRF 0 (Lossless)
- filesize: 495.1MB
```
  Duration: 00:02:00.00, start: 0.000000, bitrate: 33004 kb/s
  Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 128 kb/s (default)
```

## Limit CPU Usage

- In an infrastructure environment, if `ffmpeg` consumes 100% of CPU resources, there can be a lot of problems.
- There is no option to limit CPU usage directly provided by `ffmpeg`, but it can be controlled indirectly through `-threads` option.

### If you do not use the -threads option

```bash
ffmpeg -y -v error -ss 01:10:30 -t 120 \
   -i /Users/user/Movies/a6fd876f-72db-11ec-9990-246e963a41ed.mp4 \
   -crf 18 -qscale:a 6 \
   /var/folders/9w/wbdl0s1s67vc1rv789307n9h0000gn/T/video-11194128045073791782/shortclip-4230-4350_a6fd876f-72db-11ec-9990-246e963a41ed.mp4
```

- Duration: 15sec 464ms

![c5ba17d3-ae4e-4257-a681-29811a064d92.png](/c5ba17d3-ae4e-4257-a681-29811a064d92.png)

### When using the -threads option

```bash
ffmpeg -y -v error -ss 01:10:30 -t 120 \
   -i /Users/user/Movies/a6fd876f-72db-11ec-9990-246e963a41ed.mp4 \
   -crf 18 -qscale:a 6 -threads 7 \
   /var/folders/9w/wbdl0s1s67vc1rv789307n9h0000gn/T/video-14701788610086880799/shortclip-4230-4350_a6fd876f-72db-11ec-9990-246e963a41ed.mp4
```

- Show time: 23sec 172ms

![74df05b8-7638-4eb7-a95b-f8098d897163.png](/74df05b8-7638-4eb7-a95b-f8098d897163.png)

### with Java

- If you use the `net.bramp.ffmpeg` package in Java, you can calculate and apply threads as follows.
- The code below gave an option to use roughly 70% of the number of threads of the CPU core.

```java
int cores = Runtime.getRuntime().availableProcessors();

FFmpegOutputBuilder output = new FFmpegOutputBuilder()
     .setConstantRateFactor(FFMPEG_OUTPUT_CRF)
     .setAudioQuality(FFMPEG_AUDIO_QUALITY_SCALE)
     .addExtraArgs("-threads", String.valueOf((int)Math.floor(cores * 0.7)))
     .setFilename(extractedFile.getPath());
```

> The order in which the `-threads` options are added can be a problem.
> For example, `ffmpeg -i input.mp4 -threads 4 output.mp4` works with the `-threads` option, but
> For `ffmpeg -threads 4 -i input.mp4 output.mp4`, the `-threads` option does not work properly.
{.is-warning}