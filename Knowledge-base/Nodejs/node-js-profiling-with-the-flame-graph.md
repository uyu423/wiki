---
title: Flame 그래프로 Node.js 프로파일링
description: 
published: true
date: 2023-02-06T08:17:21.223Z
tags: 
editor: markdown
dateCreated: 2023-02-06T08:17:19.468Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Node.js Profiling with the Flame Graph***English** document is available*](/en/Knowledge-base/Nodejs/node-js-profiling-with-the-flame-graph)
{.links-list}


# Flame 그래프로 Node.js 프로파일링

Node.js 개발자로서 우리는 항상 애플리케이션을 더 빠르고 효율적으로 실행할 수 있는 방법을 찾고 있습니다. 이를 돕기 위해 Flame 그래프라는 도구를 사용할 수 있습니다.

플레임 그래프는 Node.js 애플리케이션이 가장 많은 시간을 소비하는 위치를 보여주는 일종의 성능 프로필입니다. 애플리케이션의 성능을 최적화할 수 있도록 코드의 병목 현상을 식별하는 데 유용한 방법이 될 수 있습니다.

이 기사에서는 Flame 그래프 도구를 사용하여 Node.js 애플리케이션을 프로파일링하는 방법을 살펴보겠습니다. 또한 Node.js에서 성능 프로파일링에 사용할 수 있는 다른 도구에 대해서도 알아봅니다.

## 플레임 그래프란?

플레임 그래프는 Node.js 애플리케이션이 가장 많은 시간을 소비하는 위치를 보여주는 일종의 성능 프로필입니다. 애플리케이션의 성능을 최적화할 수 있도록 코드의 병목 현상을 식별하는 데 유용한 방법이 될 수 있습니다.

Flame 그래프는 원래 Brendan Gregg가 컴퓨터 시스템의 성능을 시각화하기 위해 개발했습니다. "플레임 그래프"라는 이름은 그래프가 시각화될 때 표시되는 방식에서 유래되었으며 가장 긴 막대는 가장 많은 시간이 소요되는 영역을 나타냅니다.

 Gregg는 플레임 그래프와 성능 프로파일링 용도에 대해 광범위하게 저술했습니다. 그의 웹 사이트에서 Flame 그래프에 대한 자세한 정보를 찾을 수 있습니다.

http://www.brendangregg.com/flamegraphs.html

## Node.js 프로파일링에 Flame 그래프를 사용하는 방법

Node.js 애플리케이션용 Flame 그래프를 생성하는 몇 가지 방법이 있습니다. 이 섹션에서는 가장 널리 사용되는 두 가지 도구를 살펴보겠습니다.

### 노드 불꽃

Node Flame은 성능 프로필에서 Flame 그래프를 생성하는 Node.js 성능 프로파일링 도구입니다. Node.js 플랫폼에서 실행 중인 애플리케이션을 프로파일링하는 데 사용할 수 있습니다.

Node Flame을 사용하려면 먼저 npm 패키지 관리자를 사용하여 설치해야 합니다.

```
npm install -g node-flame
```

Node Flame이 설치되면 다음 명령을 실행하여 이를 사용하여 Node.js 애플리케이션을 프로파일링할 수 있습니다.

```
node-flame <path-to-application>
```

 Node Flame은 애플리케이션이 가장 많은 시간을 보내는 위치를 보여주는 Flame 그래프를 생성합니다. 그런 다음 이 정보를 사용하여 코드를 최적화할 수 있습니다.

### 0x

0x는 Flame 그래프를 생성하는 데 사용할 수 있는 Node.js 성능 프로파일링 도구입니다. 오픈 소스이며 GitHub에서 사용할 수 있습니다.

https://github.com/davecheney/0x

0x를 사용하려면 먼저 npm 패키지 관리자를 사용하여 설치해야 합니다.

```
npm install -g 0x
```

0x가 설치되면 다음 명령을 실행하여 이를 사용하여 Node.js 애플리케이션을 프로파일링할 수 있습니다.

```
0x <path-to-application>
```

0x는 애플리케이션이 가장 많은 시간을 소비하는 위치를 보여주는 플레임 그래프를 생성합니다. 그런 다음 이 정보를 사용하여 코드를 최적화할 수 있습니다.

## 결론

이 기사에서는 Flame 그래프와 이를 사용하여 Node.js 애플리케이션을 프로파일링하는 방법에 대해 배웠습니다. 또한 Flame 그래프를 생성하는 데 사용할 수 있는 두 가지 도구인 Node Flame과 0x도 보았습니다.

성능 프로파일링은 Node.js 애플리케이션 최적화의 중요한 부분입니다. Flame 그래프는 애플리케이션의 성능을 개선할 수 있도록 코드의 병목 현상을 식별하는 데 유용한 도구가 될 수 있습니다.