---
title: Kubernetes Operators: 맞춤형 컨트롤러로 애플리케이션 관리 자동화
description: 
published: true
date: 2023-02-09T03:23:44.316Z
tags: 
editor: markdown
dateCreated: 2023-02-09T03:23:42.742Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes Operators: Automating Application Management with Custom Controllers***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-operators-automating-application-management-with-custom-controllers)
{.links-list}


# 쿠버네티스 오퍼레이터: 맞춤형 컨트롤러로 애플리케이션 관리 자동화

이 기사에서는 Kubernetes Operator에 대해 설명합니다. Kubernetes는 컨테이너화된 애플리케이션을 자동화하기 위한 오픈 소스 시스템입니다. 오퍼레이터는 Kubernetes 애플리케이션을 패키징, 배포 및 관리하는 방법입니다. 이 기사에서는 오퍼레이터가 무엇이고 애플리케이션 관리를 자동화하는 데 오퍼레이터가 어떻게 도움이 되는지에 초점을 맞출 것입니다.

## 오퍼레이터란?

Operator는 Kubernetes 애플리케이션을 패키징, 배포 및 관리하는 방법입니다. Kubernetes Operator는 특정 유형의 애플리케이션을 관리하는 데 사용되는 Kubernetes의 소프트웨어 확장입니다. 운영자는 사용자 지정 리소스를 사용하여 애플리케이션의 상태를 나타내고 원하는 동작을 정의합니다. 사용자 지정 컨트롤러는 이러한 사용자 지정 리소스의 변경 사항을 감시하고 필요한 변경을 수행하여 응용 프로그램을 원하는 대로 계속 실행합니다.

오퍼레이터는 Kubernetes API 및 모범 사례를 사용하여 구축됩니다. 이를 통해 Kubernetes 구현 간에 이식 가능하고 쉽게 확장할 수 있습니다.

## 연산자를 사용하는 이유는 무엇입니까?

연산자는 애플리케이션 관리에 대한 선언적 접근 방식을 제공합니다. 즉, 원하는 애플리케이션 상태를 설명할 수 있으며 운영자는 애플리케이션이 해당 상태에 도달하고 유지되도록 합니다.

운영자는 또한 애플리케이션 관리를 자동화하는 방법을 제공합니다. 응용 프로그램은 복잡할 수 있으며 올바르게 배포하고 구성하려면 다양한 구성 요소가 필요합니다. 이는 시간이 오래 걸리고 오류가 발생하기 쉬운 프로세스일 수 있습니다. 운영자는 이 프로세스를 자동화하여 애플리케이션을 더 쉽고 빠르게 배포하고 관리할 수 있습니다.

운영자는 또한 애플리케이션의 수명 주기를 관리하는 데 도움을 줄 수 있습니다. 여기에는 애플리케이션 업그레이드 및 다운그레이드, 애플리케이션 확장 또는 축소와 같은 작업이 포함됩니다.

## 오퍼레이터는 어떻게 사용하나요?

연산자는 CRD(사용자 지정 리소스 정의)로 배포됩니다. CRD는 기존 Kubernetes 리소스에 추가되는 주석입니다. 이를 통해 운영자는 리소스의 변경 사항을 감시하고 필요한 조치를 취할 수 있습니다.

Operator는 Custom Controller로도 배포됩니다. 사용자 지정 컨트롤러는 사용자 지정 리소스의 변경 사항을 감시하는 Kubernetes 컨트롤러입니다. 변경 사항이 감지되면 컨트롤러는 리소스가 원하는 상태에 도달하도록 필요한 조치를 취합니다.

## 연산자 작성하기

연산자는 Go로 작성되었습니다. Operator SDK는 Kubernetes Operator를 쉽게 작성, 구축 및 배포할 수 있게 해주는 툴킷입니다. SDK는 CLI, 스캐폴딩 및 테스트 도구를 제공합니다.

오퍼레이터는 Kubernetes API 및 모범 사례를 사용하여 구축됩니다. 이를 통해 Kubernetes 구현 간에 이식 가능하고 쉽게 확장할 수 있습니다.

Operator SDK CLI를 사용하여 Operator에 대한 스캐폴딩을 생성할 수 있습니다. 여기에는 CRD(Custom Resource Definition) 및 Custom Controller가 포함됩니다.

스캐폴딩이 생성되면 Operator를 구현할 수 있습니다. 운영자는 사용자 지정 리소스의 변경 사항을 감시하고 필요한 조치를 취해야 합니다.

kubectl 또는 Operator SDK CLI를 사용하여 Kubernetes에 Operator를 배포할 수 있습니다.

## 결론

이 기사에서는 Kubernetes Operator에 대해 논의했습니다. 오퍼레이터가 무엇이며 애플리케이션 관리를 자동화하는 데 어떻게 도움이 되는지 살펴보았습니다. 또한 Operator를 작성하고 배포하는 방법도 살펴보았습니다.