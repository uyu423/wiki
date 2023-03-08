---
title: 056: TensorFlow.js 및 Node.js 애플리케이션 디버깅
description: 
published: true
date: 2023-02-02T20:04:29.638Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:04:27.951Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [056: Debugging TensorFlow.js and Node.js Applications***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/056-debugging-tensorflow-js-and-node-js-applications)
{.links-list}


TensorFlow.js 및 Node.js 애플리케이션 디버깅

TensorFlow.js와 Node.js는 각각 기계 학습과 웹 개발을 위한 두 가지 인기 있는 JavaScript 플랫폼입니다. 이 게시물에서는 TensorFlow.js 및 Node.js 애플리케이션을 디버깅하는 방법을 보여줍니다.

각 플랫폼의 디버깅 도구에 대한 개요부터 시작하겠습니다. 그런 다음 몇 가지 일반적인 디버깅 시나리오와 이를 해결하는 방법을 살펴보겠습니다.

## 디버깅 도구

### TensorFlow.js

TensorFlow.js 디버깅 도구는 Chrome DevTools를 기반으로 합니다. 이를 사용하려면 DevTools를 지원하는 브라우저에서 TensorFlow.js 애플리케이션을 실행해야 합니다.

브라우저에서 애플리케이션을 실행했으면 DevTools를 열고 "Sources" 탭을 선택합니다. 여기에서 중단점을 설정하고, 변수를 검사하고, 코드를 단계별로 실행할 수 있습니다.

TensorFlow.js 디버깅 도구에는 'TensorFlow.js용 디버거' 패널도 포함되어 있습니다. 이 패널은 TensorFlow.js 코드의 상위 수준 보기를 제공하며 TensorFlow.js 작업을 디버그하는 데 사용할 수 있습니다.

### Node.js

Node.js 디버깅 도구는 V8 디버깅 프로토콜을 기반으로 합니다. 이를 사용하려면 --inspect 플래그와 함께 Node.js 애플리케이션을 실행해야 합니다.

애플리케이션이 --inspect 플래그와 함께 실행되면 디버거를 연결할 수 있습니다. V8 디버깅 프로토콜을 지원하는 Visual Studio Code 디버거를 사용하는 것이 좋습니다.

디버거가 연결되면 중단점을 설정하고, 변수를 검사하고, 코드를 단계별로 실행할 수 있습니다.

## 디버깅 시나리오

### TensorFlow.js

#### 시나리오: 내 애플리케이션이 실행되고 있지 않습니다.

TensorFlow.js 애플리케이션이 실행 중이 아니면 가장 먼저 브라우저 콘솔에서 오류를 확인해야 합니다. 브라우저 콘솔은 DevTools "콘솔" 탭으로 열 수 있습니다.

브라우저 콘솔에 오류가 없는 경우 다음으로 확인할 사항은 TensorFlow.js 작업 패널입니다. 이 패널은 DevTools "TensorFlow.js용 디버거" 탭으로 열 수 있습니다.

TensorFlow.js 작업 패널에 오류가 표시되면 오류를 클릭하여 자세한 내용을 볼 수 있습니다.

#### 시나리오: 내 애플리케이션이 느리게 실행 중입니다.

TensorFlow.js 애플리케이션이 느리게 실행되는 경우 가장 먼저 확인해야 할 것은 브라우저 콘솔에서 경고를 확인하는 것입니다. 브라우저 콘솔은 DevTools "콘솔" 탭으로 열 수 있습니다.

브라우저 콘솔에 경고가 없으면 TensorFlow.js 작업 패널에서 다음으로 확인해야 합니다. 이 패널은 DevTools "TensorFlow.js용 디버거" 탭으로 열 수 있습니다.

TensorFlow.js 작업 패널에 경고가 표시되면 경고를 클릭하여 자세한 내용을 볼 수 있습니다.

#### 시나리오: 내 애플리케이션이 GPU를 사용하지 않습니다.

TensorFlow.js 애플리케이션이 GPU를 사용하지 않는 경우 가장 먼저 확인해야 할 것은 브라우저 콘솔에서 오류를 확인하는 것입니다. 브라우저 콘솔은 DevTools "콘솔" 탭으로 열 수 있습니다.

브라우저 콘솔에 오류가 없는 경우 다음으로 확인할 사항은 TensorFlow.js 작업 패널입니다. 이 패널은 DevTools "TensorFlow.js용 디버거" 탭으로 열 수 있습니다.

TensorFlow.js 작업 패널에 오류가 표시되면 오류를 클릭하여 자세한 내용을 볼 수 있습니다.

### Node.js

#### 시나리오: 내 애플리케이션이 실행되고 있지 않습니다.

Node.js 애플리케이션이 실행 중이 아니면 가장 먼저 디버거 콘솔에서 오류를 확인해야 합니다. 디버거 콘솔은 Visual Studio Code "디버그" 패널에서 열 수 있습니다.

디버거 콘솔에 오류가 없으면 다음으로 확인할 사항은 Node.js 작업 패널입니다. 이 패널은 Visual Studio Code "Node.js" 패널로 열 수 있습니다.

Node.js 작업 패널에 오류가 표시되면 오류를 클릭하여 자세한 내용을 볼 수 있습니다.

#### 시나리오: 내 애플리케이션이 느리게 실행 중입니다.

Node.js 애플리케이션이 느리게 실행되는 경우 가장 먼저 확인해야 할 것은 디버거 콘솔에서 경고를 확인하는 것입니다. 디버거 콘솔은 Visual Studio Code "디버그" 패널에서 열 수 있습니다.

디버거 콘솔에 경고가 없으면 다음으로 확인해야 할 것은 Node.js 작업 패널입니다. 이 패널은 Visual Studio Code "Node.js" 패널로 열 수 있습니다.

Node.js 작업 패널에 경고가 표시되면 경고를 클릭하여 자세한 내용을 볼 수 있습니다.

#### 시나리오: 내 애플리케이션이 CPU를 사용하지 않습니다.

Node.js 애플리케이션이 CPU를 사용하지 않는 경우 가장 먼저 디버거 콘솔에서 오류를 확인해야 합니다. 디버거 콘솔은 Visual Studio Code "디버그" 패널에서 열 수 있습니다.

디버거 콘솔에 오류가 없으면 다음으로 확인할 사항은 Node.js 작업 패널입니다. 이 패널은 Visual Studio Code "Node.js" 패널로 열 수 있습니다.

Node.js 작업 패널에 오류가 표시되면 오류를 클릭하여 자세한 내용을 볼 수 있습니다.

## 추가 정보

### TensorFlow.js

TensorFlow.js 애플리케이션 디버깅에 대한 자세한 내용은 TensorFlow.js 디버깅 설명서를 참조하세요.

### Node.js

Node.js 애플리케이션 디버깅에 대한 자세한 내용은 Node.js 디버깅 설명서를 참조하세요.