---
title: Linux 프로세스 스케줄링
description: 
published: true
date: 2023-02-11T13:32:46.633Z
tags: 
editor: markdown
dateCreated: 2023-02-11T13:32:44.895Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Linux Process Scheduling***English** document is available*](/en/Knowledge-base/Linux/linux-process-scheduling)
{.links-list}


# 리눅스 프로세스 스케줄링

Linux 프로세스 스케줄러는 선점형 우선 순위 기반 스케줄러입니다. 스케줄러는 우선 순위 및 기타 요인에 따라 실행할 다음 프로세스를 선택합니다. 스케줄러는 선입선출(FIFO) 대기열로 구현됩니다.

## 프로세스 스케줄링 알고리즘

Linux 프로세스 스케줄러는 여러 스케줄링 알고리즘을 지원합니다.

* 선입선출(FIFO)
* 라운드 로빈(RR)
* 정적 우선순위 선제 스케줄링(SPP)
* DPP(Dynamic Priority Pre-emptive Scheduling)
* 다중 대기열 스케줄링(MQS)
* 완전히 공정한 스케줄링(CFS)

스케줄러는 다음 알고리즘을 사용하여 실행할 다음 프로세스를 선택합니다.

1. 스케줄러는 우선 순위가 가장 높은 프로세스를 선택합니다.
2. 우선 순위가 같은 프로세스가 여러 개 있을 경우 스케줄러는 가장 오래 대기한 프로세스를 선택합니다.
3. 우선 순위와 대기 시간이 같은 프로세스가 여러 개 있는 경우 스케줄러는 pid가 가장 낮은 프로세스를 선택합니다.

## 프로세스 우선순위

각 프로세스에는 우선 순위가 할당됩니다. 우선 순위는 -20에서 19 사이의 정수 값입니다. 우선 순위 값이 낮을수록 프로세스의 우선 순위가 높습니다. 프로세스의 기본 우선 순위는 0입니다.

`nice` 명령을 사용하여 프로세스에 더 높은 우선 순위를 할당할 수 있습니다. 예를 들어 `firefox` 프로세스에 우선 순위 10을 할당하려면 다음 명령을 사용합니다.

```
$ nice -n 10 firefox
```

`renice` 명령을 사용하여 프로세스에 더 낮은 우선 순위를 할당할 수 있습니다. 예를 들어 `firefox` 프로세스에 -10의 우선 순위를 할당하려면 다음 명령을 사용합니다.

```
$ renice -n -10 firefox
```

## 프로세스 스케줄링 클래스

프로세스는 다음 스케줄링 클래스 중 하나로 분류됩니다.

* 실시간
* 최고의 노력
* 유휴

### 실시간 프로세스

실시간 프로세스가 가장 높은 우선 순위를 갖습니다. 일정이 보장됩니다.

### 최선을 다하는 프로세스

Best-Effort 프로세스는 0에서 99 사이의 우선 순위를 가집니다. 일정이 보장되지는 않습니다.

### 유휴 프로세스

유휴 프로세스의 우선 순위가 가장 낮습니다. 실행할 다른 프로세스가 없을 때만 예약됩니다.

## 프로세스 스케줄링 정책

다음 정책 중 하나를 사용하여 프로세스를 예약할 수 있습니다.

* 선입선출
* RR
* SPP
* DPP
* MQS
* CFS

### FIFO

FIFO는 가장 간단한 스케줄링 정책입니다. 생성된 순서대로 프로세스를 예약합니다.

### RR

RR은 보다 발전된 스케줄링 정책입니다. 라운드 로빈 방식으로 프로세스를 예약합니다.

### SPP

SPP는 정적 우선순위 스케줄링 정책입니다. 정적 우선 순위에 따라 프로세스를 예약합니다.

### DPP

DPP는 동적 우선순위 스케줄링 정책입니다. 동적 우선 순위에 따라 프로세스를 예약합니다.

### MQS

MQS는 다중 대기열 스케줄링 정책입니다. 대기열을 기반으로 프로세스를 예약합니다.

### CFS

CFS는 완전히 공정한 일정 정책입니다. 대기 시간을 기준으로 프로세스를 예약합니다.

## 프로세스 스케줄링 매개변수

Linux 프로세스 스케줄러는 다음 매개변수를 사용하여 프로세스를 예약합니다.

* `nice`: 프로세스의 우선순위.
* `rt_priority`: 프로세스의 실시간 우선순위.
* `policy`: 프로세스의 스케줄링 정책.
* `sched_latency`: 프로세스가 예약되기 전에 지연될 수 있는 최대 시간입니다.
* `sched_min_granularity`: 프로세스 스케줄링 사이의 최소 시간.
* `sched_wakeup_granularity`: 프로세스가 깨어날 때 스케줄 사이의 시간.

## 결론

Linux 프로세스 스케줄러는 선점형 우선 순위 기반 스케줄러입니다. 스케줄러는 우선 순위 및 기타 요인에 따라 실행할 다음 프로세스를 선택합니다. 스케줄러는 선입선출(FIFO) 대기열로 구현됩니다.

스케줄러는 다음 알고리즘을 사용하여 실행할 다음 프로세스를 선택합니다.

1. 스케줄러는 우선 순위가 가장 높은 프로세스를 선택합니다.
2. 우선 순위가 같은 프로세스가 여러 개 있을 경우 스케줄러는 가장 오래 대기한 프로세스를 선택합니다.
3. 우선 순위와 대기 시간이 같은 프로세스가 여러 개 있는 경우 스케줄러는 pid가 가장 낮은 프로세스를 선택합니다.

각 프로세스에는 우선 순위가 할당됩니다. 우선 순위는 -20에서 19 사이의 정수 값입니다. 우선 순위 값이 낮을수록 프로세스의 우선 순위가 높습니다.

프로세스는 다음 스케줄링 클래스 중 하나로 분류됩니다.

* 실시간
* 최고의 노력
* 유휴

실시간 프로세스가 가장 높은 우선 순위를 갖습니다. 일정이 보장됩니다.

Best-Effort 프로세스는 0에서 99 사이의 우선 순위를 가집니다. 일정이 보장되지는 않습니다.

유휴 프로세스의 우선 순위가 가장 낮습니다. 실행할 다른 프로세스가 없을 때만 예약됩니다.

다음 정책 중 하나를 사용하여 프로세스를 예약할 수 있습니다.

* 선입선출
* RR
* SPP
* DPP
* MQS
* CFS

FIFO는 가장 간단한 스케줄링 정책입니다. 생성된 순서대로 프로세스를 예약합니다.

RR은 보다 발전된 스케줄링 정책입니다. 라운드 로빈 방식으로 프로세스를 예약합니다.

SPP는 정적 우선순위 스케줄링 정책입니다. 정적 우선 순위에 따라 프로세스를 예약합니다.

DPP는 동적 우선순위 스케줄링 정책입니다. 동적 우선 순위에 따라 프로세스를 예약합니다.

MQS는 다중 대기열 스케줄링 정책입니다. 대기열을 기반으로 프로세스를 예약합니다.

CFS는 완전히 공정한 일정 정책입니다. 대기 시간을 기준으로 프로세스를 예약합니다.

Linux 프로세스 스케줄러는 다음 매개변수를 사용하여 프로세스를 예약합니다.

* `nice`: 프로세스의 우선순위.
* `rt_priority`: 프로세스의 실시간 우선순위.
* `policy`: 프로세스의 스케줄링 정책.
* `sched_latency`: 프로세스가 예약되기 전에 지연될 수 있는 최대 시간입니다.
* `sched_min_granularity`: 프로세스 스케줄링 사이의 최소 시간.
* `sched_wakeup_granularity`: 프로세스가 깨어날 때 스케줄 사이의 시간.