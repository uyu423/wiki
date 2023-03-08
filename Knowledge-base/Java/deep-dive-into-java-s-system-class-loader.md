---
title: Java의 시스템 클래스 로더에 대해 자세히 알아보기
description: 
published: true
date: 2023-02-26T16:32:20.661Z
tags: 
editor: markdown
dateCreated: 2023-02-26T16:32:19.232Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Deep Dive into Java's System Class Loader***English** document is available*](/en/Knowledge-base/Java/deep-dive-into-java-s-system-class-loader)
{.links-list}


# 자바의 시스템 클래스 로더에 대해 자세히 알아보기

시스템 클래스 로더는 JRE(Java Runtime Environment)에서 사용하는 기본 클래스 로더입니다. 파일 시스템 및 클래스 경로에서 클래스 파일을 로드합니다. 이 기사에서는 시스템 클래스 로더의 작동 방식과 사용 방법에 대해 자세히 알아봅니다.

## 클래스 로더란?

클래스 로더는 파일 시스템 또는 네트워크에서 클래스 파일을 로드하고 JVM(Java Virtual Machine)에서 사용할 수 있도록 만드는 프로그램입니다. 클래스 로더는 런타임에 클래스를 로드하는 데 사용됩니다.

Java에는 세 가지 유형의 클래스 로더가 있습니다.

- 부트스트랩 클래스로더
- 확장 클래스 로더
- 시스템 클래스 로더

Bootstrap ClassLoader는 rt.jar 파일에서 java.lang.Object와 같은 핵심 Java 클래스를 로드합니다. Extension ClassLoader는 ext 폴더에서 클래스를 로드합니다. System ClassLoader는 클래스 경로에서 클래스를 로드합니다.

## 시스템 클래스 로더는 어떻게 작동합니까?

시스템 클래스 로더는 파일 시스템 및 클래스 경로에서 클래스 파일을 로드합니다. 파일 시스템은 로컬 시스템의 파일 시스템입니다. 클래스 경로는 시스템 클래스 로더가 클래스 파일을 검색하는 위치 목록입니다.

시스템 클래스 로더는 3단계 프로세스를 사용하여 클래스 파일을 로드합니다.

1. 시스템 클래스 로더는 파일 시스템에서 클래스 파일을 검색합니다.
2. 클래스 파일이 없으면 시스템 클래스 로더는 클래스 파일의 클래스 경로를 검색합니다.
3. 클래스 파일이 없으면 시스템 클래스 로더가 네트워크에서 클래스 파일을 로드합니다.

시스템 클래스 로더는 파일 시스템, 클래스 경로 또는 네트워크에서 클래스 파일을 로드할 수 있습니다.

## 시스템 클래스 로더를 사용하는 방법?

시스템 클래스 로더는 파일 시스템, 클래스 경로 또는 네트워크에서 클래스 파일을 로드하는 데 사용할 수 있습니다.

파일 시스템에서 클래스 파일을 로드하려면 java.lang.ClassLoader.getSystemResourceAsStream() 메소드를 사용할 수 있습니다. 이 메서드는 파일 시스템에서 클래스 파일을 읽는 데 사용할 수 있는 InputStream을 반환합니다.

클래스 경로에서 클래스 파일을 로드하려면 java.lang.ClassLoader.getSystemResourceAsStream() 메소드를 사용할 수 있습니다. 이 메서드는 클래스 경로에서 클래스 파일을 읽는 데 사용할 수 있는 InputStream을 반환합니다.

네트워크에서 클래스 파일을 로드하려면 java.lang.ClassLoader.getSystemResourceAsStream() 메소드를 사용할 수 있습니다. 이 메서드는 네트워크에서 클래스 파일을 읽는 데 사용할 수 있는 InputStream을 반환합니다.

## 결론

이 기사에서는 Java의 시스템 클래스 로더에 대해 자세히 살펴보았습니다. 우리는 클래스 로더가 무엇이며 시스템 클래스 로더가 어떻게 작동하는지 살펴보았습니다. 또한 시스템 클래스 로더를 사용하여 파일 시스템, 클래스 경로 또는 네트워크에서 클래스 파일을 로드하는 방법도 살펴보았습니다.