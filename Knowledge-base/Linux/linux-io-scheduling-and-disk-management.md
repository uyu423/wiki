---
title: Linux I/O 스케줄링 및 디스크 관리
description: 
published: true
date: 2023-02-11T17:32:34.237Z
tags: 
editor: markdown
dateCreated: 2023-02-11T17:32:32.647Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Linux I/O Scheduling and Disk Management***English** document is available*](/en/Knowledge-base/Linux/linux-io-scheduling-and-disk-management)
{.links-list}


# Linux I/O 스케줄링 및 디스크 관리

Linux 커널의 I/O 스케줄러는 커널 블록 계층의 블록 I/O 요청이 저장 장치에 제출되는 순서를 최적화하는 역할을 합니다. I/O 스케줄링이라고 하는 이 프로세스는 시스템 성능에 상당한 영향을 미칠 수 있습니다.

I/O 스케줄링에는 세 가지 주요 목표가 있습니다.

- 검색을 최소화하기 위해 요청을 재정렬하여 성능 향상
- 요청을 병합하여 성능 향상
- I/O 우선순위가 낮은 프로세스의 요청에 우선순위를 부여하여 대기 시간 감소

Linux 커널의 I/O 스케줄러는 이 세 가지 목표의 균형을 맞추도록 설계되었습니다.

## I/O 스케줄링 알고리즘

Linux 커널에서 사용할 수 있는 세 가지 I/O 스케줄링 알고리즘이 있습니다.

- 데드라인 I/O 스케줄러
- Noop I/O 스케줄러
- CFQ I/O 스케줄러

Deadline I/O 스케줄러는 Linux 커널의 기본 I/O 스케줄러입니다. I/O 우선 순위가 낮은 프로세스의 요청에 우선 순위를 부여하여 대기 시간을 최소화하도록 설계되었습니다.

Noop I/O 스케줄러는 요청을 재정렬하지 않는 매우 간단한 I/O 스케줄러입니다. 일반적으로 솔리드 스테이트 드라이브와 같이 I/O 대기 시간이 매우 짧은 장치에 사용됩니다.

CFQ I/O 스케줄러는 대부분의 Linux 배포판에서 기본 I/O 스케줄러입니다. I/O 스케줄링의 세 가지 목표인 검색 시간 최소화, 요청 병합 및 대기 시간 감소의 균형을 맞추도록 설계되었습니다.

## I/O 스케줄러 변경

I/O 스케줄러는 `blockdev` 명령의 `-s` 옵션을 사용하여 장치별로 변경할 수 있습니다. 예를 들어 `/dev/sda`의 I/O 스케줄러를 Deadline I/O 스케줄러로 변경하려면 다음 명령을 사용합니다.

```
blockdev -s /dev/sda deadline
```

I/O 스케줄러는 파일 시스템별로 변경할 수도 있습니다. `/` 파일 시스템의 I/O 스케줄러를 CFQ I/O 스케줄러로 변경하려면 다음 명령을 사용합니다.

```
mount -o remount,ioscheduler=cfq /
```

## I/O 스케줄링 및 디스크 관리

I/O 스케줄러는 디스크 성능에 상당한 영향을 미칠 수 있습니다. 예를 들어 Deadline I/O 스케줄러는 I/O 우선 순위가 낮은 프로세스의 요청에 우선 순위를 부여하여 대기 시간을 최소화하도록 설계되었습니다. 이로 인해 데이터베이스 서버와 같이 I/O 우선 순위가 높은 프로세스의 성능이 향상될 수 있습니다.

CFQ I/O 스케줄러는 I/O 스케줄링의 세 가지 목표(검색 시간 최소화, 요청 병합 및 대기 시간 감소)의 균형을 맞추도록 설계되었습니다. 이로 인해 대부분의 워크로드에서 성능이 향상될 수 있습니다.

## 결론

Linux 커널의 I/O 스케줄러는 커널 블록 계층의 블록 I/O 요청이 저장 장치에 제출되는 순서를 최적화하는 역할을 합니다. I/O 스케줄링의 세 가지 주요 목표는 검색을 최소화하기 위해 요청을 재정렬하여 성능을 개선하고, 요청을 병합하여 성능을 개선하고, I/O 우선 순위가 낮은 프로세스의 요청에 우선 순위를 부여하여 대기 시간을 줄이는 것입니다.

I/O 스케줄러는 디스크 성능에 상당한 영향을 미칠 수 있습니다. Deadline I/O 스케줄러는 I/O 우선 순위가 낮은 프로세스의 요청에 우선 순위를 부여하여 대기 시간을 최소화하도록 설계되었습니다. CFQ I/O 스케줄러는 I/O 스케줄링의 세 가지 목표(검색 시간 최소화, 요청 병합 및 대기 시간 감소)의 균형을 맞추도록 설계되었습니다.

## 자원

- [리눅스 I/O 스케줄링](https://www.kernel.org/doc/Documentation/block/ioprio.txt)
- [I/O 스케줄러](https://en.wikipedia.org/wiki/I/O_scheduler)
- [Noop I/O 스케줄러](https://www.kernel.org/doc/Documentation/block/noop-iosched.txt)
- [CFQ I/O 스케줄러](https://www.kernel.org/doc/Documentation/block/cfq-iosched.txt)
- [데드라인 I/O 스케줄러](https://www.kernel.org/doc/Documentation/block/deadline-iosched.txt)