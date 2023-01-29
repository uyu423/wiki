---
title: Java 메모리 관리 이해
description: 
published: true
date: 2023-01-29T23:50:05.362Z
tags: 
editor: markdown
dateCreated: 2023-01-29T23:50:05.362Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Understanding Java Memory Management***English** version of this document is available*](/en/Knowledge-base/Backend/understanding-java-memory-management)
{.links-list}


Java 메모리 관리는 Java 프로그래밍의 가장 중요하고 중요한 측면 중 하나입니다. 효율적이고 올바른 코드를 작성하려면 Java 메모리 관리가 작동하는 방식을 명확하게 이해하는 것이 중요합니다.

이 기사에서는 먼저 Java에서 메모리 관리가 작동하는 방식에 대한 높은 수준의 개요를 제공합니다. 그런 다음 Java 메모리 관리 시스템의 여러 부분이 어떻게 함께 작동하는지 자세히 살펴보겠습니다.

Java 메모리 관리 시스템은 힙과 스택의 두 부분으로 나뉩니다.

힙은 Java 프로그램의 모든 개체가 저장되는 곳입니다. 스택은 해당 객체에 대한 참조가 저장되는 곳입니다.

객체가 생성되면 힙에 저장됩니다. 그런 다음 해당 개체에 대한 참조가 스택에 저장됩니다. 개체가 더 이상 필요하지 않으면 참조가 스택에서 제거되고 개체는 가비지 수집 대상이 됩니다.

힙은 Young Generation과 Old Generation의 두 부분으로 나뉩니다.

젊은 세대는 모든 새로운 객체가 생성되는 곳입니다. old generation은 한동안 주변에 있던 객체가 이동되는 곳입니다.

더 이상 필요하지 않은 개체는 가비지 수집됩니다. 가비지 수집 프로세스는 사용되지 않은 개체가 힙에서 제거되는 곳입니다.

Java에는 Young Generation Garbage Collector와 Old Generation Garbage Collector의 두 가지 유형의 Garbage Collector가 있습니다.

젊은 세대 가비지 수집기는 젊은 세대의 개체 수집을 담당합니다. 구세대 가비지 수집기는 구세대의 개체 수집을 담당합니다.

가비지 수집 프로세스는 두 가지 이유로 중요합니다. 힙이 너무 꽉 차는 것을 방지하고 프로그램의 메모리 부족을 방지하는 데 도움이 됩니다.

힙이 가득 차면 Java 프로그램에서 OutOfMemoryError가 발생합니다. 이 경우 프로그램이 충돌합니다.

효율적이고 올바른 코드를 작성하려면 Java 메모리 관리 시스템의 여러 부분이 함께 작동하는 방식을 이해하는 것이 중요합니다.

Java 메모리 관리 시스템은 복잡한 주제입니다. 이 기사에서는 표면만 긁어 보았습니다. 자세한 내용은 다음 리소스를 참조하십시오.

-자바 메모리 모델
-가비지 컬렉터
-자바 가상 머신